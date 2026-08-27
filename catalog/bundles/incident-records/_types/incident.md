---
type: type_definition
defines: incident
fields:
  incident_id:
    field_presence: required
    field_type: text
    desc: "3–5 letters, a dash, then digits — INC-0007. Never reused, and what every later reference cites"
  kind:
    field_presence: required
    field_type: enum
    values: [outage, security, data-breach, ai-policy-breach, other]
    desc: "what happened, which decides how it is recorded. An open vocabulary — an organization adds its own rather than forcing a fit"
  severity:
    field_presence: required
    field_type: enum
    values: [sev1, sev2, sev3, sev4]
    desc: "how much harm reached the world, not how loud it was. Graded per kind — see the policy"
  detected_at:
    field_presence: required
    field_type: timestamp
    desc: "when somebody or something first knew. The one timestamp always knowable exactly"
  began_at:
    field_presence: recommended
    field_type: timestamp
    desc: "when it started, which is usually an estimate. Say so in the body rather than implying precision"
  resolved_at:
    field_presence: optional
    field_type: timestamp
    desc: "when it stopped. Absent means open — the status is derived from this field, never stored separately"
  detected_by:
    field_presence: required
    field_type: actor
    desc: "who or what noticed (§7.4). A `process:` here and a `human:` there is the difference between a check that works and one that does not"
  responders:
    field_presence: recommended
    desc: "who acted. No field_type: a list of actors, which §10.2 cannot yet express"
  impact:
    field_presence: required
    field_type: text
    desc: "who or what was affected, in one line. Nobody, honestly stated, is a valid and useful answer"
  recorded_under:
    field_presence: required
    field_type: text
    desc: "the bundle and version that shaped this record — `lumastack/luma-catalog/incident-records 0.1.0`. Provenance for migration, never a dispatch key. See below"
---

# Incident

**One thing that went wrong, recorded once, where every kind of wrong lands in
the same place.** An outage, a leaked credential, a breach, an agent that
violated a policy — all incidents, all `INC-` numbered, all in the same
directory.

## One type, several shapes

**The fields above are what every incident has.** They are the questions you can
ask about any of them: what happened, how bad, when, who noticed, who was hurt.

**Everything past that differs by `kind`, and forcing it not to would be worse.**
A data breach needs the data categories, the jurisdictions and the notification
clock. An outage needs the services and the customer-facing duration. An AI
policy breach needs the model, the policy, and whether the output was acted on.
**Those sets have almost nothing in common**, and a type carrying all of them
would mark nearly every field `optional` — which is a type that has stopped
constraining anything.

**So the kind-specific fields live in the templates, not here.** Each kind's
template is a complete document with its required sections, and
[[recording-an-incident]] says what each kind owes.

## The limitation, stated rather than discovered

**A Type Definition cannot say *if `kind` is `data-breach` then jurisdictions are
required*.** `field_presence` is per-field and unconditional (§10.2), so nothing
mechanical enforces the per-kind requirements.

**That is a real gap and it is carried deliberately.** The alternatives were a
type per kind — which puts incidents in different places and shares nothing — or
conditional field logic, which the format does not have and which would be a
large thing to invent for this. **What fills the gap is the template and a
reader**, and saying so is better than implying a check exists.

## `recorded_under` — provenance, and deliberately not a dispatch key

**An incident says which bundle version shaped it.** Not the type alone: what an
incident record actually looks like comes from the type *and* the kind's
template, which version together as the bundle.

**Two things it buys**, both of which arrive years later and cannot be
reconstructed:

- **Reading an old record correctly.** *Why does INC-0004 have no `began_at`?*
  is answerable if you can see it was written under `0.1.0`, where the field did
  not exist. Without it you are guessing whether somebody omitted it or could not
  have supplied it.
- **Migrating without changing meaning.** A migration that knows what a record
  was written against can move it forward; one that does not has to infer intent
  from shape, which is how a migration quietly rewrites what a record said.

**It must not become a version switch, and this is the part worth guarding.**
`change-a-shared-type` states the rule it appears to contradict: *tools are
field-tolerant rather than version-aware, and have no choice — a document never
records which type version it was written against, so version dispatch is
impossible.* **That rule stands.** Read the new field, or if absent the old one,
remains the technique.

**What changes is that the impossibility is no longer the reason.** Field
tolerance survives on its own merits — it is simpler, it does not break when a
version string is wrong or missing, and it degrades well. `recorded_under` is for
**a person reading history and a migration doing one deliberate pass**, not for a
consumer branching at read time. *A tool that starts dispatching on it has taken
a shortcut this field was not offered for.*

**It generalises**, and is not generalised here. Audits, decisions and
retirements have the same blind spot and would want the same field; adding it to
one type to see whether it earns its keep is cheaper than adding it to four.

## Status is derived, never stored

**`resolved_at` absent means open.** There is no `status` field, for the same
reason an audit has none: a stored status is a thing somebody has to remember to
update, and the moment it disagrees with the record it is worse than absent.

## Time is the substance of an incident

**Three timestamps, and only one is ever exact.** `detected_at` is knowable to
the second. `began_at` is usually inferred afterwards from logs or from a
customer report, and **an estimate presented as a measurement is the most common
lie in an incident record** — mark it in the body. `resolved_at` is knowable but
argued about, because *resolved* and *mitigated* are different and people
conflate them under pressure.

Everything else — duration, time to detect, time to resolve — is derived. Do not
store what subtraction can answer.
