---
type: bundle
version: 0.1.0
published: 2026-08-29
consumers: [project, organization]
entrypoint: policy/what-these-are-for
description: Behaviours Opus 5 exhibits that cost its user time, each with a guardrail. Every policy loads in every session, so every policy is short.
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

- [[what-these-are-for]] — how to read the rest. Start here.
- [[check-before-objecting]] — fluent objections nobody verified.
- [[justify-in-the-message-not-the-artifact]] — reasoning written into the
  deliverable instead of the reply.
- [[a-correction-is-a-class]] — the same fix applied only where it was pointed.
- [[never-declare-it-finished]] — completeness asserted from intention.

## When these apply

**Whenever this model is what is running**, which is what every document here
declares:

```yaml
matches:
  - model: opus-5
```

**A guardrail that arrives after the mistake is a description of the mistake**,
so these cannot be topic-matched — by the time a topic fires, the behaviour has
happened. The condition is the model, and nothing narrower is honest.

**Nothing delivers on `model:` yet.** The trigger parses, reaches the ring and
`routing.toml`, and fires nowhere — so today these are advertised rather than
loaded, and an agent reaches them by being pointed at the ring. That is a real
reduction in what this bundle does, and it is the correct trade: `matches:
always` would work today by charging every session of every adopter, including
those running a different model entirely. See
`lumastack/luma-catalog/model-enhancement-manager`, which carries the problem.

**They are written to a budget regardless.** When delivery lands they load in
every session of this model, forever. The whole bundle is intended to stay under
a thousand words, and sharpening an existing policy is preferred to adding a
sixth.

## Version

`0.1.0` — five policies from one long session with one user. The behaviours are
real; whether they are the *most* costly five is unknown, and a second user's
evidence may reorder or replace them entirely.
