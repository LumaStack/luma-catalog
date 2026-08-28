---
type: policy
title: How a sweep is stored
description: Where a review sweep lives, why it is backlog rather than a record, and the two units — the file that must be covered and the cluster actually reviewed in one go.
matches:
  - topic: running or resuming a review sweep
  - path: ".luma/backlog/reviews/**"
---

# How a sweep is stored

A **sweep** is a person reading their own codebase from one end to the other,
with an agent beside them. It runs for as long as it takes — days, usually more
— and survives every session boundary in between.

```
.luma/backlog/reviews/the-cli-surface/
  sweep.md                    scope, exclusions, the order chosen, the index
  sittings/
    001-entrypoint-and-args.md
    002-the-permission-gate.md
```

## It is backlog, not a record

**The tier is decided by lifecycle, and a sweep in progress is an intention.**
It churns — the index is edited at every sitting, files are added when the tree
moves under it, units go from pending to reviewed. `records/` is append-only and
never edited, so a sweep filed there would break the tier on its first day.

**This is the difference from an audit, and it is worth stating plainly because
the two look alike from a distance.**

| | **audit** | **sweep** |
| --- | --- | --- |
| pinned to | one commit | nothing — the code moves as you go |
| written by | an auditor, for somebody else | the person reading, for themselves |
| the fixing | is somebody else's response, later | happens in the same sitting |
| independence | required between finding and answering | impossible, and not wanted |
| ends as | a settled exchange | nothing — the outputs went elsewhere |

**Do not file a sweep as an audit to make it look more rigorous.** An audit's
value comes from a pinned commit and a party that did not write the finding
answering it. A sweep has neither and is not trying to: it is one person
building a model of their own system, fixing what they find on the way. Forcing
it into the audit shape produces a commit pin that is false by the third file
and a response written by the auditor, which is the one thing that shape exists
to prevent.

*The `audit-records` bundle owns audits. Where a sweep turns up something that
genuinely wants an independent answer, that is a finding to raise there — not a
reason to restructure the sweep.*

## The sittings are the source; the index is a cache

`sweep.md` carries a table of every in-scope file and its status. **That table
is an index and can be rebuilt** — the truth is in the sittings, each of which
says which files it covered.

This matters the first time the table and the notes disagree, which they will.
A sitting note is written once and never revised; a table cell is edited every
time anything happens. **When they conflict, the notes win**, and the table is
regenerated from them rather than argued with.

*Storing derived status is a thing records must never do, for a reason that does
not reach here: it forces somebody to edit a document they did not write. A
sweep has one writer. The prohibition is about authorship, not about
derivation.*

## Two units, and confusing them is the common failure

**The unit of coverage is the file.** Every file in scope appears in the index,
so *reviewed and clean* stays distinguishable from *never looked at*. A sweep
that cannot tell those apart has produced confidence it did not earn.

**The unit of a sitting is a cluster** — a module, an execution path, a
directory that means something. You review six files together because they only
make sense together.

Reviewing files in isolation because the index is a list of files is the mistake
this distinction exists to prevent. **A file read without its collaborators is
read as a stranger**: you can see that a function is called and not whether the
caller holds the lock it assumes. The index is a coverage ledger, not a running
order.

**One sitting, one note, several files marked off.** A sitting that covers one
file is fine when the file genuinely stands alone. A sitting that covers thirty
is not a sitting; it is a skim with a note attached.

## Naming

**The sweep directory is a slug for what is being read** — `the-cli-surface`,
`everything`, `docs-and-prose`. No date, and no commit: a sweep spans many of
both, and pinning either in the name would be a claim it cannot keep.

**Sittings are numbered and slugged** — `001-entrypoint-and-args.md`. The number
is the identity and the order they happened in; the slug is for finding one
again. Numbering from `001` rather than by date, because *what did we do first*
is the question anybody asks of a sweep and the date does not answer it.

## More than one sweep at a time

**Permitted, and usually a mistake.** Two open sweeps over the same repository
compete for the only scarce resource involved, which is the person's attention,
and neither finishes.

The case where it is right: **sweeps with different readers**, or genuinely
disjoint scopes with different purposes — somebody reading the prose while
somebody else reads the CLI. If the scopes overlap at all, they are one sweep
with two people in it.

## Archive when closed; delete later and deliberately

A closed sweep moves to `.luma/backlog/reviews/archived/<slug>/`, keeping the
`sittings/` beside it. **What the sweep produced has already left** — a merged
pull request, an idea, a decision, a finding — so what remains is working notes,
and their value decays.

Deleting them is fine eventually and is nobody's emergency. Archiving needs no
permission; deleting somebody else's sweep needs theirs.
