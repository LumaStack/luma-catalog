# ADR-NNNN: <short decision title, active voice>

- **Date:** YYYY-MM-DD
- **Status:** Draft | Provisional | Ratified | Superseded by ADR-NNNN | Retired | Rejected

> Copy to `docs/decisions/ADR-NNNN-kebab-title.md` (next free 4-digit number). Status is always
> tracked and sets what you may edit: **Draft/Provisional** records are edited freely as they settle;
> a **Ratified** decision is frozen — edit only to clarify (with approval), and supersede or retire it
> to change it. See [README.md](README.md) → Status lifecycle. Keep the four **required** sections;
> add **optional** ones only when they carry real content (an empty section hasn't earned its place —
> delete it).

<!-- ─── Required ──────────────────────────────────────────────── -->

## Summary

One sentence: what was decided.

## Problem

Why are we deciding anything? The trigger, the forces, the constraints.

## Decision

What was actually decided — "We will …".

## Why

The rationale. Observable reasoning, not opinion — "it replaces three agents with one and
speaks Prometheus, Loki, and OTLP", not "it's obviously best".

<!-- ─── Optional (delete the ones you don't use) ──────────────── -->

## Alternatives

Options evaluated, each with a one-line why-not.

## Tradeoffs

What we gain and give up — explicitly.

**Pros**
- …

**Cons**
- …

## Assumptions

Things believed true when deciding. If one proves false, that's a reason to revisit — feed
those into **Revisit When**.

## Revisit When

Conditions that should reopen this decision, so it doesn't persist by inertia — e.g. "Docker
supports feature X", "we exceed 100 hosts", "cost exceeds $200/month".

## Follow-up

Tasks this decision creates — *link* to the backlog / a project / an issue; don't inline them.

## References

Supporting docs and research, plus **related/affected decisions** — link other `ADR-NNNN`
this one *supersedes*, *makes obsolete*, *amends*, or *relates to*. (A supersede is also
reflected in **Status**; flip the superseded record's Status too.)
