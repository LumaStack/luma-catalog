---
type: workflow
title: Close a session
description: Wind a session down for good — land everything durably, shut down what is running, and leave nothing that only exists in this machine or this conversation. Use when stopping with no idea when work resumes.
---

# Close a session

**We are done.** Not *continue somewhere else* — that is [[session-handoff]],
and it has a successor to build for. This has none, so everything it produces
has to stand on its own in the repository, and its effort goes into shutting
things down rather than setting them up.

| | |
| --- | --- |
| **reader** | a stranger, at an unknown time. It may be you, having forgotten everything |
| **budget** | whatever it takes. Nothing is left to protect |
| **ends with** | no note, nothing running, and a repository that can be picked up cold |

## The exit test

**Could someone with only this repository — no agent memory, no state directory,
no access to this machine — pick this up?**

If no, something is in the wrong place. Checkpoint and handoff cannot pass this
test and do not need to. Close is defined by it.

## 1. Drain the session note

Read every note this session wrote:

```sh
cat ~/.local/state/luma/sessions/<project>/<branch>.md 2>/dev/null
```

**Go line by line and ask: does this exist anywhere else?** Anything that does
not gets a durable home now, via [[where-knowledge-goes]], or is deliberately
dropped and said to be dropped.

This is the step that makes deleting the note safe. Skipping it is how a
session's entire learned state evaporates while looking like a clean shutdown.

## 2. Land everything, with the user

```sh
git status --short && git diff --stat
```

Show them and ask in **one message** — commit all, some, or leave it. Then push,
because a branch that exists only here does not survive the machine.

**Close cannot leave the mess a handoff can.** There is nobody to explain it to,
so anything you leave, somebody finds later with no way to ask.

- A pull request opened? Give it a real description; a draft with an empty body
  is a puzzle for whoever finds it.
- A branch nobody will return to? Say so in the record, or merge it, or delete
  it — with the user's agreement.

## 3. Shut down what is running

Background processes, dev servers, subagents, worktrees. **Stop them.**

Worktrees especially: an abandoned one holds a branch checked out, so a future
session cannot check that branch out and will be told the reason in terms that
make no sense to them.

## 4. Give the loose ends a home

**Everything unfinished becomes something, or it evaporates**, because the note
is about to be deleted.

- **Will be picked up** → an idea or a backlog item.
- **Will not be picked up** → **recorded as deliberately abandoned**, with what
  was tried and why it was dropped.

Abandonment is a real outcome and worth the same care as a decision. Without it
the next person restarts the dead end, spends the same hours, and reaches the
same wall — the failure the whole *record the dead ends* habit exists to
prevent.

## 5. Retrospective — this is the only workflow that sees the whole arc

Checkpoint is mid-flight and handoff is aimed at a successor. Close is the only
one that can look back at the entire session, which makes it **the only place
this practice gets better.**

It is also the step most likely to be skipped, because the session is ending and
everybody wants to leave. Do it anyway.

- What worked, and would be worth doing again.
- What was wasted — time spent on the wrong thing, and what the earlier signal
  was.
- What should become a policy, a memory, or an idea. Route it.

## 6. Apply the learnings, or queue them explicitly

**If there is time, apply them now.** A learning recorded and never applied is a
learning that did not happen, and close is the natural moment: the work is done,
nothing is in flight, and the change is small and obvious while the session is
still fresh. A misleading comment, a missing line in the readme, a policy that
sent you the wrong way — fix it.

**If you are in a hurry, capture it as work to do next time**, and capture it as
work rather than as an observation. *"The contributing guide describes the old
gate path"* is a note nobody acts on. *"Update `CONTRIBUTING.md` to the current
gate path — it still says the pre-rename one"* is a thing somebody can pick up
in five minutes.

**Say which learnings were applied and which were queued.** Otherwise a reader
cannot tell a fixed problem from an open one, and the queued ones look like
history rather than work.

## 7. Pin the world

The note is going, so the record that replaces it must say **what was true when
it was written**:

- Commit, branch, open pull request numbers and their state.
- Versions of anything that matters — tool, spec, dependency.
- The date.

Read in six months, *next: rerun the gate tests* may name a file that no longer
exists on a branch that merged. Pinning is what lets a reader tell **still true**
from **was true in August**, and it is the difference between a useful record and
a confidently misleading one.

## 8. Delete the note

Last act. By step 1 everything in it lives somewhere else, so this costs
nothing — and leaving it is not free: **a `close` note found later means the
close did not finish**, and a reader has no way to know whether its contents
ever reached a durable home.

```sh
rm ~/.local/state/luma/sessions/<project>/<branch>.md
```

If it is worth keeping for audit or study, it moves to
`.luma/records/sessions/<date>-<slug>.md` and becomes a record — dated,
append-only, never edited. **That is the exception, not the default.** See
[[session-continuity]].

## 9. Tell the user what was left

Short and specific:

- What landed, and where — paths and pull request numbers.
- What was **deliberately abandoned**, so they can object while somebody still
  remembers.
- Which learnings were applied, and which are queued.
- What is still open, and what would restart it.
- **Recommended practices this project does not have**, if any — filtered by the
  catalog's `requires` obligation, not everything that was skipped. Name the gap
  and the command that closes it, and leave it there: adoption is a durable
  change to the repository, and somebody who is shutting down is not in a
  position to decide on one. See [[where-knowledge-goes]].

**No prompt for a successor**, because there is not one. If it turns out there
is, that was a [[session-handoff]].
