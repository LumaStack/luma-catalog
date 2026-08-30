---
type: document
title: Loading by model is unsolved
description: A document can declare the model it is for and nothing fires on it, so a model's guardrails are advertised rather than delivered. The three routes to closing that, and what each costs.
---

# Loading by model is unsolved

**A model bundle cannot state its own condition, let alone have it delivered.**

`matches` takes a closed vocabulary — `command`, `event`, `path`, `tool`,
`topic`, or the bare words `always` and `nothing`. **`model` is not in it**, and
`inspect` reports anything else as a HIGH finding: *"anything else parses,
publishes, and never fires, which is indistinguishable from a rule whose moment
has not come."*

**So the entrypoint declares nothing.** It is on-demand, named in its bundle's
ring, and reached by an agent following the ring. The condition that actually
governs it — *this model is running* — is unsayable.

**`matches: always` remains available and remains wrong.** It would deliver
today by charging every session of every adopter whatever model is running,
which is a claim false for most of them.

**So the gap is a vocabulary before it is a transport.** Nothing can carry a
condition the format cannot express.

## What has been looked at

**A session-start hook.** The obvious route, and `luma-foreman`'s own
hook-delivery planning is sceptical of it for a different reason — it *"swaps
one Claude Code mechanism for another"* and is not more harness-neutral, while
costing a process at every session start. **Model conditioning is a reason that
planning did not consider**, and it may change the answer.

**Harness configuration.** Some harnesses can select context by model directly.
Where one can, that is strictly better than anything the format could do, and
the bundle should carry the config rather than reimplement the selection.

**Adding `model` to the trigger vocabulary.** This has to come first: nothing
else can be built on a condition that cannot be written down. It is a change to
a type more than one tool reads, so `lumastack/luma-catalog/luma-types` and
`change-a-shared-type` govern it, and it is not a local decision.

## What it costs to leave open

**Not tokens — reach.** Nothing is over-delivered, because nothing is delivered.
The guardrails sit in the ring and an agent finds them by looking, which is
exactly the failure they exist to prevent: a model that does not check is not
going to go looking for the policy telling it to check.

**So the bundle is worth less than it looks until this closes**, and that should
be said plainly to anyone adopting it rather than discovered.

**What would settle which route:** whether the harness can already select by
model. If it can, the third option is dead and the bundle carries config
instead. Nobody has checked, and it is one question to whoever owns the
harness.
