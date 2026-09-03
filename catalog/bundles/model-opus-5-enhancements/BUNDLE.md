---
type: bundle
title: lumastack/luma-catalog/model-opus-5-enhancements
version: 0.3.1
published: 2026-09-02
stage: draft
consumers: [project, organization]
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
- [[get-confirmation-before-finished]] — completeness asserted from intention.
- [[prove-what-you-did]] — past actions reported from memory of intending them.

## When these apply

**Whenever this model is what is running — which nothing can currently express.**
`matches` takes a closed vocabulary and `model` is not in it, so no document
here declares a trigger at all. The condition that actually governs this bundle
is unsayable, and `matches: always` is the wrong substitute: it would charge
every session of every adopter whatever model is running.

**So [[entrypoint]] is reached through this bundle's ring**, and the guardrails
are reached through the entrypoint, whose first line makes reading them
mandatory rather than optional. Existence is cheap and content is expensive.

**A guardrail cannot be topic-matched.** One delivered after the mistake is a
description of the mistake, so the condition is the model and nothing narrower —
which is why the missing vocabulary matters rather than being tidied around.
`lumastack/luma-catalog/model-enhancement-manager` carries the problem and what
closing it would take.

**Ceiling: 1,300 words**, measured with `wc -w catalog/bundles/model-opus-5-enhancements/policy/*.md`.
Sharpening an existing guardrail is preferred to adding another, and one that
stops earning its place is removed rather than kept for completeness.

**Raised from 1,100 when the contrastive example became required.** An example outweighs
more instruction, so it is the last thing to cut — and a ceiling that forced it
out would have been optimising the number at the expense of the thing the
number exists to protect.

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

`0.1.0` — three guardrails and an entrypoint, from one long session with one
user. The behaviours are real; whether they are the *most* costly three is
unknown, and a second user's evidence may reorder or replace them entirely.

**Two were dropped before publication.** *A correction is a class* asked the
model to sweep the artifact after any correction and report what else it found —
the only policy here that added a step to every exchange rather than redirecting
one, and inferring a rule from a single correction is how a model ends up
editing files nobody mentioned. *What these are for* explained the other
documents, which is what the entrypoint replaced with an instruction.
