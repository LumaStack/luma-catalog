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

**They are capitalised and the two above them are not.** `Problem` and `Goal`
describe; these two instruct, and the casing is the only thing marking which is
which at a glance.

**Every label says what it holds without the one above it.** *Instead* was a
connective — it meant nothing to anyone reading that block on its own, which is
how an agent often meets it.

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
