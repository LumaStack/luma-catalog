# Idea template

Copy the blocks to `.luma/backlog/ideas/<slug>.md`. **Copy the blocks, not this
file.**

The whole point is that this is fast. **Only the first three fields are needed
to capture something** — everything else can wait for a tending session, and
`horizon` already defaults to `someday` when absent.

## Frontmatter — capture

```yaml
---
type: idea
title: <the idea in one line>
captured: YYYY-MM-DD
originated: human:<id>
---
```

`originated` answers **was a person involved in having this**, not who typed it.
An agent that prompted the idea, phrased it and wrote the file is a
`contributor`; the person who had it is the originator. Use `agent:<model>` only
when **no person was involved at all** — that is the case somebody needs to be
able to find.

## Frontmatter — when curating

```yaml
---
type: idea
title: <the idea in one line>
captured: YYYY-MM-DD
originated: human:<id>
contributors: [agent:<model>]
horizon: next | later | someday
scope: project | department | organization
lifecycle_status: draft
archived: YYYY-MM-DD          # only when pruning
---
```

## Body

```markdown
# <the idea in one line>

<One or two sentences. What it is — not how it would be built.>

## The problem it addresses

<Recommended, not required. What is wrong now, or what becomes possible.

 Skip it at capture time. An idea whose problem you cannot state in a sentence
 is often one worth revisiting later rather than solving now.>

## Why not now

<Optional, and useful surprisingly often: too large, blocked on something,
 unclear, or simply not worth the current week. This is what a future reader
 checks first to see whether the reason still holds.>

## Notes

<Anything worth keeping. Prior art, an objection somebody already raised, the
 conversation it came out of.

 If this section grows long enough to need headings, the idea has probably
 become a backlog item — see the type definition.>
```

## Before moving on

- **Did you stop mid-flow to write this?** Do not. Capture the run first,
  tidy afterwards.
- **Does something like it already exist?** Check *after* capturing, not before,
  and merge rather than accumulate.
- **Working with a person?** Propose it and get agreement before writing
  anything durable.
