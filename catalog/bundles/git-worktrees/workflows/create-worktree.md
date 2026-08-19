---
type: workflow
title: Create a worktree
description: Create an isolated worktree for a task, provision what it needs to run, and verify it before starting work. Use before beginning any task that runs alongside another agent.
preload: mandatory
---

# Create a worktree

Every step here closes a failure that otherwise appears later as something
unrelated. Run them in order; do not skip verification.

## 1. Establish the slug

```sh
SLUG=<short-kebab-task-name>
REPO=$(git rev-parse --show-toplevel)
TREE="${REPO}.worktrees/${SLUG}"
BRANCH="agent/${SLUG}"
```

The slug is the identity of the whole thing — directory, branch, port offset,
container names. Keep it short, kebab-case, and derived from the task.

**Run this from the main checkout.** Creating a worktree from inside another
worktree works, but the relative paths below will be wrong.

## 2. Fail fast on collisions

```sh
git show-ref --verify --quiet "refs/heads/${BRANCH}" && echo "branch exists"
test -e "$TREE" && echo "directory exists"
git worktree list --porcelain | grep -q "^worktree ${TREE}$" && echo "worktree exists"
```

Any of these means another agent is already on this task, or a previous one did
not clean up. **Stop and resolve it** — do not append `-2` to the slug. A second
worktree for the same task is how two agents end up doing the same work and
merging conflicting versions of it.

## 3. Create it

```sh
git worktree add -b "$BRANCH" "$TREE"
```

This creates the branch from the current `HEAD` and checks it out in one step.
Branch from an explicit base when the default is not what you want:

```sh
git worktree add -b "$BRANCH" "$TREE" origin/main
```

## 4. Provision what the checkout needs to run

**Only the files the project names.** Default is `.env` and its variants:

```sh
for f in .env .env.local; do
  [ -f "$REPO/$f" ] && cp "$REPO/$f" "$TREE/$f"
done
```

**If a required file is missing from the main checkout, stop and say so.** Do
not fall back to `.env.example`, and do not invent values — a worktree that
comes up with placeholder credentials fails in ways that look like bugs in the
code, sometimes hours later.

**Never copy dependencies or build output.** `node_modules`, `.venv`, `dist`,
`target`, `.next` and caches are regenerated. Copied ones are often invalid in a
new path, and some embed the absolute directory they were built in.

## 5. Install dependencies

```sh
cd "$TREE" && <the project's install command>
```

Prefer the offline or frozen-lockfile form. This is the slow step, and it is the
price of a checkout that is actually correct.

## 6. Claim a port and namespace anything shared

```sh
OFFSET=$(( 0x$(printf '%s' "$SLUG" | shasum | cut -c1-4) % 1000 ))
PORT=$(( 3000 + OFFSET ))
```

**Derived from the slug, never from position in `git worktree list`.** Position
shifts the moment another worktree is removed, which would silently reassign the
port of a process already running.

Apply the same prefix to every shared namespace the project touches — container
names, compose project name, database name, cache directory. Anything two
agents could both claim needs the slug in it.

## 7. Initialise submodules, if there are any

```sh
git submodule update --init --recursive
```

They are not inherited. Multi-worktree submodule support is incomplete, so
verify rather than assume this worked.

## 8. Verify before starting work

```sh
cd "$TREE"
git rev-parse --show-toplevel        # this worktree, not the main one
git branch --show-current            # agent/<slug>
<the project's test command>
```

**A clean test baseline before the first edit is the highest-value step here.**
Without it, the first failure is ambiguous — a pre-existing break and a break
you just caused look identical, and distinguishing them costs more than this
step ever will.
