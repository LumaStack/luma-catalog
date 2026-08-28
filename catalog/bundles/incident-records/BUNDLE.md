---
type: bundle
version: 0.2.1
published: 2026-08-27
consumers: [project, organization]
entrypoint: policy/recording-an-incident
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

`0.2.1` — **`entry_point` is now `entrypoint`.** One word, per LKF §11.1, so the same word names the same thing at every level it appears.

Patch: one key renamed. Same value, same meaning, same `optional` presence, and `luma-foreman` reads both spellings while the rename lands.

`0.2.0` — **`recorded_under` becomes `created_using`, and is fixed forever.**

*The preposition was worked at.* `under` reads as a regime the record answered
to; a bundle version is not that. `with` is instrumental but can read as
accompaniment — *created with a colleague* — which matters in a type that already
carries `detected_by` and `responders` as actors. **`using` can only mean
instrument.**

**It names the bundle version that created the record** — the adopted copy that
was actually read, not what the catalog published then or has since. The vendored
bundle under `.luma/bundles/` is the one in play, so there is nothing to
disambiguate.

**And it never changes, including by a future migration.** A single field
overwritten on each migration would answer *which version created this* right up
until the first migration, then quietly stop — the worst kind of change, because
nothing announces it. `created_using` means one thing and always will.

**Room for migrations, which do not exist.** No machinery ships here. When
something does migrate records, `migrated_using` is **added beside** this field:
purely additive, since a consumer must not reject a document for keys it does not
understand, so a minor bump and no existing record becomes wrong. If chains turn
out to be common, that field grows into a list — also additive. **Neither is
designed now**, because a mechanism built before its first user is a guess with a
version number.

**The templates also stopped asserting a version they cannot know.** All four
hardcoded `incident-records 0.1.0` and were already lying one release later — a
provenance field lying about provenance. The catalog cannot know what any adopter
holds, so a pre-filled value is wrong by construction rather than merely stale.
They carry a placeholder and name the command that reads it,
`luma-foreman bundle show incident-records`.

Minor rather than patch: a required field is renamed, which breaks anything
reading `recorded_under`. Nothing does — `0.1.x` shipped today and is adopted
nowhere.

`0.1.1` — **`recorded_under` keeps its place on better reasons than it was given.**
`0.1.0` claimed the provenance it captures "cannot be reconstructed", which is
false: the record is committed, and at that commit `adopted.toml` names the
version held. Git answers this in the ordinary case, and *do not store what
subtraction can answer* is a rule this bundle applies elsewhere.

**What survives is narrower and holds.** The commit is not when the template was
copied — a record opened during an incident and committed days later reports the
wrong version confidently, and drafting late is normal for exactly this kind of
work. Records also travel into registers and postmortems where history does not
follow, and a hand-copied template leaves no adoption trace at all.

*Whether that is enough is genuinely open*, which is why the field stays on one
type rather than spreading to audits, decisions and retirements. If records never
travel and drafts always land same-day, git is sufficient and this is ceremony.

Patch: no field changed, only the argument for one.

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

**No `event` trigger, and the first draft wrongly had one.** It declared
`event: incident-declared`, which is not in the format's closed vocabulary —
before-commit, before-merge, before-push, before-release, session-end,
session-start. **A name nothing fires is a rule that never arrives**, and CI
caught it before this shipped. The policy matches on topic alone, which is
sufficient: an incident is declared by a person noticing, not by a hook.

*If an `incident-declared` event is ever worth having, it belongs in the format
as a vocabulary change, not invented in a bundle that reads it.*

**What an adopter has to do:** decide where incidents live if not
`.luma/records/incidents/`, and read the severity table before the first
incident rather than during it.
