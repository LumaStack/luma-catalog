---
type: policy
title: What an enhancement is
description: One observed model behaviour and its guardrail, in four parts. The bar it has to clear, and why the harness is a condition inside one rather than a bundle of its own.
matches:
  - topic: writing or reviewing a model enhancement
---

# What an enhancement is

**Write for the agent, not the person reviewing it.** An agent reads a
guardrail thousands of times; a human reads it once, or never. Where the two
conflict, the agent wins — take the term a model has seen ten thousand times in
training over the plainer word a person would prefer on first reading.
*Contrastive example* over *near-miss* is that trade, made deliberately.

**And the usual objection does not hold: a person reads this through an
agent.** Unfamiliar vocabulary is not a cost when the reader can ask what a term
means and get an answer in a sentence. Plain wording buys a first-time human
reader something they can obtain on demand anyway, and charges the agent for it
on every session forever. **So optimise wholly for the agent, and let
explanation be the thing that is asked for.**

**The explaining agent has to be the model the guardrail is for.** A different
model tells you how *it* reads the text, and the text was tuned to one — so a
correct explanation from the wrong model is a false pass, and it is silent.
Nothing downstream reports that the model actually governed by the rule reads it
differently.

**What still has to hold is auditability, which is not the same as plainness.**
A person must be able to tell whether a guardrail is *right* — with an agent
beside them, reading it together. Two of these carried the contrastive label
without contrasting, and that was caught exactly that way: the rule was
explained, then the examples were read side by side. **No check found it.**
Precision serves that review; simplification does not.

**One behaviour, one document, five parts.**

| part | what it holds |
| --- | --- |
| **Problem** | the behaviour, stated plainly and without excuse |
| **Goal** | what it should do instead, in a sentence |
| **ALWAYS** | what to do, positively — two or three bullets |
| **NEVER** | the edges — the specific things not to do |
| **Contrastive example** | it going wrong, quoted, beside it going right — both quoted |

**ALWAYS carries the rule; NEVER holds the edges.** A prohibition makes the
model represent the banned behaviour and then invert it, where a positive
instruction gives it a target — so a guardrail whose NEVER is longer than its
ALWAYS is inverted and will underperform. Both are still required: NEVER alone
leaves nothing to replace the failure with, and a model given a prohibition and
no substitute finds a neighbouring way to fail.

**A contrastive example is it going wrong where it was close to going right.**
An obvious failure teaches nothing — the model was never going to write that.
The useful one is the version it would produce while believing it complied,
quoted, beside the version that passes. **Both sides quoted**: describing the
right one in prose makes it a negative example, which is weaker.

**It is the highest-leverage part when it is real.** An example
outweighs the instruction it sits under, and the useful example is the one that
*looks* like compliance and is not. See [[what-makes-a-guardrail-stick]].

**Attempt one every time. Include it only when it is real.** The attempt is
where the value is — trying to name a case on the border is what exposes a
rule that is vague, or one so obvious it needs no guardrail at all. That
diagnosis is the point; the example is a by-product.

**Requiring one to exist produces the opposite.** A fabricated contrastive example teaches
a wrong edge, and it is followed over the rule above it, because an example
outweighs its instruction whether or not it is any good. **The pressure to
produce one turns good rules into bad ones**, which is a worse outcome than the
missing example it was meant to prevent.

**Leave it out when it does not fit, or would not make the policy better.**
That is a judgement, not an escape hatch — and a guardrail without one is not a
defect and owes no explanation. Some behaviours have no case on the border.

**Not having looked is the defect**, and it is not one anything can check for.

## Every requirement here is a default you depart from in writing

**The bar is that an agent can actually follow it.** Every requirement above
exists because it makes that more likely — none is a formality, and none is
there for tidiness.

**So none of them is optional, and none is absolute.** Where one genuinely does
not fit, say so in the document and say why, in a line. **A stated departure is
a decision somebody can disagree with; a silent one cannot be told apart from
not having tried.**

**The contrastive example is the exception to this section**, and the reason is worth
keeping: requiring an example to exist produces fabricated ones, so it is
attempted every time and included only where it helps. Where a requirement can
be satisfied badly, mandating it buys the bad version.

**And a requirement you cannot meet is usually telling you about the rule, not
about the requirement.** An ALWAYS you cannot scope to be literally true, a
guardrail you cannot state a pass or fail for, a behaviour whose border you
cannot name — each is a signal the rule is vague or unnecessary. **Rework the guardrail before
writing the exception**, because the exception is the cheaper move and it is
almost never the right one.

## The bar

**It has to have cost somebody something.** A way a model *could* misbehave is a
guess, and guesses are what the reader deletes later. Name the case.

**It has to be the model.** Before writing one, rule out the prompt, the
harness, and a missing tool — those have their own homes and a guardrail aimed
at the wrong cause is charged to every session forever without ever firing.

**And it has to fix a defect rather than add a capability.** The test is not
whether another model shares it — earlier versions of this same model often have
the same fault, and it is still a correction. The test is: **would this help a
model that does not have the problem?** If yes, it is a practice, and it belongs
in a model-neutral bundle.

**Where several models do share a correction**, that is a question about where
it lives rather than whether it belongs — see [[start-a-model-bundle]].

**Getting that wrong fails twice.** A practice filed here is charged to every
session of one model, and withheld from every other model that needed it just
as much. **A correction earns its seat because this model in particular gets it
wrong; a practice never does.**

**It has to be worth its recurring cost.** See [[the-per-session-budget]].

## The harness is a condition, not a bundle

**One bundle per model. Where something is harness-specific, scope it in a
line** — *"In Claude Code, …"* — inside the policy that needs it.

Models turn over a few times a year and a harness changes weekly. A bundle per
model×harness is a matrix nobody keeps current, and most behaviours are not
harness-specific anyway.
