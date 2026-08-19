---
type: policy
title: Worktree isolation
description: Where worktrees live, how they are named, and what is shared versus isolated — so concurrent agents in one repository can never collide.
preload: mandatory
---

# Worktree isolation

Several agents working one repository at once need real isolation, not
discipline. A worktree gives each its own directory and branch over one shared
object database — but only the *tracked* files come with it. **Everything that
makes a checkout runnable is untracked, and none of it arrives on its own.**

These rules exist so no situation requires judgement. Where a rule looks
excessive, it is closing an edge case that has bitten somebody.

## Worktrees live outside the repository

```
<repo>/                     the main checkout
<repo>.worktrees/<slug>/    every linked worktree
```

**Never inside the repository, even gitignored.** A gitignored directory inside
the tree is one `.gitignore` mistake away from being committed, and every tool
that walks the tree — scanners, linters, formatters, test discovery — now walks
*n* copies of the codebase. A secrets scanner reporting the same `.env` five
times is the mild version; a formatter rewriting another agent's working files
is not.

Outside, the main checkout stays exactly as clean as it was, and contamination
is impossible rather than prevented.

## One branch, one worktree, one agent

**Git enforces the first part**: a branch can be checked out in exactly one
worktree, and a second attempt fails. That is a feature — it is the collision
detector — but only if branch names cannot accidentally coincide.

```
agent/<task-slug>          branch
<repo>.worktrees/<task-slug>/   directory
```

The slug appears in both, so a directory maps to a branch by inspection and
neither can drift. Namespacing under `agent/` keeps them out of the way of
branches people create by hand.

**An agent must be able to tell where it is without asking:**

```sh
git rev-parse --show-toplevel      # which worktree
git branch --show-current          # which branch
git rev-parse --git-common-dir     # the shared object database
```

## What is shared, and what is not

| | |
| --- | --- |
| **Shared** — one copy, all worktrees | object database, refs, remotes, `config`, hooks, stash |
| **Per-worktree** — separate, and empty on creation | working files, index, `HEAD`, **everything untracked** |

That second row is the whole problem. `.env`, installed dependencies, build
output, local databases and generated config are all untracked, so a new
worktree has **none of them** and will not run until something puts them there.

## Provision from `.worktreeinclude`

A project declares what a worktree needs in a **`.worktreeinclude`** at its
root, in `.gitignore` syntax:

```gitignore
.env
.env.*
!.env.example
config/local.yml
certs/*.pem
```

**Only files that match a pattern *and* are already gitignored are copied.**
That second condition is the safety rule and it is doing real work: a tracked
file can never be duplicated into a worktree, so the pattern list cannot cause
two copies of something git is managing.

Everything else is absent by design. **Dependencies are reinstalled, not
copied** — `node_modules`, `.venv`, `dist`, `target` and build caches are
frequently invalid in a new path, and some embed the absolute directory they
were built in. Slower once, correct always.

Copy with **mode preserved** and parent directories created. A `0600` key that
arrives as `0644` is a security regression introduced by the provisioning step
itself, which is the worst place to have one.

## Secrets are copied deliberately, and never widened

Copying `.env` into a sibling directory does not meaningfully increase exposure
— it is already unencrypted on the same disk, owned by the same user. The risks
are different:

- **A worktree outliving its task**, holding credentials nobody remembers.
  Removing a worktree the moment its branch merges is the mitigation, and it is
  why teardown is a step rather than a habit.
- **A secret reaching the repository** because a worktree sat inside it. Ruled
  out by the location rule above.

**Never generate or invent credentials for a worktree.** If a required file is
missing from the main checkout, stop and say so. A worktree that silently comes
up with a placeholder produces failures that look like bugs in the code.

## Anything holding a port or a name needs a per-worktree value

Two agents running a dev server on the same port is the most common collision,
and it surfaces as an unrelated error.

**Derive it from the slug, not from position in the worktree list.** Position
shifts the moment any other worktree is removed, silently reassigning the port
of a process already running.

```sh
OFFSET=$(( 0x$(printf '%s' "$SLUG" | shasum | cut -c1-4) % 6900 ))
PORT=$(( 3100 + OFFSET ))
```

**Hex, with an explicit `0x`.** Extracting decimal digits from a hash and doing
arithmetic on them is a common recipe and it is broken: digits beginning with
`0` are read as octal, so any hash yielding `08…` or `09…` fails outright. It
works until a branch name happens to produce one.

The same prefixing applies to every shared namespace — container names, compose
project, database name, cache directory. Anything two agents could both claim
takes the slug.

**Where the derived value lives.** Git has per-worktree configuration, gated
behind an extension enabled once per repository:

```sh
git config --global extensions.worktreeConfig true   # once, per repo
git config --worktree luma.port "$PORT"
```

That is the right home for a value that must differ per worktree. Where the
application reads an env file instead, **append — never rewrite.** Truncating a
file that was just provisioned destroys it, and the failure looks like the copy
never happened.

## Cleanup is part of the task, not a periodic chore

**Remove the worktree when the branch merges.** Not weekly, not when disk fills
— at merge, as the last step of the work.

Two things surprise people, and both are deliberate:

**Removing a worktree never deletes its branch.** Git will not discard history
as a side effect of cleaning a directory.

**Deleting the directory by hand leaves metadata behind** in the shared git
directory, and that entry keeps the branch locked to a worktree that no longer
exists. `git worktree remove` handles both; `rm -rf` requires
`git worktree prune` afterwards.

## Submodules do not come along

A new worktree does not initialise submodules, and multi-worktree submodule
support is still incomplete. A project using them must initialise per worktree
and should expect rough edges — this is the one case where "it just works" is
not achievable and the honest answer is to say so.
