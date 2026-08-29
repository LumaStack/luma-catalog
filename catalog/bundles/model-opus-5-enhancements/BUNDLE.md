---
type: bundle
version: 0.1.0
published: 2026-08-29
consumers: [project, organization]
entrypoint: policy/entrypoint
description: Behaviours Opus 5 exhibits that cost its user time, each with a guardrail. One entrypoint fires on the model and compels the rest to be read.
---

# Model: Opus 5 enhancements

**Opus 5 fails differently from Opus 4.x**, and a guardrail written for the
older model does not catch the newer one. This bundle holds what this model in
particular gets wrong, and what to do instead.

**Everything here is observed.** Each policy came from a session where the
behaviour cost somebody time, and the policy names the case. A way a model
*could* go wrong does not belong here — see
`lumastack/luma-catalog/model-enhancement-manager` for the bar and how to add
one.

## What is here

- [[entrypoint]] — **the only document that fires.** It names the guardrails and
  requires them to be read. Everything else is reached through it.
- [[check-before-objecting]] — fluent objections nobody verified.
- [[justify-in-the-message-not-the-artifact]] — reasoning written into the
  deliverable instead of the reply.
- [[never-declare-it-finished]] — completeness asserted from intention.

## When these apply

**Whenever this model is what is running.** [[entrypoint]] declares it and
nothing else here declares anything:

```yaml
matches:
  - model: opus-5
```

**The guardrails are reached through the entrypoint, not by matching.** They are
on-demand, so nothing is charged for them until the entrypoint sends a reader to
them — and the entrypoint's first line makes that mandatory rather than
optional. Existence is cheap and content is expensive.

**A guardrail cannot be topic-matched.** One delivered after the mistake is a
description of the mistake, so the condition is the model and nothing narrower.

**Nothing delivers on `model:` yet.** The trigger parses, reaches the ring and
`routing.toml`, and fires nowhere — so today the entrypoint is advertised rather
than fired, and an agent arrives via the ring. `matches: always` would work now
by charging every session of every adopter whatever model is running, which is a
larger bill for a claim false in most of those sessions. A hook is the intended
route; see `lumastack/luma-catalog/model-enhancement-manager`.

## Version

`0.1.0` — three guardrails and an entrypoint, from one long session with one
user. The behaviours are real; whether they are the *most* costly three is
unknown, and a second user's evidence may reorder or replace them entirely.

**Two were dropped before publication.** *A correction is a class* asked the
model to sweep the artifact after any correction and report what else it found —
the only policy here that added a step to every exchange rather than redirecting
one, and inferring a rule from a single correction is how a model ends up
editing files nobody mentioned. *What these are for* explained the other
documents, which is what the entrypoint replaced with an instruction.
