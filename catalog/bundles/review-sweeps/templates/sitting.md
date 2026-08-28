# Sitting template

Copy the blocks to `.luma/backlog/reviews/<slug>/sittings/<NNN>-<slug>.md`.
**Copy the blocks, not this file.**

## Frontmatter

```yaml
---
type: sitting
title: <the cluster, in a few words>
created: YYYY-MM-DD
covers:
  - src/cli.py
  - src/args.py
contributors:
  - human:<id>
  - agent:<model>
---
```

**List every file read, including the ones where nothing was found.** Coverage
is derived from `covers`; a file left out of it cannot be shown to have been
examined.

## Body

```markdown
# <NNN>: <the cluster>

## What this is

<The orientation, compressed to what is worth keeping. What these files do and
how they connect — the part a later sitting will want.>

## What we made of it

<Their read first, then yours. Where you disagreed, and why — a sitting where
the agent agreed with everything is worth a second look.>

<If the agent read first — because they asked, or because the file warranted
it — say so here. A disclosed weakness can be discounted.>

## What this makes me doubt about earlier

<Optional, and often the most valuable section. A sweep learns as it goes and
the ninth sitting routinely falsifies the third.>

## Where it went

<Every outcome, routed out of the sweep during this sitting. Nothing worth
keeping stays in this note — it is archived with the sweep and eventually
deleted.>

| what | where it went |
| --- | --- |
| retry loop swallows the timeout | fixed — PR #214 |
| this whole layer wants restructuring | idea — `.luma/backlog/ideas/flatten-the-transport-layer.md` |
| why the cache is keyed on the raw path | decision — ADR-0012 |
| the four config readers disagree | finding — audit 2026-09-02-a1b2c3d4e5f6 |

## Still open

<Only a conclusion the sweep genuinely has not reached yet — a suspicion needing
more sittings before it can be stated. Say what would confirm it.>

<Not a to-do list. Anything actionable was routed above.>
```
