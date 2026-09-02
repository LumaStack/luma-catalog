---
type: bundle
title: lumastack/luma-catalog/model-enhancement-manager
version: 0.2.0
published: 2026-09-02
lifecycle: draft
consumers: [project, organization]
description: Building and maintaining per-model guardrail bundles — the shape an enhancement takes, the evidence bar, the per-session budget, and the unsolved problem of loading them only for the model they describe.
---

# Model enhancement manager

**Models fail differently from each other, and a guardrail written for one does
not catch another.** So each model gets a bundle —
`model-opus-5-enhancements` is the first — and this is the practice for
building them, keeping them honest, and keeping them small.

**The hard part is not writing them.** It is the two things that make them worth
having: an evidence bar strict enough that the bundle stays true, and a size
budget strict enough that it stays affordable. Every enhancement loads in every
session of its model, so a bundle that accumulates is one that eventually costs
more than it saves.

**The reader is an agent, thousands of times over.** A human reads a guardrail
once or never, and reads it *through* an agent when they do — so an unfamiliar
term costs a person one question and costs the agent nothing. Where plain
wording and the term a model knows best diverge, the agent's vocabulary wins.

**Working comes first, small comes second, and they never compete.** A guardrail
is optimised for size only inside what already works — never against it. Nothing
that aids comprehension is spent for words, because a compressed rule the model
misreads has cost its words for nothing. See [[the-per-session-budget]].

## What is here

- [[what-an-enhancement-is]] — the shape and the bar. Start here.
- [[the-entrypoint-compels-the-read]] — the one document that fires, and why
  it is an instruction.
- [[the-per-session-budget]] — what adding one costs, and what to remove.
- [[write-an-enhancement]] — the procedure, from noticing to publishing.
- [[start-a-model-bundle]] — standing one up for a model that has none.
- [[what-makes-a-guardrail-stick]] — what the published work says, what it
  changed here, and what was rejected on evidence.
- [[loading-by-model-is-unsolved]] — the open problem, and what has been ruled
  out.
- [the enhancement template](templates/enhancement.md) and [the entrypoint
  template](templates/entrypoint.md) — copy the blocks, never the file.

## When these apply

**None of it is always-on.** This bundle is read by whoever is authoring or
maintaining an enhancement, which is rare and deliberate — the opposite of what
it produces. Each document says what surfaces it.

## Version

`0.1.1` — **the manifest declares `lifecycle: draft`.** The field was absent, and
absent reads as `unknown` — *nobody has said*. Something was known: this is
developed by its maintainers for their own use, and its shape can reverse
without notice.

**Publication did not promote it.** Being reachable by somebody who did not
write it makes the question live rather than answering it, and the answer here
is *still a draft* — which is a legitimate thing to publish, and says more than
silence did.

Patch: a fact written down. Nothing an adopter is obliged to do has changed, and
`unknown` promised nothing that `draft` withdraws.

`0.1.0` — the practice is one bundle old. The evidence bar and the budget are
both guesses calibrated against a single model and a single user's sessions.
