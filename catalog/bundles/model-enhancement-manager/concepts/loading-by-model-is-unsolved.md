---
type: document
title: Loading by model is unsolved
description: A document can declare the model it is for and nothing fires on it, so a model's guardrails are advertised rather than delivered. The three routes to closing that, and what each costs.
---

# Loading by model is unsolved

**Declaring the condition works. Delivering on it does not.**

`matches: model: opus-5` parses, survives into a bundle's ring and into
`routing.toml`, and reads correctly to anybody who opens either. **Nothing acts
on it.** A document conditioned on a model is advertised and never fired, so it
is reached by an agent following the ring rather than by arriving on its own.

**That is the honest state and it is better than the alternative.** `matches:
always` would deliver today by charging every session of every adopter whatever
model is running — presence bought with a claim that is false for most adopters.
A trigger that states the truth and waits is recoverable; a permanent seat in
everybody's context is not.

**So the gap is a transport, not a vocabulary.** Whatever closes it has to learn
which model is running and fire the documents conditioned on it.

## What has been looked at

**A session-start hook.** The obvious route, and `luma-foreman`'s own
hook-delivery planning is sceptical of it for a different reason — it *"swaps
one Claude Code mechanism for another"* and is not more harness-neutral, while
costing a process at every session start. **Model conditioning is a reason that
planning did not consider**, and it may change the answer.

**Harness configuration.** Some harnesses can select context by model directly.
Where one can, that is strictly better than anything the format could do, and
the bundle should carry the config rather than reimplement the selection.

**Making `model:` a first-class trigger.** It already parses as a trigger and
carries through to `routing.toml`, so this is not a vocabulary change — it is
teaching one consumer to read a value it already receives. That is a smaller
change than it first appears, and it is the one worth costing first.

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
