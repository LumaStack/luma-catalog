---
type: bundle
version: 0.1.0
published: 2026-08-18
consumers: [project, organization]
entry_point: workflows/recording-decisions
description: Decisions recorded with their reasoning, deferred alternatives, and re-open triggers.
---

# Decisions

A decision without its reasoning is not finished. The answer is perishable — it
gets superseded, or the constraint that forced it disappears — but the argument
is what survives, and it is the only thing that lets someone six months later
tell a decision that still holds from one that was never revisited.

This bundle carries the contract for a decision record, the workflow for keeping
them, and the rule for when to correct one versus supersede it.

It applies at both levels deliberately. An organization records decisions about
how it works; a project records decisions about how it is built. The documents
are the same shape, and which level a given adopter wants is not the
publisher's call to make.

## What is here

- [[recording-decisions]] — the workflow. Where records live, what to do when
  nothing exists yet, and how a project graduates from one file to many.
- `_types/decision` — a single decision record.
- `_types/decision_log` — one document holding many decisions, for projects
  small enough that a directory would be overhead.
- `_types/workflow` — a procedure a person or agent follows.

## Loading

Only [[recording-decisions]] is `preload: mandatory` — a consumer that cannot
load it should fail rather than proceed without it, because everything else here
is a contract it refers to.

The Type Definitions carry no `preload` at all, which means `optional`: they are
read when something needs to know what a field means, not held in context
against the possibility. That is the field working as intended rather than an
omission.

## Version

`0.1.0` rather than `1.0.0`. The conventions here are extracted from practice
rather than invented, but that practice is days old and has been run in one
place. `1.0.0` would claim more than is true.
