---
type: policy
title: Reasoning that changed course belongs in history
description: A false start is worth keeping, and usually in the commit rather than the document. The test for when history earns its place, and the record types where showing the work is the format.
---

# Reasoning that changed course belongs in history

**Guidance, not a rule.** Documentation systems keep producing cases where showing
how a conclusion was reached is exactly what a reader needs, and a prohibition
would be wrong in all of them. **Avoid this by default; do not forbid it.**

## The test

**Not *is this history*. It is: does keeping this stop somebody re-deriving a dead
end?**

A summary of what was rejected and why passes — the next person reads it instead of
spending a day rediscovering it. A record of how the team went back and forth
before deciding does not; it costs a reader attention and returns nothing they can
act on.

That test cuts cleanly through most cases, and it is worth applying rather than
reaching for a rule.

## What belongs in history rather than the document

**The mess, in all its forms.** Scratchpad notes. Waffling and indecision. The
false starts, taken one at a time. Everything that shows the shape of the work
rather than the shape of the answer.

**It is worth keeping** — a false start is how a team learns what its process gets
wrong — and the commit message is where it costs a reader nothing until they go
looking.

| | usually belongs in |
| --- | --- |
| what we decided | the document |
| what we rejected, and why it stays rejected | the document |
| the back-and-forth that got there | the commit message |
| what an earlier draft said | the commit message |
| that somebody was wrong, and corrected it | the commit message |

**This is [[documentation-layout]]'s distinction applied inside a file rather than
between them:** *documentation describes what is true now; a record says what
happened at a moment.*

**The destination already claims the job.** [[merge-commits]] in the
`luma/git-workflow` bundle rests its case against squashing on the commit message
being where rationale lives, so sending reasoning there uses a home that exists
rather than creating an obligation.

## When history earns its place in the document

**A summary of rejected paths, where re-litigation is likely.** Not the argument as
it happened, but the compressed version: *this was considered, and here is why it
was not taken.* One paragraph that saves the next person a week.

**A live constraint that only makes sense with its history.** Some rules are
unreadable without the failure that produced them, and stripping the story leaves a
rule nobody can apply.

**Where a type exists for it** — see below.

**In each case the history is doing work now.** That is the difference from a diary
entry, which only reports.

## Why it matters more than tidiness

**A document is not only read by people. It is loaded into agents, in full,
repeatedly, against a finite budget.**

A paragraph a person skims in a second is paid for on every read, forever, by
everything that loads the file — and an agent cannot skim. It reads what it is
given and reasons about all of it.

**And the second effect is worse than the cost.** Content describing a position
nobody holds any more invites a reader to reason about it as though somebody did.
A human recognises *we used to think X* as background. An agent may treat it as a
live constraint, and there is nothing in the text marking which sentences are
still in force.

That gives *every document is a liability until somebody reads it* — from
[[which-document]] — a second and sharper reason.

## What this is not

**Not an argument for terse documents.** Length spent on what is true now earns
its place. A long explanation of a live constraint is fine; a short paragraph
about a dead one is not. **The test is whether a reader needs it to act correctly
today**, not how many words it takes.

**A rejected alternative is design. "I previously thought X" is a diary.** The
difference is whether it helps somebody decide, or only tells them what happened —
which is the test above, in fewer words.

## Some types show their work by design

**Where a record type exists whose job is showing the work, the question does not
arise** — there, reasoning that changed course is the content rather than noise:

- **decision records** — deferred alternatives, re-open triggers, and the argument
  that was not taken, kept deliberately so a decision can be revisited rather than
  re-litigated
- **audit records** — a finding written by one party and answered by another,
  where the exchange is the point

**Naming types rather than circumstances is deliberate, and it is why this is the
easy case.** *Show your work where it matters* is a judgement every author makes
generously about their own writing. *A decision record shows its work; a README
does not* is a fact about which file is open. Everywhere else the test above still
has to be applied by somebody thinking about it.

## Applying it

**The default when reasoning changes course mid-edit:** the correction goes in the
commit message and the document simply reads correctly afterwards. A note
explaining the change is usually worth deleting — if the wrong turn was
instructive, the commit is where it instructs.

**When reviewing, one check does most of the work:** would a reader who had never
seen the previous version notice anything missing? A sentence that only makes
sense to somebody who knows what it used to say is the candidate — then ask
whether it stops a dead end being re-derived, and keep it if it does.

**Where the answer is genuinely unclear, leave it out and see whether anybody
misses it.** Adding it back later costs a paragraph; the reverse costs everyone
who read it in between.
