---
type: policy
title: What an enhancement is
description: One observed model behaviour and its guardrail, in four parts. The bar it has to clear, and why the harness is a condition inside one rather than a bundle of its own.
matches:
  - topic: writing or reviewing a model enhancement
---

# What an enhancement is

**One behaviour, one document, five parts.**

| part | what it holds |
| --- | --- |
| **Problem** | the behaviour, stated plainly and without excuse |
| **Goal** | what it should do instead, in a sentence |
| **ALWAYS** | what to do, positively — two or three bullets |
| **NEVER** | the specific things not to do, including the tempting near-misses |

**ALWAYS carries the rule; NEVER holds the edges.** A prohibition makes the
model represent the banned behaviour and then invert it, where a positive
instruction gives it a target — so a guardrail whose NEVER is longer than its
ALWAYS is inverted and will underperform. Both are still required: NEVER alone
leaves nothing to replace the failure with, and a model given a prohibition and
no substitute finds a neighbouring way to fail.

**The near-miss is the highest-leverage part and the last to cut.** An example
outweighs more instruction, and the useful example is the one that *looks* like
compliance and is not. See [[what-makes-a-guardrail-stick]].

**It is required, and leaving it out needs a reason written in the document** —
`**No near-miss.**` followed by why, never a silent omission.

**A weak near-miss is worse than none, and this is not a formality.** An example
outweighs the instruction it sits under — that is the whole reason to have one,
and the leverage runs both ways. One that is vague, invented, or not actually a
case of near-compliance teaches a wrong edge, and the model will follow it over
the rule above it.

**So: write a real one, or rework the rule until one exists, or state its
absence. Never fabricate one to satisfy the requirement.**

**Being unable to write one is a finding about the rule, not about the
example.** A behaviour with no near-compliance case is either obvious enough
that it needs no guardrail, or too vague for the model to know when it is
violating. Both say rework the rule rather than ship it bare.

**They are capitalised and the two above them are not.** `Problem` and `Goal`
describe; these two instruct, and the casing is the only thing marking which is
which at a glance.

**Every label says what it holds without the one above it.** *Instead* was a
connective — it meant nothing to anyone reading that block on its own, which is
how an agent often meets it.

## Every requirement here is a default you depart from in writing

**The bar is that an agent can actually follow it.** Every requirement above
exists because it makes that more likely — none is a formality, and none is
there for tidiness.

**So none of them is optional, and none is absolute.** Where one genuinely does
not fit, say so in the document and say why. `**No near-miss.**` with its one
line is the pattern for all of them. **A stated departure is a decision somebody
can disagree with; a silent one cannot be told apart from not having tried.**

**And a requirement you cannot meet is usually telling you about the rule, not
about the requirement.** An ALWAYS you cannot scope to be literally true, a
guardrail you cannot state a pass or fail for, a behaviour with no near-miss —
each is a signal the rule is vague or unnecessary. **Rework the guardrail before
writing the exception**, because the exception is the cheaper move and it is
almost never the right one.

## The bar

**It has to have cost somebody something.** A way a model *could* misbehave is a
guess, and guesses are what the reader deletes later. Name the case.

**It has to be the model.** Before writing one, rule out the prompt, the
harness, and a missing tool — those have their own homes and a guardrail aimed
at the wrong cause is charged to every session forever without ever firing.

**It has to be worth its recurring cost.** See [[the-per-session-budget]].

## The harness is a condition, not a bundle

**One bundle per model. Where something is harness-specific, scope it in a
line** — *"In Claude Code, …"* — inside the policy that needs it.

Models turn over a few times a year and a harness changes weekly. A bundle per
model×harness is a matrix nobody keeps current, and most behaviours are not
harness-specific anyway.
