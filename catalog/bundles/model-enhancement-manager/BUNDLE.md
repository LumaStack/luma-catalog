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
session, so a bundle that accumulates is one that eventually costs more than it
saves.

## What is here

- [[what-an-enhancement-is]] — the shape and the bar. Start here.
- [[the-per-session-budget]] — what adding one costs, and what to remove.
- [[write-an-enhancement]] — the workflow, from noticing to publishing.
- [[start-a-model-bundle]] — standing one up for a model that has none.
- [[loading-by-model-is-unsolved]] — the open problem, and what has been ruled
  out.

## When these apply

**None of it is always-on.** This bundle is read by whoever is authoring or
maintaining an enhancement, which is rare and deliberate — the opposite of what
it produces. Each document says what surfaces it.

## Version

`0.1.0` — the practice is one bundle old. The evidence bar and the budget are
both guesses calibrated against a single model and a single user's sessions.
