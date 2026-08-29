---
type: bundle
version: 0.1.0
published: 2026-08-29
consumers: [project, organization]
entrypoint: policy/what-an-enhancement-is
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
- [[write-an-enhancement]] — the workflow, from noticing to publishing.
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

`0.1.0` — the practice is one bundle old. The evidence bar and the budget are
both guesses calibrated against a single model and a single user's sessions.
