---
type: policy
title: Reasoning that changed course belongs in history
description: A false start is worth keeping and belongs in the commit, not in the document. Why the document carries only what is true now, and the record types that are the exception.
---

# Reasoning that changed course belongs in history

**Git history should show how you arrived. The document should show only what is
true now.**

The false start, the argument that was reversed, the assumption that turned out
untrue — that record is worth keeping. It is how a team learns what its process
gets wrong. It belongs in the commit message, where it costs a reader nothing
until they go looking for it.

**What it must not do is stay in the document**, explaining itself to everyone who
reads the file afterwards.

| | belongs in |
| --- | --- |
| what we decided | the document |
| what we rejected, and why | the document — see below |
| what an earlier draft said | the commit message |
| that somebody was wrong, and corrected it | the commit message |
| how long it took to get there | the commit message |

**This is [[documentation-layout]]'s distinction applied inside a file rather than
between them:** *documentation describes what is true now; a record says what
happened at a moment.* A sentence explaining what an earlier draft got wrong is a
record that has wandered into the wrong artifact.

**The destination already claims the job.** [[merge-commits]] in the
`luma/git-workflow` bundle rests its case against squashing on the commit message
being where rationale lives. Sending reasoning there uses a home that exists
rather than creating an obligation.

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

**Not an argument against recording rejected options.** *We considered X and did
not take it, because Y* is live content — it stops the next person re-deriving a
dead end, and it says what would change the answer.

**A rejected alternative is design. "I previously thought X" is a diary.** The
difference is whether it helps somebody decide, or only tells them what happened.

## The exception is a type, not a mood

Some records exist **precisely** to show their work, and there reasoning that
changed course is the content rather than noise:

- **decision records** — deferred alternatives, re-open triggers, and the argument
  that was not taken, kept deliberately so a decision can be revisited rather than
  re-litigated
- **audit records** — a finding written by one party and answered by another,
  where the exchange is the point

**Naming these as types rather than as circumstances is deliberate.** *Show your
work where it matters* is a judgement every author makes generously about their
own writing. *A decision record shows its work; a README does not* is a fact about
which file you have open, and nobody has to decide whether their case is special.

## Applying it

**When reasoning changes course mid-edit, the correction goes in the commit
message and the document simply reads correctly afterwards.** Do not leave a note
explaining the change. If the wrong turn was instructive, the commit is where it
instructs.

**When reviewing a document, one check does most of the work:** would a reader who
had never seen the previous version notice anything missing? If a sentence only
makes sense to somebody who knows what it used to say, it belongs in history.
