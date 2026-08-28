---
type: policy
title: What a slice produces
description: Where each reaction goes — fixed now, recorded, captured, or nothing — and the rule that nothing worth keeping stays inside the sweep.
matches:
  - topic: acting on what a code review turned up
---

# What a slice produces

**Everything worth keeping leaves the sweep.** A sweep is backlog: it gets
archived and eventually deleted, and anything parked in a slice note as *we
should really…* dies with it.

So the last few minutes of a slice are routing, and they are not optional. A
slice that ends with six observations in a note has produced nothing.

## Where each reaction goes

| the reaction | where it goes | owned by |
| --- | --- | --- |
| **this is wrong and I understand it** | fix it now, in this slice's branch | the pull request |
| **this is wrong and I do not understand it yet** | an idea, or a finding | `backlog-ideas`, or `audit-records` |
| **this is fine, but I had to work out why** | a decision record | `decision-records` |
| **this is fine** | mark it reviewed and move on | the sweep index |

*Those bundles are named rather than linked — they are separate bundles and may
not be adopted here. If one is absent, the destination is whatever this project
already uses for that kind of thing, and the routing rule is unchanged.*

## The fourth row is the most common and the easiest to skip

**Reviewed and clean is a result.** It is what lets somebody later tell
*examined and fine* from *never looked at*, and a sweep that only records
problems cannot make that distinction — its index becomes a list of complaints
with unexplained gaps between them.

Mark it off. It costs a cell.

## Fix what you understood in the slice; capture the rest

**The fix that belongs in this slice is the one you both just reasoned
through.** You have the context, it will not be cheaper later, and the review
is what justified it.

**Everything larger is an idea.** *This whole layer wants restructuring* is a
real observation and it is not slice work: taking it on stalls the sweep on
file four for a week, and the sweep is the thing with momentum worth
protecting.

**Watch for `while I'm here`.** It is how a two-file slice becomes a
nineteen-file diff nobody can review, including you. The test is whether the
change is one you understood *in this slice* — not whether it is small, and not
whether it is obviously correct.

## Landing the fixes

**A slice is not a pull request boundary.** Most slices produce no change at
all — *reviewed and clean* is the common result — so one pull request per slice
means a stream of empty and one-line pull requests, and the ones that matter
get lost among them.

**The two sizes are governed by different things.** A slice is sized by what
you can comprehend together; a pull request by what reviews well. Forcing them
to be the same object guarantees one of them is wrong.

**Batch by kind, across slices.** *Here are the six places that swallow the
exception* is one idea, reviewable as one idea — better than six pull requests
of one line each, where nobody ever sees the pattern. It is also how the sweep
actually learns: slice 009 routinely reveals that 003 and 005 had the same
problem, and under a per-slice rule those landed separately and the pattern was
never visible.

**The one constraint is staleness, not size.** Do not carry a large pile of
unlanded fixes into the next slice — reading with a big uncommitted diff
underneath you means reviewing your own work in progress, and the sweep starts
chasing itself. Land when the pile is deep enough to distort what you are
reading, which is a judgement rather than a count.

*How changes get integrated is not this bundle's to say — `git-workflow`, and
whatever this project already does, own that. The staleness sentence is the
only part that belongs here, because it is about the reading rather than the
merging.*

## The agent does not fix what the reader has not agreed to

**Applying a change the reader has not seen turns their review into a diff
review of yours**, and it happens easily — the fix is obvious, it is right
there, and asking feels like friction.

Propose, get a yes, then apply. **A yes to one fix is not a yes to the
pattern** elsewhere in the file; if the same thing appears four more times,
that is one proposal covering five sites, not four unremarked edits.

## Nothing is deferred to the end of the sweep

**Route it during the slice.** A pile of *to be filed later* items is filed by
nobody: the reasoning that made each one worth capturing is gone within a day,
and what gets written a fortnight later is a shorter, worse version of it.

The one thing that legitimately waits is a **conclusion the sweep has not
reached yet** — a suspicion about the shape of the whole system that needs
three more slices before it can be stated. Write it in the slice as a
suspicion, say what would confirm it, and let a later slice settle it.
