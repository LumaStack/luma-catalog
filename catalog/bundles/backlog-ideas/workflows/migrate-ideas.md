---
type: workflow
title: Migrate an IDEAS file
description: Move ideas out of a single IDEAS.md into individual files, verify nothing was lost, and only then remove the original. Use once per project that has one.
---

# Migrate an IDEAS file

A one-off per project. The risk is not the moving — it is **removing the
original before anybody has checked**, so verification is a step rather than a
feeling.

## 1. Read the whole file first

Not every entry deserves to survive. A long-lived `IDEAS.md` accumulates things
that were done, abandoned, or overtaken, and **migrating them unchanged
launders stale material into the place people are told to trust.**

For each entry, decide: *migrate*, *drop*, or *already happened*.

**Record what you drop and why**, in the commit if nowhere else. *We
deliberately stopped wanting this* is worth keeping; silence is not.

## 2. Decide where each one lives

Per entry, using [[where-an-idea-lives]]: **who would act on this?**

An organization-scoped idea belongs in the organization's `.luma/`, not in
whichever repository the file happened to sit in. **This is the step most worth
slowing down for** — an idea migrated into the wrong place is one the people who
would act on it never see, and nothing announces it.

Default to `project` when unclear.

## 3. Check whether a version already exists

```sh
grep -ril "<a distinctive word>" .luma/backlog/ideas/
```

**If one does**, do not create a second. Read both, decide what this entry adds
that the existing idea lacks, propose the merge, get agreement, then append and
add the original's author to `contributors`.

## 4. Otherwise create it

Follow [[capture-idea]] from step 1, with two differences:

- **`captured` is the date the idea was written, not today** — if the file or
  its history says. Backdating to today erases how long something has been
  waiting, which is exactly what the tending session reads.
- **`originated` is whoever actually had it.** If that is unrecoverable,
  `unknown:unknown` is honest and better than guessing.

## 5. Mark it migrated, in the original

In `IDEAS.md`, against each entry:

```markdown
> *Migrated to `.luma/backlog/ideas/<slug>.md`.*
```

**Do not delete anything yet.** The marker is what makes step 6 possible, and a
half-finished migration with no markers is worse than one not started.

## 6. Verify before removing anything

**Both a person and an agent, if you can get both.** They miss different things:
an agent catches an entry with no marker, a person catches an entry whose
meaning did not survive the rewrite.

- Every entry has a marker, or an explicit note that it was dropped
- Every named file exists
- Nothing acquired detail that was not in the original — **migration is not
  the moment to improve an idea**, and an idea silently enlarged during a move
  is one nobody agreed to

## 7. Archive, then delete on confirmation

**Archiving needs nobody's permission. Deleting needs the user's.**

The same rule as pruning, for the same reason: the original is somebody's work,
and a migration that ate it silently is the version of this that goes wrong.

Once confirmed, **delete the original.** Leaving it is the worst outcome — two
places holding the same ideas, drifting apart, with nothing saying which is
current. The history keeps it.
