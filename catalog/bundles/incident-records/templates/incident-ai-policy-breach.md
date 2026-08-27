# Incident template — AI policy breach

Copy the blocks to `.luma/records/incidents/INC-NNNN-<slug>.md`. **Copy the
blocks, not this file.** For a model or agent that violated a policy.

> **This template asks one question the others do not: was the policy ever in
> front of the agent?** An agent that violated a rule it was never given has not
> failed — the delivery has, and the remedy is adoption or `matches`, not
> correction.

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
model: <the model, exactly — including version>
agent: <the agent or harness, if not the model directly>
policy_violated: <the document, by id or path>
policy_was_delivered: yes | no | unknown   # see below. Often the real finding
output_acted_on: yes | no | partially      # did anything downstream consume it
---
```

## Body

```markdown
# INC-0000: <what the agent did>

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

## What the policy said, and what happened instead

<Quote the rule. Then what was actually done. **Keep them adjacent** — a reader
should not have to open the policy to judge the gap.>

## Was the policy delivered?

<**The question that decides whose failure this is.**

- **Delivered and violated** — the agent held the rule and did not follow it.
  The remedy is the agent, the prompt, or a check.
- **Not delivered** — the bundle was not adopted, or nothing surfaced the
  document. **This is a delivery failure wearing an agent's clothes**, and
  fixing the agent fixes nothing.
- **Unknown** — say so. It is common and worth recording as a gap in its own
  right: a project that cannot tell what its agents were holding has a bigger
  problem than this incident.>

## What consumed the output

<Was it published, merged, sent, acted on? **An unreviewed output that nobody
used is a near miss; one that shipped is the incident.** Say where it went and
what was done to retract it.>

## Whether a check could have caught it

<And if one exists, why it did not fire. **A policy with no check behind it is a
rule that depends on attention**, which is what this record is evidence
about.>
```
