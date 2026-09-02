---
type: procedure
title: Start a model enhancement bundle
description: Stand up an enhancements bundle for a model that has none. Use when adopting a new model, or when an existing bundle's guardrails stop matching what you see.
---

# Start a model enhancement bundle

**Every model should need fewer of these than the last, and the target is
none.** A bundle is a list of things a model gets wrong, so a shorter list is a
better model. Enhance only what you must.

**A bundle that grows from one generation to the next is evidence**, and of one
of two things: the model regressed, or the bundle is accumulating guesses. Say
which in `BUNDLE.md`. Neither is a reason to keep writing.

## 1. Name it

**`model-<name+version>-enhancements`** — `model-opus-5-enhancements`.

**The last segment matters.** It leaves room for other bundles about the same
model later: a bare `model-opus-5` would squat the whole name for one purpose
and read, wrongly, as everything known about it.

**Version granularity is per major model**, not per family and not per point
release. Opus 5 and Sonnet 5 fail differently; 5.0 and 5.1 mostly do not.

## 2. Start empty

**Do not copy another model's bundle.** It is the fastest way to a bundle full
of guardrails for behaviours this model does not exhibit — which cost the same
as real ones and are never triggered, so nothing reveals them as wrong.

Scaffold with the `create-bundle` procedure in
`lumastack/luma-catalog/bundle-manager`, then declare the word ceiling in
`BUNDLE.md` before the first policy goes in.

**Write the entrypoint first, from [the entrypoint
template](../templates/entrypoint.md).** It is the only document
that will declare `matches`, and starting from it is what stops the guardrails
each claiming a trigger of their own.

## 3. Take from an existing bundle only what you have seen here

**A policy earns its place in each bundle separately.** Watching the new model
do the same thing is the only reason to carry a guardrail across — and when it
does, cite both cases.

**When three models share one**, that is evidence of a common base bundle rather
than three copies. Do not build one at two.

## 4. Say what is unverified

A new bundle is a set of predictions until the model has been watched under
real work. **`version: 0.1.0`, and `BUNDLE.md` says how many sessions and how
many users it is drawn from** — one long session with one user is a fact a later
reader needs.
