# Incident template — outage

Copy the blocks to `.luma/records/incidents/INC-NNNN-<slug>.md`. **Copy the
blocks, not this file.** For something unavailable or degraded.

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
recorded_under: lumastack/luma-catalog/incident-records 0.1.0
services: [<what was down or degraded>]
customer_facing_duration: <how long users felt it — often shorter than the total>
trigger: self-inflicted | external
---
```

## Body

```markdown
# INC-0000: <what was down>

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

## Services and duration

<What was affected and for how long. **Total duration and customer-facing
duration are different numbers** and reporting only the first overstates the
harm while hiding how long detection took.>

## Self-inflicted or not

<A deploy, a config change, a dependency, a provider. **Most outages are
self-inflicted and recording that honestly is what makes the trend visible** —
a record set that blames providers for everything is a record set nobody has
read.>
```
