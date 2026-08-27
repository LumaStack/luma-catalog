# Incident template — data breach

Copy the blocks to `.luma/records/incidents/INC-NNNN-<slug>.md`. **Copy the
blocks, not this file.** For data reaching somebody who should not have it.

> **A clock starts when you detect this, not when you confirm it.** The
> notification section is in this template rather than tracked elsewhere, because
> a missed deadline is the specific failure this record exists to prevent.

## Frontmatter

```yaml
---
type: incident
incident_id: INC-0000
kind: KIND
severity: sev1 | sev2 | sev3 | sev4
detected_at: YYYY-MM-DDTHH:MM:SSZ    # when somebody first knew. Exact
began_at: YYYY-MM-DDTHH:MM:SSZ       # usually an estimate — say so in the body
# resolved_at: YYYY-MM-DDTHH:MM:SSZ  absent means open
detected_by: human:<id> | agent:<model> | process:<tool>
responders: [human:<id>, ...]
impact: <who or what was affected, one line>
created_under: <namespace>/incident-records <version>   # luma-foreman bundle show incident-records
data_categories: [<what kind of data — be specific, not "user data">]
records_affected: <count, or a bounded estimate. "Unknown" is an answer>
jurisdictions: [<where the affected people are, not where you are>]
notification_due: YYYY-MM-DD          # the earliest deadline across jurisdictions
# notified_at: YYYY-MM-DD             absent means outstanding
---
```

## Body

```markdown
# INC-0000: <what was exposed>

## What happened

<One paragraph a stranger can follow. No jargon that needs this team to decode.>

## Timeline

<What was seen, believed, tried, and ruled out — in order, with times. Include
the wrong hypotheses. A timeline that jumps to the answer hides the thing worth
fixing.

Mark estimates as estimates. `began_at ~03:10 (inferred from the first failed
health check)` is honest; a bare timestamp is not.>

## Impact

<Who was affected and how. If the answer is nobody, say so plainly — that is a
real and useful finding, not an empty section.>

## Detection

<How this was noticed, and how long after it began. If a person noticed before a
check did, that is the most important sentence in the record.>

## What is being done

<Immediate mitigation, then the cause. Obligations this created — notifications,
rotations, fixes, a postmortem — are tracked where work is tracked and cited by
`INC-NNNN`, not ticked off here.>

## What data, and whose

<Categories and counts. **Specific beats reassuring** — "email addresses and
hashed passwords for 4,102 accounts" is a record; "some user data" is not.

Where a count is an estimate, give the bound and how you got it.>

## Jurisdictions and the clock

<Where the affected people are — **their location decides the deadline, not
yours.** One incident can carry several clocks; record the earliest as
`notification_due` and list the rest here.

| jurisdiction | who must be told | by when | done |
|---|---|---|---|
| | | | |

**An outstanding row here is an obligation somebody owes.** It does not close
because the technical fix shipped.>

## Containment

<What stopped it, and when. Whether the exposure is ongoing.>
```
