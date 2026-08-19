---
type: policy
title: Writing a decision record
description: When to record a decision, what makes one worth reading years later, and what you may edit once it is settled.
preload: mandatory
---

# Writing a decision record

The contract — which fields a record carries — is in `_types/decision`. This is
the craft: when to write one, what makes it survive, and what you may change
after the fact.

## Record it early, and record it small

**Write the record while the decision is still being argued**, as a `draft`, or
as `provisional` the moment you start acting on it. Capturing intent is the
point; waiting until it is built means writing from memory about reasoning you
have already lost.

**One decision per record.** A discussion that produced three independent
choices produces three records. Bundled decisions cannot be superseded
independently, so the first one to change drags two unrelated positions with it.

**Write for a newcomer.** Enough context that someone who was not in the
discussion can follow the reasoning. The reader you are writing for has not met
any of this before and cannot ask you.

## Reasoning must be observable

A record that asserts is worth nothing to the person who disagrees with it.

- Avoid: *"Alloy is obviously the best choice."*
- Prefer: *"Alloy replaces three agents with one and speaks Prometheus, Loki
  and OTLP."*

The second can be checked, argued with, and invalidated when it stops being
true. The first can only be believed or dismissed.

**Focus on why, not how.** Implementation belongs in a runbook or a project
plan — link to it. The *why* outlives every one of them, and it is the only
part nobody can reconstruct later.

## State what was given up

Record the **tradeoff**, not just the choice. What was gained and what was
sacrificed, explicitly, both sides.

*"We chose ZFS"* tells a future reader nothing. Checksums, snapshots and
replication **against** memory footprint, complexity and resilver time tells
them whether the decision still holds under their constraints.

A record with no cons is a record that either hid something or never examined
it, and both read the same way years later.

## Say what would reopen it

A decision with no re-open condition becomes permanent by inertia — not because
anyone reaffirmed it, but because nobody knew what would justify revisiting.

Name the conditions concretely: *"if the platform gains feature X"*, *"above
100 hosts"*, *"if cost exceeds $200 a month"*, *"if this tool becomes
unmaintained"*. Vague triggers never fire.

## What you may edit depends on how settled it is

`lifecycle_status` is a **mutability ladder**, not just a label. It says how
settled the decision is *and* what you are permitted to change.

| `lifecycle_status` | means | what you may edit |
| --- | --- | --- |
| `draft` | proposed, under discussion, not yet decided | anything — nothing is binding |
| `provisional` | decided and in force, but on trial | freely, in place, as it settles. No approval, no superseding record |
| `stable` | settled | **the decision never changes.** Only how it is explained — and with approval first |
| `archived` | no longer the current answer, kept as history | nothing |

**A `stable` record is frozen.** Fix a stale reference, a dead link, a typo, or
terminology the codebase has since renamed — and get agreement before doing even
that. Never delete or overwrite one to save space; the whole value is that it is
still there.

**A changed decision is never an edit.** If the decision or its reasoning
actually changes, do not rewrite the old text:

- **A different decision replaces it** — write a new record, set the old one to
  `archived`, and point `superseded_by` at the replacement.
- **It reached its planned end** — a stopgap whose re-open condition fired —
  set `archived` and add a short dated closing note.

When you cannot tell whether a change is clarification or a new decision, raise
that question rather than guessing. Guessing wrong in one direction loses
history; in the other it clutters the record with records.

## Sections

See [the template](../templates/decision-template.md).

**Required, every record:** Summary · Problem · Decision · Why.

**Optional, only when they carry real content:** Alternatives · Tradeoffs ·
Assumptions · Revisit When · Follow-up · References.

**An empty section has not earned its place — delete it.** A record padded with
headings and no content is harder to read than a short one, and it teaches the
next author that the headings matter more than the reasoning.

There is no *Risks* section: accepted downsides are Tradeoffs, and what would
change the answer is Revisit When.

## Working style, when a decision is still open

For an open-ended question, **lead with an honest comparison and a
recommendation in prose**, and invite discussion before offering a structured
choice. Multiple-choice too early narrows the space to whatever the options
happened to contain.
