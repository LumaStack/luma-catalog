---
type: policy
title: The per-session budget
description: Working comes first and small comes second, and they never compete. What the budget may cut, what it may never cut, and what has to come out before something goes in.
matches:
  - topic: adding to or trimming a model enhancement bundle
---

# The per-session budget

**Two goals, ranked, and they do not compete.** A guardrail has to work. Then it
has to be small. Size is optimised inside what already works, never against it —
so there is no trade-off to weigh and no judgement to make at the boundary.

**Nothing that aids comprehension is spent for words.** A heading naming a
block, a label that stands alone, a contrastive example: that is what the rule
costs, not padding laid over it. A compressed rule the model misreads
has spent its words for nothing, which is the worst outcome available and the
one that looks thriftiest.

**The budget cuts everything else** — explanation, hedging, repetition, and any
rule that has stopped earning its place.

## Why the cost is unavoidable

**An enhancement cannot be topic-matched.** A guardrail delivered after the
mistake is a description of the mistake, so it has to be present before the work
starts — which means every session of its model pays for it, including every
session where the behaviour never appears.

**Do not reach for `matches: always` to get that.** It buys presence today by
charging every adopter on every model, which is a larger bill for a smaller
claim. Declare `model:` on the entrypoint and accept that delivery is pending —
see [[the-entrypoint-compels-the-read]] and [[loading-by-model-is-unsolved]].

**Count the whole bundle, not the document that fires.** The entrypoint defers
the guardrails rather than removing them, and an agent that obeys it reads all
of them. A budget measured on the entrypoint alone would report a number nobody
pays.

**So the cost is unavoidable and the size is not.**

## The rules

**A budget, declared in the bundle.** State a word ceiling in `BUNDLE.md` and
keep to it. Without a number, a bundle grows one reasonable-looking addition at
a time.

**Sharpen before adding.** Most new observations are a sharper case of a policy
already there. Adding a document when an existing one could absorb it buys a
distinction the model will not act on differently, and charges every session
for it.

**Remove what stops earning.** A guardrail for a behaviour that has not recurred
is being paid for by every session. Removal is ordinary, not a failure — and
[[write-an-enhancement]] closes by asking what came out.

**Measure it, do not estimate it.** `wc -w` on the bundle. An estimate of a
context cost is the thing this whole area exists to stop.

## What not to spend it on

- **Explaining the practice to the model.** It needs the rule, not the
  reasoning behind the rule. The reasoning lives here, and here is not loaded.
- **Restating a rule the harness already enforces.**
- **Hedging.** *Consider whether you might* is a sentence that changes nothing
  and is charged in full.
