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
  created_using:
    field_presence: required
    field_type: text
    desc: "the bundle and version that **created** this record — `<namespace>/incident-records 0.2.0`. Written once and never changed, including by a migration"
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

## `created_using` — the version that made this record

**The bundle version that created this record, and it never changes.** Not what
the catalog published at the time, and not what is available now — **the adopted
copy that was actually read.** The vendored bundle under `.luma/bundles/` is the
one in play, so there is no ambiguity to resolve.

**It is not the type version.** What a record looks like comes from the type
*and* the kind's template, which version together as the bundle — so the bundle
is the unit, and the value carries its id so the answer survives the record being
copied out of this repository.

### Room for migrations, which do not exist yet

**Nothing migrates incident records today**, and this ships no machinery for it.
What it ships is a name that will still be true when something does.

**`created_using` means one thing and will never have to mean another.** A single
field called `bundle_version`, overwritten by each migration, would answer *which
version created this* until the first migration and then quietly stop — the worst
kind of change, because nothing announces it.

**When migrations arrive, `migrated_using` is added beside it.** That is purely
additive: consumers must not reject a document for keys they do not understand,
so a new optional field is invisible to everything that has not learned it. Minor
bump, nothing to rewrite, and no existing record becomes wrong.

*If chains of migrations turn out to be common, that field grows into a list —
also additive.* **Neither step is designed here**, because a mechanism built
before its first user is a guess with a version number.

**Git can usually answer this, and an earlier draft of this section wrongly said
it could not.** The record is committed; at that commit `adopted.toml` names the
version held. In the ordinary case the field is redundant, and *do not store what
subtraction can answer* is a rule this same document applies to durations.

**It is kept for the cases where git answers wrongly or not at all:**

- **The commit is not when the template was copied.** A record is opened during
  an incident and committed days later. If the bundle upgraded in between,
  `adopted.toml` at that commit reports **the wrong version, confidently** — and
  incidents are exactly the work where a record is drafted long before it lands.
  This is the case that makes the field a correctness measure rather than a
  convenience.
- **Records travel; history does not.** Copied into an organization's register, a
  postmortem or a report, the file survives and its git history does not.
- **A hand-copied template leaves no adoption trace.** Taken from the catalog
  directly, or from a colleague, `adopted.toml` never mentions it.
- **The cost of asking.** `git log --follow`, then `git show <sha>:…/adopted.toml`,
  then parse. Nobody does that during a review; a field is free to read.

**Record the version that ran, not the version that exists.** The adopted copy
under `.luma/bundles/` *is* what the author read — a project holding `0.1.0`
while this catalog publishes `0.3.0` used `0.1.0`, and that is the honest answer.
There is no ambiguity to resolve: the vendored copy is the one in play.

**Which is why a template cannot carry a value.** The catalog does not know what
any adopter holds, so anything pre-filled here would be wrong for somebody by
construction rather than merely stale — and `0.1.0`'s templates hardcoded a
version and were already lying one release later. The templates carry a
placeholder and name the command that reads it: `luma-foreman bundle show`.

**It must not become a version switch, and this is the part worth guarding.**
`change-a-shared-type` states the rule it appears to contradict: *tools are
field-tolerant rather than version-aware, and have no choice — a document never
records which type version it was written against, so version dispatch is
impossible.* **That rule stands.** Read the new field, or if absent the old one,
remains the technique.

**What changes is that the impossibility is no longer the reason.** Field
tolerance survives on its own merits — it is simpler, it does not break when a
version string is wrong or missing, and it degrades well. `created_using` is for
**a person reading history and a migration doing one deliberate pass**, not for a
consumer branching at read time. *A tool that starts dispatching on it has taken
a shortcut this field was not offered for.*

**Nothing may rewrite `created_using`, including a future migration.** A
migration that moves a record forward records that separately; overwriting this
field would destroy the only answer to why the record looks the way it does.

**It generalises**, and is not generalised here. Audits, decisions and
retirements have the same blind spot and would want the same field; adding it to
one type to see whether it earns its keep is cheaper than adding it to four.

**And it may not earn it.** If the drafted-late case turns out to be rare and
records never travel, git is sufficient and this field is ceremony. That is a
real possible outcome and the reason it is on one type rather than four.

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
