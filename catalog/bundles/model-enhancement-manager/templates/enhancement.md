# Enhancement template

Copy the blocks below into `<model-bundle>/policy/<kebab-slug>.md`. **Copy the
blocks, not this file** — a template carrying `type: policy` would be indexed
and loaded as a real guardrail.

The shape is in [[what-an-enhancement-is]]; the budget it has to fit is in
[[the-per-session-budget]].

## Frontmatter

```yaml
---
type: policy
title: <imperative — the rule, not the failure. "Check before objecting">
description: <the behaviour, then the correction, in one sentence>
---
```

**No `matches`.** A guardrail is reached through its bundle's entrypoint and
declares nothing of its own — see [[the-entrypoint-compels-the-read]].

## Body

```markdown
# <the same words as the title>

**Problem.** What the model does, stated plainly and without excuse. Name the
case if one sentence covers it.

**Goal.** What it should do instead, in a sentence.

**ALWAYS**
- <two or three bullets, each true every time>

**NEVER**
- <the specific things not to do, including the tempting near-miss>
```

## Write it to be followed, then make it small

**In that order, and they do not compete.** Cut explanation, hedging and
repetition. Never cut a heading, a standalone label, or the example showing the
near-miss — those are what make the rule survive being read in a hurry, in
fragments, by something that will not go back for context.

## The three that get written wrongly

**Both lists are required.** ALWAYS alone leaves the failure available. NEVER
alone leaves nothing to replace it with, and a model given a prohibition and no
substitute finds a neighbouring way to fail.

**Test ALWAYS literally.** If a bullet is not true *every* time, it is not
scoped yet — and an unscoped ALWAYS produces padding appended to every turn,
which costs more than the behaviour it was aimed at.

**Every label has to stand alone.** A reader who meets one block with none of
the others still knows what it is. That is why there is no *Instead*: a
connective means nothing to whoever is holding one fragment.
