---
type: document
title: What makes a guardrail stick
description: What the published work says about instructions models actually follow — positive framing, examples over prose, objective tests — what this bundle changed because of it, and what it deliberately did not.
---

# What makes a guardrail stick

**Read before changing the shape of an enhancement.** The four-part form is not
taste; most of it is supported, one part of it is the strongest lever available,
and two tempting additions were rejected on evidence.

**Evidence here is mixed and labelled.** Peer-reviewed and arXiv work is marked
*paper*; practitioner testing is marked *practice*. Practice is not worthless —
several of these are direct A/B results — but it is not the same thing, and a
bundle that flattens the difference is doing what it tells the model not to.

## Positive framing carries more than prohibition

**A negative instruction makes the model represent the banned behaviour and then
invert it; a positive one gives it a target.** *"Always lowercase"* outperforms
*"don't uppercase"* in direct comparison. *(practice)*

**Prohibitions are not useless** — they hold firm boundaries where the positive
form would be vague, and negative framing outperforms positive in some reasoning
settings. *(paper, practice)*

**So ALWAYS carries the rule and NEVER holds the edges.** A guardrail whose
NEVER is longer than its ALWAYS is inverted and will underperform.

## An example beats more instruction

**This is the strongest single finding, and it changed this bundle.** Examples
outweigh instructions, and a **negative example** — the wrong version, the one
that looks like compliance and is not — is what gives a rule a border the model
can locate. Pairing it with the right version is a **contrastive example**, and
the sources recommend the pair over the negative alone. *(practice, consistent
across sources)*

**Best practice guardrails include a contrastive example**, showing the wrong
version beside the right one. It is the last thing to cut, not the first.

**The leverage runs both ways, which is why a weak one is worse than none.** If
an example outweighs the instruction it sits under, a bad example outweighs it
too — and teaches an edge that is wrong.

**Where one cannot be written, that is evidence about the rule.** The research
says examples are high-leverage; it does not say every rule has a good one. A
guardrail with no case on the border is obvious or vague, and both are reasons
to rework it — so the omission is stated and justified rather than silent.

## A guardrail has to admit a pass/fail

**An instruction that cannot be objectively checked is not a guardrail**, it is
a preference. *"Respond only in English"* is checkable; *"be thorough"* is not.
*(practice)*

**This is what ALWAYS-tested-literally is for.** A bullet that cannot be failed
cannot be followed either.

## Rejected, with reasons

**Wrapping constraints in XML tags.** Reported to improve adherence in current
models. *(practice)* Not taken: the knowledge format is markdown and read by
humans and several tools, and one bundle inventing a delimiter convention is a
change to the format, not to a bundle. **Worth revisiting as a format proposal
rather than locally.**

**Making the model restate the constraints.** Reported to reinforce them
measurably. *(practice)* Not taken: it produces exactly the per-turn padding
that got a policy dropped from `model-opus-5-enhancements`. **The gain is real
and so is the cost, and nobody has measured them against each other here.**

## Two things nobody has settled

**Order within the entrypoint.** Position affects compliance, and constraint
order changes it measurably. *(paper)* No source gives a rule for which order,
so the entrypoint lists guardrails in no principled sequence. Worth an
experiment, not a guess.

**Robustness.** Prompt-based control degrades across contextual shifts — a rule
that holds in one setting fails in a neighbouring one. *(paper)* **So none of
this makes a guardrail reliable, only more likely to fire.** A behaviour that
must not happen needs a hook or a check, not a policy.

## Sources

- [The Pink Elephant Problem: Why "Don't Do That" Fails with LLMs](https://eval.16x.engineer/blog/the-pink-elephant-negative-instructions-llms-effectiveness-analysis)
- [Why Positive Prompts Outperform Negative Ones with LLMs](https://gadlet.com/posts/negative-prompting/)
- [Beyond the Basics: Advanced Prompt Engineering Techniques](https://dev.to/joao_victorsouza_ef8ff8a/beyond-the-basics-advanced-prompt-engineering-techniques-3oh)
- [A Closer Look at System Prompt Robustness](https://arxiv.org/pdf/2502.12197)
- [The Instruction Hierarchy: Training LLMs to Prioritize Privileged Instructions](https://arxiv.org/html/2404.13208v1)
- [Revisiting the Reliability of Language Models in Instruction-Following](https://arxiv.org/html/2512.14754v1)
- [Building simple & effective prompt-based Guardrails](https://www.qed42.com/insights/building-simple-effective-prompt-based-guardrails)
