---
type: workflow
title: Migrate an IDEAS file
description: Move ideas out of a single IDEAS.md into individual files, verify nothing was lost, and only then remove the original. Use once per project that has one.
---

# Migrate an IDEAS file

A one-off per project. The risk is not the moving — it is **removing the
original before anybody has checked**, so verification is a step rather than a
feeling.

## 1. Ask how involved they want to be

**Before reading anything**, because it changes how every step below is run.

| | |
| --- | --- |
| **delegated** | run the whole thing and record what happened. They read the result |
| **reviewed** | propose in batches — a table of title, one-line explanation, and where each would go — take feedback, and repeat until they are ready to sign off |
| **together** | one idea at a time: show what is needed to judge it, recommend where it goes, and decide keep-or-prune jointly |

**Ask rather than assume.** A long `IDEAS.md` is somebody's accumulated
thinking, and running `delegated` over it uninvited is how a migration becomes
something that happened *to* them.

**`delegated` still stops at step 9.** Deleting the original always needs their
confirmation, whichever mode is chosen — the mode governs how much they are
consulted along the way, never whether they consent to the destructive step.

## 2. Find out where ideas can go

**Before deciding where anything belongs, establish what *where* can mean.**
Migrating into the wrong place is the failure that matters here, and it is
silent — an idea filed under the wrong organization is one the people who would
act on it never see.

At minimum, ask. Four questions:

- **Which organization is this repository under**, and is there more than one in
  play? Somebody working across two is the case that goes wrong.
- **What other projects exist** that an idea might belong to?
- **Is there a headquarters** for any of those organizations?
- **If there is no headquarters**, where do private ideas belong?

**That last one is the only question here whose wrong answer cannot be undone.**
An organization-scoped idea often names customers, people, or strategy, and the
tempting move with nowhere obvious to put it is whichever repository happens to
be open. If that one is public, the idea is published permanently — deleting it
afterwards no more unpublishes it than deleting a committed credential does.

**With no private destination, do not file sensitive or private ideas.** Say so,
hold the idea, and ask. A private repository that already exists, or somewhere
outside git entirely, both beat the nearest convenient place.

Ordinary ideas are unaffected — most are not sensitive, and the absence of a
private home is no reason to stop migrating the ones that were never private.

Cheap discovery that narrows the questions rather than replacing them:

```sh
git remote -v                       # which organization this repository belongs to
ls -d ../*/.git 2>/dev/null         # sibling repositories, if they are checked out side by side
```

**Confirm what you find rather than acting on it.** Sibling directories are a
hint about what somebody has cloned, not a statement about what exists — and a
remote tells you where this repository lives, not where an idea should.

**A destination may not exist yet, and may not want to.** A repository with no
ideas directory needs one created and said so. A repository with **no luma at
all** is a different case: do not install `.luma/` there to make room for an
idea — ask, and if the answer is no, use whatever that repository already keeps
prose in. If a user agrees to adding `.luma/`, ask if it's their intention to
conform all affected repositories to using the standardized `.luma/` layout.

*The better version is not implemented: asking foreman or a headquarters for
this on the user's behalf.* A headquarters has the breadth to answer properly,
where a single checkout can only guess from what happens to be nearby.

## 3. Read the whole file first

Not every entry deserves to survive. A long-lived `IDEAS.md` accumulates things
that were done, abandoned, or overtaken, and **migrating them unchanged
launders stale material into the place people are told to trust.**

For each entry, decide: *migrate*, *drop*, or *already happened*.

**Record what you drop and why**, in the commit if nowhere else. *We
deliberately stopped wanting this* is worth keeping; silence is not.

## 4. Decide where each one lives

Per entry, against the destinations from step 2: **who would act on this?**
[[where-an-idea-lives]] has the scope call.

**This is the step most worth slowing down for.** Everything before it was
preparation; this is where an idea gets put somewhere it will or will not be
found.

**Ask for guidance, or lean towards `project`, when it is unclear.** A
project-scoped idea is cheap to promote later; one filed under an organization
nobody checks is the kind that goes quiet.

**When nothing fits, say so rather than forcing it.** The three scopes are a
first guess, and a migration is the first time many ideas meet them at once —
which makes it the best opportunity to find out where they are wrong.

Record the mismatch: *this belongs to a customer, a product line, a
community, something that is not a project and not the organization.* That note
is the evidence the list needs to grow, and **the `project` default is what
destroys it** — an awkward idea quietly filed as `project` looks exactly like a
well-placed one, and the signal is gone.

## 5. Check whether a version already exists

```sh
grep -ril "<a distinctive word>" <ideas-directory>/
```

**If one does**, do not create a second. Read both, decide what this entry adds
that the existing idea lacks, propose the merge, get agreement, then append and
add the original's author to `contributors`.

## 6. Otherwise create it

Follow [[capture-idea]] from step 1, with two differences:

- **`created.at` is when the idea was written, not today** — if the file or its
  history says. Backdating to today erases how long something has been waiting,
  which is exactly what a tending session reads.
- **`created.by` is whoever actually had it.** If that is unrecoverable,
  `unknown:unknown` is honest and far better than guessing — a name attached to
  an idea somebody never had is the one error here worth avoiding outright.

## 7. Mark it migrated, in the original

In `IDEAS.md`, against each entry:

```markdown
> *Migrated to `<ideas-directory>/<slug>.md`.*
```

**Do not delete anything yet.** The marker is what makes step 6 possible, and a
half-finished migration with no markers is worse than one not started.

## 8. Verify before removing anything

**Both a person and an agent, if you can get both.** They miss different things:
an agent catches an entry with no marker, a person catches an entry whose
meaning did not survive the rewrite.

- Every entry has a marker, or an explicit note that it was dropped
- Every named file exists
- Nothing acquired detail that was not in the original — **migration is not
  the moment to improve an idea**, and an idea silently enlarged during a move
  is one nobody agreed to

## 9. Archive, then delete on confirmation

**Archiving needs nobody's permission. Deleting needs the user's.**

The same rule as pruning, for the same reason: the original is somebody's work,
and a migration that ate it silently is the version of this that goes wrong.

Once confirmed, **delete the original.** Leaving it is the worst outcome — two
places holding the same ideas, drifting apart, with nothing saying which is
current. The history keeps it.
