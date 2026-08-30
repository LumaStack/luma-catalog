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
- <the edges — the specific things not to do>

**Contrastive example.** <the wrong version and the right one, side by side, in two
lines. The wrong one has to look like compliance.>
```

## Write it to be followed, then make it small

**In that order, and they do not compete.** Cut explanation, hedging and
repetition. Never cut a heading, a standalone label, or the contrastive
example — those are what make the rule survive being read in a hurry, in
fragments, by something that will not go back for context.

**Departing from any of this is allowed and has to be written down**, with the
reason, in the document — see [[what-an-enhancement-is]]. Skipping a requirement
silently is indistinguishable from not having attempted it.

## The three that get written wrongly

**Both lists are required, and ALWAYS carries more.** A prohibition makes the
model represent the banned behaviour and then invert it; a positive instruction
gives it a target. A NEVER longer than its ALWAYS is inverted.

**The contrastive example is the highest-leverage part when it is real**, and
the one to protect when trimming — an example outweighs more instruction. See
[[what-makes-a-guardrail-stick]].

**Try to write one every time; include it only if it is real.** The attempt is
what has value: failing to find a case that sits on the border tells you the
rule is vague, or obvious enough to need no guardrail. Fix the rule then.

**Never fabricate one to fill the slot.** A weak example outweighs the
instruction above it just as a good one does, and teaches the wrong border.
Leave it out where it does not fit or would not make the policy better — that
needs no note and is not a gap.

**Test ALWAYS literally.** If a bullet is not true *every* time, it is not
scoped yet — and an unscoped ALWAYS produces padding appended to every turn,
which costs more than the behaviour it was aimed at.

**Every label has to stand alone.** A reader who meets one block with none of
the others still knows what it is. That is why there is no *Instead*: a
connective means nothing to whoever is holding one fragment.
