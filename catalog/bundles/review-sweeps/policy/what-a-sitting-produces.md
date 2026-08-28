---
type: policy
title: What a sitting produces
description: Where each reaction goes — fixed now, recorded, captured, or nothing — and the rule that nothing worth keeping stays inside the sweep.
matches:
  - topic: acting on what a code review turned up
---

# What a sitting produces

**Everything worth keeping leaves the sweep.** A sweep is backlog: it gets
archived and eventually deleted, and anything parked in a sitting note as *we
should really…* dies with it.

So the last few minutes of a sitting are routing, and they are not optional. A
sitting that ends with six observations in a note has produced nothing.

## Where each reaction goes

| the reaction | where it goes | owned by |
| --- | --- | --- |
| **this is wrong and I understand it** | fix it now, in this sitting's branch | the pull request |
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

## Fix what you understood in the sitting; capture the rest

**The fix that belongs in this sitting is the one you both just reasoned
through.** You have the context, it will not be cheaper later, and the review is
what justified it.

**Everything larger is an idea.** *This whole layer wants restructuring* is a
real observation and it is not sitting work: taking it on stalls the sweep on
file four for a week, and the sweep is the thing with momentum worth protecting.

**Watch for `while I'm here`.** It is how a two-file sitting becomes a
nineteen-file diff nobody can review, including you. The test is whether the
change is one you understood *in this sitting* — not whether it is small, and
not whether it is obviously correct.

## One pull request per sitting

**Not per file** — a stream of one-line pull requests is noise, and reviewing
them costs more than the changes are worth.

**Not per sweep** — a branch open for three weeks accumulating every fix is
unreviewable by the time it lands, conflicts constantly, and holds every
improvement hostage to the slowest one.

**Per sitting is the natural unit** because it is already a coherent chunk of
reasoning: the pull request body is the sitting note, and it explains itself.

**Land it before the next sitting starts.** An unmerged sitting means the next
one reviews code that is about to change, which is how a sweep starts reviewing
its own uncommitted work.

## The agent does not fix what the person has not agreed to

**Applying a change the person has not seen turns their review into a diff
review of yours**, and it happens easily — the fix is obvious, it is right
there, and asking feels like friction.

Propose, get a yes, then apply. **A yes to one fix is not a yes to the pattern**
elsewhere in the file; if the same thing appears four more times, that is one
proposal covering five sites, not four unremarked edits.

## Nothing is deferred to the end of the sweep

**Route it during the sitting.** A pile of *to be filed later* items is filed by
nobody: the reasoning that made each one worth capturing is gone within a day,
and what gets written a fortnight later is a shorter, worse version of it.

The one thing that legitimately waits is a **conclusion the sweep has not
reached yet** — a suspicion about the shape of the whole system that needs three
more sittings before it can be stated. Write it in the sitting as a suspicion,
say what would confirm it, and let a later sitting settle it.
