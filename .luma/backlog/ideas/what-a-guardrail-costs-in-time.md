---
type: luma/idea
title: What a guardrail costs in time, not just in words
created: { by: human:benlinton, at: 2026-08-29T00:00:00Z }
contributors: [human:benlinton, agent:claude-opus-5]
horizon: next
scope: project
lifecycle: draft
---

# What a guardrail costs in time, not just in words

**`the-per-session-budget` counts words, and words are the smallest part of the
bill.** `prove-what-you-did` is 200 words and makes the model run extra
commands, quote their output, and write longer messages — on every turn where a
claim is made. **The induced cost dwarfs the document and nothing measures it.**

**That is the number that decides whether a guardrail is worth having**, and
right now the honest answer to *how much slower does this make it* is that
nobody knows.

## Everything that could work

Captured broadly on purpose — the right answer is probably two or three of these
together, and it is too early to pick.

### Baseline comparison

- **A fixed task suite**, run with the bundle and without it, comparing
  wall-clock, total tokens, turn count and tool-call count.
- **Counterfactual replay** — the same prompt against both configurations, then
  diff the transcripts. Cleanest signal, and only works where the task is
  deterministic enough to replay.
- **Coin-flip A/B over real sessions**, aggregated. Slower to yield an answer,
  but measures the thing people actually do rather than a proxy for it.

### Auditing what already happened

- **Transcript audit** — parse session records for actions attributable to a
  guardrail: verification commands that would not otherwise have run, messages
  carrying evidence blocks.
- **Usage records** — token counts per session from the API or harness, before
  and after adoption. Coarse, free, and already collected.
- **Instrumented read** — a hook logging when the entrypoint and each guardrail
  were actually opened. Answers a different and equally unknown question:
  whether they are being read at all.

### Asking the model

- **Self-report behind a measurement flag** — the model tags which guardrail
  caused an action. **Rejected for production** in
  `what-makes-a-guardrail-stick`, because it is per-turn padding — but as a
  temporary measurement mode it is exactly the right tool, and the objection
  does not apply.

### Classifying instead of measuring

- **Cost tiers per guardrail**, assigned when written: does it induce a command,
  a longer message, or nothing? Crude, costs nothing, and would already have
  flagged `prove-what-you-did` as the expensive one.

## Two costs that are not wall-clock

**The user's attention.** Longer messages are slower to read, and a guardrail
that makes every response 30% longer has a real cost that no timer catches.

**Turns.** A guardrail that prevents one wrong answer saves more than it spends,
and a guardrail that adds a verification step to every turn spends continuously.
**The comparison has to be net, not gross** — the whole case for these is that
they cost less than the failures they prevent, and neither side of that is
measured today.

## The honest difficulty

**The system is non-deterministic**, so either N has to be large or the effect
has to be obvious. A measurement that cannot distinguish a 10% slowdown from
noise should say so rather than reporting a number.

**Related:** [[guardrails-need-a-switch-and-a-measurement]] — the switch is a
prerequisite for most of the above, and the fixed task suite is the same
artifact both ideas need.
