---
type: policy
title: Choosing an order
description: The orders a sweep can run in, what each buys and costs, and why the choice is made once per sweep and written down rather than defaulted to.
matches:
  - topic: deciding what to review first
---

# Choosing an order

**Decided once, at the start, and recorded in `sweep.md` with the reason.**

Not because one order is right — none is — but because an unrecorded order is
not an order. It becomes *whatever seemed next*, which drifts toward the files
that are pleasant to read and leaves the sweep's coverage looking complete while
its attention was not.

## The orders

| order | buys | costs | good for |
| --- | --- | --- | --- |
| **narrative** — entrypoints, then down the call graph | a model that compounds; each file arrives with its callers already read | slow to reach the risky parts; leaves unreachable files stranded for a final pass | *I want to know this system* |
| **risk-weighted** — churn × size, most-changed first | defects early, while attention is fresh | you meet the hardest code while your model of the system is weakest | *this thing keeps breaking* |
| **dependency** — leaves first, upward | nothing is read before what it depends on | utilities read with no idea what uses them, which is the stranger problem in its purest form | correctness work, small codebases |
| **directory** — top to bottom, alphabetical | zero decisions, obviously complete, trivially resumable | adjacency means nothing; two files beside each other may share no ideas | prose, config, anything without a call graph |

**Narrative is the usual answer for a first sweep**, because a first sweep is
almost always somebody wanting to know their own system, and it is the only
order in which understanding accumulates rather than resets.

**Directory order is underrated and not a failure of nerve.** For a
documentation tree, a config directory, or a package of independent leaf
modules, there is no structure for a cleverer order to follow, and inventing one
costs a decision per sitting to buy nothing.

## Risk-weighted is often the wrong tool wearing the right name

**If you already know what you are looking for, you want an audit rather than a
sweep.** A sweep covers everything and takes weeks; a targeted audit answers the
question this week and produces findings somebody else can answer. Ordering a
sweep by risk is a way of getting an audit slowly.

*The `audit-records` bundle covers that shape.* Choose risk-weighted when you
genuinely want full coverage **and** want the frightening parts read while you
are still fresh — which is a real preference, just a rarer one than it sounds.

## The order changes the sequence, never the set

**Every file in scope is covered whatever order you chose.** An order that
quietly drops files is a scope decision pretending to be an ordering one, and
scope belongs in `sweep.md` under what was excluded, where a reader can see it.

**Narrative order needs a final pass** for everything no entrypoint reaches —
utilities, generated files, dead code. That pass is where dead code is found,
which is a large part of why the order is worth using.

## Changing order mid-sweep

**Allowed, and worth doing when the first choice is clearly not working.** Write
it in the sweep as a dated line: what it was, what it is now, why.

**What is not allowed is changing it silently**, one convenient sitting at a
time. That is how an order becomes *whatever seemed next* without anybody
deciding to abandon it — and the sweep loses the only record of why its
coverage looks the way it does.

## Grouping by concern is not an order

*Read all the error handling, then all the configuration* is a legitimate
review, and it is not a sweep: it covers aspects rather than files, so nothing
can be marked off and the index never retires anything.

**Run it as its own thing if it is what you want.** Do not run it inside a sweep
and expect coverage to mean anything afterwards.
