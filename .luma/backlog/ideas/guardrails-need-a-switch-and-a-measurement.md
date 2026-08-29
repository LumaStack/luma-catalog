---
type: luma/idea
title: Guardrails need a switch, and a way to tell whether they work
created: { by: human:benlinton, at: 2026-08-29T00:00:00Z }
contributors: [human:benlinton, agent:claude-opus-5]
horizon: next
scope: project
lifecycle: draft
---

# Guardrails need a switch, and a way to tell whether they work

**Every guardrail in `model-opus-5-enhancements` is adopted on faith.** Each one
names a behaviour somebody watched cost real time, which is the evidence that it
was *worth writing*. **Nothing is evidence that it works.**

**And the stated goal is zero.** `start-a-model-enhancement-bundle` says every
model should need fewer guardrails than the last and the target is none — but
removing one needs evidence just as much as adding one did, and there is none to
have.

## Two things, and the first is a prerequisite for the second

**A switch.** Turn one guardrail off without deleting it, per project or per
session, so the same bundle can run both ways.

**A comparison.** Run with and without, and tell whether the behaviour changed.

## Where the switch could live

- **`.luma/config/`** — an override list naming documents to suppress.
  `luma-config` already owns precedence, so this is the least new machinery.
- **Adoption-time selection** — choose which documents come across at `get`.
  Wrong shape: it makes the vendored copy differ from upstream, which is drift
  by definition.
- **A field on the document** — `enabled: false`. Cheap, but it edits a vendored
  bundle, so it has the same problem.
- **Harness configuration** — where the harness can already scope context. Best
  where available and unavailable everywhere else.

**The config override looks right** and it is the only option that does not
require editing a copy.

## The hard part is attribution, not the switch

**How do you know a session went better *because* of a guardrail?** Sessions are
not comparable, the same task run twice is not the same task, and the effect
sizes are likely small against a noisy baseline.

**The natural signal is the correction itself.** A guardrail works when the
behaviour it targets stops showing up — which means counting how often the user
still has to correct it. That is observable in transcripts without instrumenting
anything, and it degrades gracefully: no correction is weak evidence, a
correction is strong evidence.

**Other candidate signals**, none obviously better:

- turns to completion, on comparable tasks
- explicit user judgement, asked once at the end of a session
- how often the model cites the guardrail unprompted
- whether the near-miss appears, which is the shape of near-compliance

## And guardrails should decay

**A model point release may remove the need for one**, and nothing will announce
that. The default should be that a guardrail has to **re-earn its place** after a
model update rather than persisting until somebody questions it.

**Re-testing is the same mechanism as the A/B**, so this is one capability
rather than two. Whichever measurement gets built should be runnable on demand
against an existing bundle, not just when a policy is written.

## What would make this real

**A small fixed task set** whose failures are the behaviours the guardrails
target. Then the comparison is a rerun rather than an argument, and *"this one
no longer earns its place"* becomes a result instead of an opinion.
