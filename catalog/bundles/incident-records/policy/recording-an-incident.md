---
type: policy
title: Recording an incident
description: What counts as an incident, the four kinds and what each one owes, and why an outage and a data breach must not be recorded on the same form.
matches:
  - topic: recording an incident, an outage, a breach or a policy violation
---

# Recording an incident

**One place, several shapes.** Every incident is `INC-` numbered and lands in the
project's records. What each one *contains* depends on what happened, and
flattening that would lose the fields that make a record worth keeping.

## What is an incident, and what is not

**An incident is something that went wrong in the world** — service was lost,
data was exposed, a rule was violated, a credential leaked. It already happened.

**A finding is not an incident.** An audit finding says something *could* go
wrong or is wrong in the abstract. A failing check is not one either. The line is
whether harm reached anybody: *this policy is stale* is a finding; *an agent
followed the stale policy and published the result* is an incident.

**A near miss is worth recording as one**, at low severity, because the only
difference between it and the real thing is luck and you will want the record
when luck runs out.

## Severity is about harm that reached the world

**Not urgency, not effort, not how loud the day was.**

| | means |
| --- | --- |
| **`sev1`** | harm reached people outside the organization and cannot be undone |
| **`sev2`** | harm reached them and is recoverable, or reached everybody inside |
| **`sev3`** | contained before it left the team, or affected a subset internally |
| **`sev4`** | a near miss. Nothing was harmed and only the mechanism failed |

**Grade it by what happened, not by what could have happened.** *It could have
been sev1* belongs in the body — it is the most useful sentence in most records
and the worst possible severity field.

## The four kinds, and what each one owes

**Shared by all four**, and identical in every template because they answer the
same question about any incident: what happened, the timeline, impact, detection,
and what is being done.

| kind | owes, beyond the shared sections |
| --- | --- |
| **`outage`** | the services affected, customer-facing duration separate from total duration, and whether it was self-inflicted (a deploy, a config change) or external |
| **`security`** | the vector, what access was gained, what was rotated and when, and whether anything was exfiltrated — **which is what separates it from `data-breach`** |
| **`data-breach`** | data categories, record counts, the jurisdictions reached, and the **notification clock** — who must be told, by when, and whether they were |
| **`ai-policy-breach`** | the model and the agent, the policy violated, whether the output was published or acted on, and **whether the policy was ever delivered to the agent** |

### `security` and `data-breach` are different records on purpose

**A compromised credential with nothing exfiltrated is a `security` incident.**
The moment data left, it is a `data-breach`, and a legal clock starts that the
security form has no field for. **Recording the second as the first is how a
notification deadline gets missed** — not through malice, but because the form
never asked.

### `ai-policy-breach` asks one question the others do not

**Was the policy ever in front of the agent?** An agent that violated a rule it
was never given has not failed — **the delivery has**, and the fix is adoption or
`matches`, not correction. An agent that violated a rule it was holding is a
different incident with a different remedy.

**Nothing else in this bundle asks a question whose answer can exonerate the
actor entirely**, which is why it is a field rather than a paragraph somebody
might omit.

## Why the shared sections are duplicated, not factored out

**Every template is complete and copied whole.** The shared sections are
byte-identical across all four rather than living in one place the others
reference.

**Templates are for copying, and DRY is the wrong optimisation for them.** An
author under incident pressure should copy exactly one file and fill it in — not
assemble two, and not discover halfway that a section they need is somewhere
else. *The duplication is a cost paid by whoever edits the templates, which is
rare, to spare whoever uses them, which is exactly when nobody has attention to
spare.*

**When you change a shared section, change it in all four.** That is the price,
and it is stated here so that finding four copies is not a surprise.

## The record is append-only, and it lands in the project's records

**`.luma/records/incidents/`**, or wherever this project keeps records — **never
in a bundle.** A bundle is copied into every adopter and a vendored copy cannot
be edited in place, so a record there could never be corrected.

**Write the timeline as it is known and correct it by appending.** An incident
record is read by people reconstructing a bad day, and a silently amended
timeline is worse than an incomplete one.
