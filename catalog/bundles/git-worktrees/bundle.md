---
type: bundle
version: 0.1.0
published: 2026-08-18
consumers: [project]
entry_point: policy/worktree-isolation
description: Isolated worktrees for concurrent agents in one repository — where they live, what has to be provisioned, and how to tear them down without leaving wreckage.
---

# Git worktrees

Two agents editing one checkout stop working within minutes. A worktree gives
each its own directory and branch over one shared object database, and Git
enforces the part that matters: **a branch can be checked out in exactly one
worktree**, so a collision fails loudly instead of silently interleaving edits.

What Git does *not* do is make the new checkout runnable. **Only tracked files
come with a worktree**, and everything that makes a repository work — `.env`,
installed dependencies, generated config, local databases — is untracked. A
fresh worktree has none of it.

That gap is what this bundle closes.

## What is here

- [[worktree-isolation]] — where worktrees live, how they are named, what is
  shared, and what has to be provisioned. Read first.
- [[create-worktree]] — create one, provision it, verify it before starting.
- [[remove-worktree]] — tear it down completely, at merge.
- [[repair-worktrees]] — the states worktrees get stuck in, and which fix
  applies to which.

## The rules that eliminate the edge cases

**Worktrees live outside the repository**, never inside it even gitignored. One
`.gitignore` mistake away from committing them, and every tool that walks the
tree — scanners, formatters, test discovery — otherwise walks *n* copies of the
codebase.

**The slug is the identity** of the directory, the branch, the port offset and
every namespaced resource. One name, so nothing can drift out of sync.

**Ports derive from a hash of the slug, not from position** in `git worktree
list`. Position changes when any other worktree is removed, silently reassigning
the port of a process already running.

**Provision from `.worktreeinclude`**, in `.gitignore` syntax at the repository
root — and copy only files that match **and are already gitignored**. That
second condition means a tracked file can never be duplicated, whatever the
patterns say.

**Never invent a missing credential.** Stop and say so. A worktree that comes up
with a placeholder produces failures that look like bugs in the code, hours
later and somewhere else.

## Where "it just works" is not achievable

**Submodules.** They are not inherited, multi-worktree support is still
incomplete, and a project using them should expect rough edges. Said plainly
rather than papered over — a workflow claiming to handle them would be lying.

## Consumers

`project` only. Worktrees are a property of one repository's checkout.

## Three corrections to published practice

Each is a failure that exists in tooling or guides in current use:

**Position-derived ports.** Several guides compute a port from a worktree's
index in `git worktree list`. That index shifts when any *other* worktree is
removed, silently reassigning the port of a running process.

**Decimal digits from a hash.** A widely copied setup script extracts digits
with `tr -d -c '0-9'` and does arithmetic on them. A result beginning with `0`
is read as octal, so any `8` or `9` is a fatal error — intermittent, and
determined by the branch name. Use hex with an explicit `0x`.

**Truncating a provisioned file.** The same script copies `.env.local` and then
writes the derived port with `cat >`, destroying the file it just copied. The
failure looks exactly like the copy never happened. **Append.**

## Version

`0.1.0`. Assembled from current practice, corrected where that practice is
fragile, and **run by no fleet of agents on a real project yet.** The submodule
section in particular is a placeholder rather than a solution.

## Sources

- [Git Worktree Isolation Patterns for Parallel AI Agent Development](https://zylos.ai/research/2026-02-22-git-worktree-parallel-ai-development/) — failure modes and per-worktree provisioning
- [git-worktree documentation](https://git-scm.com/docs/git-worktree) — `prune`, `repair`, `lock`, `move`
- [Git Worktrees for AI Coding Agents](https://nimbalyst.com/blog/git-worktrees-for-ai-coding-agents-complete-guide/)
- [Git Worktree: Pros, Cons, and the Gotchas Worth Knowing](https://joshtune.com/posts/git-worktree-pros-cons/) — branch exclusivity, stale metadata
- [Fix: Git Worktree Not Working](https://fixdevs.com/blog/git-worktree-not-working/) — submodules, locked worktrees
