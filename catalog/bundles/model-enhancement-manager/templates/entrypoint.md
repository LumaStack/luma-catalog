# Entrypoint template

Copy the blocks below into `<model-bundle>/policy/entrypoint.md`. **Copy the
blocks, not this file.**

**No `matches`, here or anywhere else in a model bundle.** `model` is not in
the trigger vocabulary, so the condition cannot be declared — see
[[loading-by-model-is-unsolved]]. The entrypoint is reached through the bundle's
ring, and everything else through the entrypoint.

## Frontmatter

```yaml
---
type: policy
title: <Model> guardrails — read these now
description: The guardrails for this model. Each must be read and followed before the work, not after a correction.
---
```

## Body

```markdown
# <Model> guardrails — read these now

**YOU MUST READ EVERY DOCUMENT LISTED BELOW, AND YOU MUST FOLLOW IT.**

They are not advice and they are not preferences. Each one names a behaviour
this model has already cost a user real time with. Read them before doing the
work — after a correction is too late, because the correction is the cost.

- [[<guardrail-slug>]] — <one line, stating the rule>

They sit beside this file, in this bundle's `policy/` directory.

**If one of them makes the work worse, say so rather than working around it.**
```

## What the lines say

**One line per guardrail, and it states the rule rather than the symptom.**
Somebody deciding whether to open it needs the instruction — *verify before
saying why something will not work*, not *fluent objections nobody checked*.

**The last line is not politeness.** A guardrail that fires wrongly costs more
than none, and the model is the only party positioned to notice.
