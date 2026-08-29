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

**The near-miss.** <the wrong version and the right one, side by side, in two
lines. The wrong one has to look like compliance.>
```

## Write it to be followed, then make it small

**In that order, and they do not compete.** Cut explanation, hedging and
repetition. Never cut a heading, a standalone label, or the example showing the
near-miss — those are what make the rule survive being read in a hurry, in
fragments, by something that will not go back for context.

**Departing from any of this is allowed and has to be written down**, with the
reason, in the document — see [[what-an-enhancement-is]]. Skipping a requirement
silently is indistinguishable from not having attempted it.

## The three that get written wrongly

**Both lists are required, and ALWAYS carries more.** A prohibition makes the
model represent the banned behaviour and then invert it; a positive instruction
gives it a target. A NEVER longer than its ALWAYS is inverted.

**The near-miss is the highest-leverage part**, and the one to protect when
trimming — an example outweighs more instruction. See
[[what-makes-a-guardrail-stick]].

**A weak one is worse than none.** An example outweighs the instruction above
it, so a vague or invented near-miss teaches a wrong edge and gets followed over
the rule. Never fabricate one to fill the slot.

**If you cannot write one, stop and look at the rule.** A behaviour with no
near-compliance case is obvious enough to need no guardrail, or too vague to be
followed. Where it is genuinely absent, write `**No near-miss.**` and one line
saying why — a silent omission reads as an oversight and gets "fixed" later by
somebody inventing filler.

**Test ALWAYS literally.** If a bullet is not true *every* time, it is not
scoped yet — and an unscoped ALWAYS produces padding appended to every turn,
which costs more than the behaviour it was aimed at.

**Every label has to stand alone.** A reader who meets one block with none of
the others still knows what it is. That is why there is no *Instead*: a
connective means nothing to whoever is holding one fragment.
