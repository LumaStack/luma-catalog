---
type: policy
title: The entrypoint compels the read
description: Every model enhancement bundle has exactly one document that fires, it names every guardrail, and it requires them rather than offering them.
matches:
  - topic: structuring a model enhancement bundle
---

# The entrypoint compels the read

**One document fires. It is the entrypoint, and it carries the model trigger:**

```yaml
matches:
  - model: <name+version>
```

**Nothing else in the bundle declares `matches` at all.** The guardrails are
on-demand and are reached only through the entrypoint, which names every one of
them and states — imperatively, in its first line — that they must be read and
followed.

## Why it is a mandate and not a list

**A guardrail cannot be topic-matched.** One that arrives after the mistake is a
description of the mistake, so the guardrails have to be in hand before the work
starts. An entrypoint that merely describes what is available gets skimmed; one
that says *you must read these* is an instruction the model can be held to.

**And one firing document is what a hook can deliver.** Whatever eventually
learns which model is running has a single target per bundle rather than a set
that grows every time a guardrail is added.

## What it does not buy

**It defers the cost, it does not remove it.** An agent that complies reads
every guardrail, so the words are the same. What changes is that the charge is
made once, deliberately, at a point where the agent has been told why — rather
than accruing invisibly across a set of documents that each claimed a seat.

**So [[the-per-session-budget]] still applies to the whole bundle**, not to the
entrypoint alone. Counting only the document that fires would be measuring the
invoice instead of the bill.
