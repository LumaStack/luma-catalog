# Entrypoint template

Copy the blocks below into `<model-bundle>/policy/entrypoint.md`. **Copy the
blocks, not this file.**

**This is the only document in a model bundle that declares `matches`**, and
every bundle has exactly one — see [[the-entrypoint-compels-the-read]].

## Frontmatter

```yaml
---
type: policy
title: <Model> guardrails — read these now
description: The guardrails for this model. Each must be read and followed before the work, not after a correction.
matches:
  - model: <name+version>
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
