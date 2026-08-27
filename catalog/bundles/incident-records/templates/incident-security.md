# Incident template — security

Copy the blocks to `.luma/records/incidents/INC-NNNN-<slug>.md`. **Copy the
blocks, not this file.** For unauthorized access, a leaked credential, or a
compromised account **where nothing left**.

> **If anything was exfiltrated, use the data-breach template instead.** When it
> is unknown — and early it usually is — **use data-breach.** It carries a
> notification clock this one does not, and downgrading later is cheap.

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
created_using: <namespace>/incident-records <version>   # luma-foreman bundle show incident-records
vector: <how access was gained>
access_gained: <what the access allowed>
exfiltration: none | unknown | some   # `some` means this is the wrong template
rotated_at: YYYY-MM-DDTHH:MM:SSZ      # when credentials were actually rotated
---
```

## Body

```markdown
# INC-0000: <what was compromised>

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

## Vector and access

<How it was gained, and what it allowed once gained. Be specific about the
blast radius: what *could* have been reached, not only what was.>

## Rotation

<What was rotated and when — a time, not "immediately". **The window between
compromise and rotation is the number this record exists to capture.**>

## Exfiltration

<What left, or the evidence that nothing did. **"No evidence of exfiltration" and
"evidence of no exfiltration" are different claims** — say which one you have.>
```
