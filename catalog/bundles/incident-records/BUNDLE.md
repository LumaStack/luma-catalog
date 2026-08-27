---
type: bundle
version: 0.1.0
published: 2026-08-27
consumers: [project, organization]
entry_point: policy/recording-an-incident
description: Incidents as records — one place for everything that went wrong, and a different shape for each kind, because an outage and a data breach do not answer the same questions.
---

# Incident records

Something went wrong and somebody will ask about it in a year. **One place for
every kind of wrong, and a different form for each** — because an outage, a
leaked credential, a data breach and an agent that broke a policy have almost
nothing in common past *what happened, when, and who was hurt*.

## What is here

- [[recording-an-incident]] — the policy. What counts as an incident, how
  severity is graded, and what each kind owes.
- [[record-an-incident]] — the workflow. Open it while it is happening.
- **Templates**, one per kind, each complete and copied whole —
  [outage](templates/incident-outage.md) ·
  [security](templates/incident-security.md) ·
  [data breach](templates/incident-data-breach.md) ·
  [AI policy breach](templates/incident-ai-policy-breach.md)

**No incidents are in here.** Records live where the project keeps records —
`.luma/records/incidents/` — never in a bundle, because a vendored copy cannot be
edited by the project holding it.

## The four ideas worth knowing before reading further

**One type, several shapes.** The type carries what every incident has: what,
how bad, when, who noticed, who was hurt. Everything past that lives in the
kind's template. **A type carrying every kind's fields would mark nearly all of
them `optional`, which is a type that has stopped constraining anything.**

**`security` and `data-breach` are separate on purpose.** A compromised
credential with nothing exfiltrated is one; the moment data left it is the other,
and a legal clock starts that the security form has no field for. **Recording the
second as the first is how a notification deadline gets missed** — not through
malice, but because the form never asked. When it is unknown, and early it
usually is, use `data-breach`.

**An AI policy breach asks whether the policy was ever delivered.** An agent that
violated a rule it was never given has not failed — **the delivery has**, and
fixing the agent fixes nothing. No other kind here has a field whose answer can
exonerate the actor outright, which is why it is a field rather than a paragraph
somebody might omit.

**Severity is harm that reached the world**, not urgency and not effort. *It
could have been worse* is the most useful sentence in most records and the worst
possible severity field.

## Consumers

Both levels. A project records its own incidents; an organization reads across
them, which only works because they land in one place under one numbering.

## Version

`0.1.0` — first release.

**Four kinds ship and the vocabulary is open.** An organization with a kind that
fits none of them should add one rather than force a fit — `other` exists for the
gap and is a prompt to write the missing template, not a resting place.

**The shared sections are duplicated across all four templates rather than
factored out.** Templates are for copying, and an author under incident pressure
should copy exactly one file — not assemble two and discover halfway that a
section is elsewhere. The cost falls on whoever edits templates, which is rare,
rather than on whoever uses them, which is when nobody has attention to spare.

**`recorded_under` is new here and is worth watching.** It records the bundle
version that shaped a record, so an old one can be read correctly and migrated
without guessing intent from shape. **It is provenance, not a dispatch key** —
`change-a-shared-type` still holds, and tools stay field-tolerant. Audits,
decisions and retirements have the same blind spot; this is one type carrying the
field to see whether it earns its keep before four do.

**What an adopter has to do:** decide where incidents live if not
`.luma/records/incidents/`, and read the severity table before the first
incident rather than during it.
