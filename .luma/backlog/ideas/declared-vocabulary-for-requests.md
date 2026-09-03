---
type: luma/idea
title: Declared vocabulary — what a request means, bound to what an agent does
created: { by: human:benlinton, at: 2026-08-17T00:00:00Z }
contributors: [human:benlinton, agent:claude-opus-5]
horizon: later
scope: project
stage: draft
---

# Declared vocabulary — what a request means, bound to what an agent does

A way to declare that a particular request means a particular thing, so an agent
resolves it the same way every time instead of improvising.

The entry as originally written:

> What does it mean when i say:
> - I want a situation report
>   you should respond with: "Let me drop the options and show you the actual situation."
> - I need help coming up to speed
> - Where did we leave off
> - What do you know to be true
> - Checkpoint

## Notes

Migrated from `luma-foreman/docs/IDEAS.md` on 2026-08-21. `created.at` is a
day-level estimate from git history.

**Retitled at migration, because three of the five phrases already resolve.** The
`session-manager` bundle implements them: `session-checkpoint` is *Checkpoint*,
and `session-resume` — the arriving side — covers both *where did we leave off*
and *I need help coming up to speed*. So the want is not five new capabilities
but a **binding layer**: a declaration that this phrase runs that workflow. The
five phrases are the evidence, not the specification.

Two are genuinely uncovered: *I want a situation report*, the only one with a
specified response, and *what do you know to be true*.

**Already named as a missing bundle.** `luma-foreman/docs/next-steps.md` lists
*"Working-style preferences — how an agent should behave here, as adoptable
content rather than as `CLAUDE.md` prose nobody versions"* among the gaps in this
catalog's coverage.

**`scope: project` is a lean on the default, recorded as such.** These are one
person's phrases. The *mechanism* is universal and belongs to a bundle, but the
*content* is personal — and there is no `personal` scope, only `project`,
`department` and `organization`. That mismatch is evidence about the scope list
rather than a fact about this idea.
