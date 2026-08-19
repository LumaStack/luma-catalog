---
type: policy
title: Decision guidelines
description: AGENT NEEDS TO FILL THIS IN.
preload: mandatory
---

# Decision guidelines

## Architecture Decision Records (ADR)

Durable records of significant decisions — *why* the system is the way it is. One file per
decision, named `ADR-NNNN-kebab-title.md`, numbered. A record's **status** sets how settled the
decision is *and* what you may edit (see [Status lifecycle](#status-lifecycle)): **Draft** and
**Provisional** records are edited freely as they settle; a **Ratified** decision is frozen — you
may only improve *how it's explained* (with approval), and change the decision *itself* only by
superseding or retiring it. Starting a new one? Copy [`decision-template.md`](decision-template.md).

## Working style

For open-ended decisions, lead with an honest comparison plus a recommendation in prose and invite discussion before presenting structured multiple-choice prompts; let the user steer the choice.

## Conventions

- **Record a decision early** — even as a **Draft** while it's still being argued, or **Provisional**
  the moment you start acting on it. Capturing intent early is the point; don't wait for it to be
  built.
- **One decision per record.** If a discussion yields three independent choices, write three
  records.
- **Focus on *why*, not implementation.** How-to belongs in project plans / runbooks — link to
  them, don't duplicate.  Why will survive the longest.
- **Link, don't duplicate.** Point to related tasks, design docs, runbooks, and other `ADR`s.
- **What you may edit depends on the record's status** (see [Status lifecycle](#status-lifecycle)).
  **Draft** and **Provisional** records are *meant* to move — edit them in place freely as the
  decision settles; no approval and no superseding record needed for a refinement. A **Ratified**
  record is frozen: the decision never changes, so **never delete or overwrite it to save space**,
  and edit it *only* to improve how it's explained — a stale reference, a typo, a dead link,
  terminology the codebase has since renamed. **Every edit to a Ratified record must be approved by
  the user first, however trivial — down to a one-character typo.** When in doubt whether a change is
  a mere clarification (vs. a decision change needing a superseding record), raise that too.
- **A changed decision is never a small edit.** If the *decision or its rationale* actually changes,
  don't rewrite the old text — flip its Status and add a dated note: a *different* decision replacing
  it gets a *new* record that **supersedes** it (Status `Superseded by ADR-NNNN`); one that simply
  reached its planned end (e.g. a stopgap whose *Revisit When* trigger fired) gets Status
  `Retired` + a short dated closing note.
- **Write for a newcomer.** Include enough context that someone without the original discussion
  can follow the reasoning.

### Separate facts from opinions

Reasoning must be observable, not asserted.

- Avoid: *"Alloy is obviously the best."*
- Prefer:
  - **Decision** — Use Alloy.
  - **Why** — it replaces three agents with one and supports Prometheus, Loki, and OTLP.

### Record tradeoffs explicitly

State what was **gained and sacrificed** — Pros *and* Cons. Future readers get the context
immediately. (Don't just write "We chose ZFS"; list the checksums/snapshots/replication wins
*and* the RAM/complexity/resilver costs.)

### Capture triggers for re-evaluation

Use the **Revisit When** section to list the conditions that should reopen the decision — so it
doesn't become permanent by inertia. Examples: "Docker supports feature X", "we exceed 100
hosts", "cost exceeds $200/month", "Grafana Alloy becomes unsupported".

## Status lifecycle

Every record carries a status. It's a **mutability ladder** — the status says how settled the
decision is *and* what you're allowed to edit.

**Live** — is, or could become, the current answer:

| Status | Means | What you may edit |
|--------|-------|-------------------|
| **Draft** | The decision isn't made yet — proposed, under discussion | Anything; nothing is binding |
| **Provisional** | Decided and in force, but *on trial* — we expect to tune it | Edit in place freely as it settles; no approval, no superseding record needed |
| **Ratified** | *Settled and unwavering* | The **decision never changes**. Edit only to aid understanding/adoption (clarify wording, add an example, fix a stale link) — and get approval first. Change the decision *itself* only by **Superseding** or **Retiring** it |

**Terminal** — no longer the current answer; kept as frozen history:

| Status | Means |
|--------|-------|
| **Superseded by ADR-NNNN** | A *different* decision replaced it — point at the replacement |
| **Retired** | Withdrawn / no longer in force, with no single replacement (e.g. a stopgap whose *Revisit When* trigger fired) — add a short dated closing note |
| **Rejected** | Considered but never adopted — died as a Draft/Provisional |

Typical path: `Draft → Provisional → Ratified`, then later `Superseded by ADR-NNNN` or `Retired`;
or `Rejected` if it's never adopted.

Example: `Status: Provisional` · `Status: Ratified` · `Status: Superseded by ADR-0014` ·
`Status: Retired`.

## Format

See [`decision-template.md`](templates/decision-template.md). Two tiers:

- **Required (every record):** Summary · Problem · Decision · Why.
- **Optional (add only when they carry real content):** Alternatives · Tradeoffs (Pros/Cons)
  · Assumptions · Revisit When · Follow-up · References.

An empty section hasn't earned its place — delete it. There's no standalone *Risks* section:
accepted downsides go in **Tradeoffs → Cons**, and "what would make us reconsider" goes in
**Revisit When**.