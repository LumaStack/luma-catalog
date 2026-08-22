---
type: policy
title: A document is loaded, not just read
description: Documentation is context an agent pays for on every read, so what a document contains is a cost. Where reasoning that changed course belongs, and the record types that are the exception.
---

# A document is loaded, not just read

Everything else in this bundle is written for a person who opened the repository.
**Documents are also loaded into agents, in full, repeatedly, against a finite
budget.**

That changes what a sentence costs. A paragraph a human skims in a second is paid
for on every read, forever, by every agent that loads the file — and unlike a
human, an agent cannot skim. It reads what it is given and reasons about all of
it.

**So noise is not a matter of taste here. It is a measurable, recurring cost, and
it has a second effect that is worse than the first:** content describing a
position nobody holds any more invites an agent to reason about it as though
somebody did.

## Reasoning that changed course belongs in history

**Git history should show how you arrived.** The false start, the argument that
was reversed, the thing that turned out not to be true — that record is worth
keeping. It is how a team learns what its process gets wrong, and it costs a
reader nothing until they go looking for it.

**The document should show only what is true now.** Not because the history is
unimportant, but because the two have different readers arriving for different
reasons, and only one of them is paying by the token.

This is [[documentation-layout]]'s distinction applied inside a file rather than
between them: *documentation describes what is true now; a record says what
happened at a moment.* A sentence explaining what an earlier draft got wrong is a
record, and it has wandered into the wrong artifact.

| | belongs in |
| --- | --- |
| what we decided | the document |
| what we rejected, and why | the document — see below |
| what an earlier draft said | the commit message |
| that somebody was wrong, and corrected it | the commit message |
| how long it took to get there | the commit message |

**The destination already claims this job.** [[merge-commits]] in the
`luma/git-workflow` bundle rests on the commit message being where rationale
lives — it is the argument against squashing. Sending reasoning there is using a
home that exists, not creating an obligation.

## What this is not

**Not an argument for terse documents.** Length spent on what is true now is
earning its place. A long explanation of a live constraint is fine; a short
paragraph about a dead one is not. **The test is whether a reader needs it to act
correctly today**, not how many words it takes.

**Not an argument against recording rejected options.** *We considered X and did
not take it, because Y* is live content — it stops the next person re-deriving a
dead end, and it says what would change the answer. **A rejected alternative is
design. "I previously thought X" is a diary.** The difference is whether it helps
somebody decide, or only tells them what happened.

## The exception is a type, not a mood

Some records exist **precisely** to show their work. There, reasoning that
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

**When reviewing a document, an easy check:** would a reader who had never seen
the previous version notice anything missing? If a sentence only makes sense to
somebody who knows what it used to say, it belongs in history.
