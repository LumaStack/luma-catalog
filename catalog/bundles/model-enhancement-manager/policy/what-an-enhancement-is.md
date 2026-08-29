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

**The near-miss is the highest-leverage part when it is real.** An example
outweighs the instruction it sits under, and the useful example is the one that
*looks* like compliance and is not. See [[what-makes-a-guardrail-stick]].

**Attempt one every time. Include it only when it is real.** The attempt is
where the value is — trying to name a near-compliance case is what exposes a
rule that is vague, or one so obvious it needs no guardrail at all. That
diagnosis is the point; the example is a by-product.

**Requiring one to exist produces the opposite.** A fabricated near-miss teaches
a wrong edge, and it is followed over the rule above it, because an example
outweighs its instruction whether or not it is any good. **The pressure to
produce one turns good rules into bad ones**, which is a worse outcome than the
missing example it was meant to prevent.

**Leave it out when it does not fit, or would not make the policy better.**
That is a judgement, not an escape hatch — and a guardrail without one is not a
defect and owes no explanation. Some behaviours have no near-compliance case.

**Not having looked is the defect**, and it is not one anything can check for.

## Every requirement here is a default you depart from in writing

**The bar is that an agent can actually follow it.** Every requirement above
exists because it makes that more likely — none is a formality, and none is
there for tidiness.

**So none of them is optional, and none is absolute.** Where one genuinely does
not fit, say so in the document and say why, in a line. **A stated departure is
a decision somebody can disagree with; a silent one cannot be told apart from
not having tried.**

**The near-miss is the exception to this section**, and the reason is worth
keeping: requiring an example to exist produces fabricated ones, so it is
attempted every time and included only where it helps. Where a requirement can
be satisfied badly, mandating it buys the bad version.

**And a requirement you cannot meet is usually telling you about the rule, not
about the requirement.** An ALWAYS you cannot scope to be literally true, a
guardrail you cannot state a pass or fail for, a behaviour whose near-miss you
cannot name — each is a signal the rule is vague or unnecessary. **Rework the guardrail before
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
