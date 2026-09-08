---
type: luma/idea
title: Violations — when agents do not behave the way we want them to
created: { by: human:benlinton, at: 2026-09-08T03:12:00Z }
contributors: [human:benlinton, agent:claude-opus-5]
horizon: next
scope: project
stage: draft
---

# Violations — when agents do not behave the way we want them to

**`.luma/records/violations/`, working like incidents and weighing far less.**
**There should be a lot of them** — that is the design rather than a concession
— and they exist to improve policy and procedure governance rather than to be
investigated one at a time.

## What each one is

**A violation is a breach of policy.** An incident is when something **broke or
was compromised in the real world**, outside of a session.

That is the discriminator, and it is cleaner than severity: a violation happens
*inside* the work, and an incident happens *to* something.

**Policy here includes what was wanted and never written down.** An agent can
behave wrongly against an expectation that exists only in somebody's head, and
that is still a violation — one whose remedy is a rule rather than a correction.
This is where it parts from `incident-records`' `ai-policy-breach` kind, which
asks *which policy was violated* and assumes a document to cite.

## Three answers, three different remedies

The `ai-policy-breach` template already asks *was the policy ever in front of the
agent?* and calls it *often the real finding*. Widening the subject adds a third
answer, and it is the most valuable one:

┌─────────────────────────────────────┬──────────────┬─────────────────────────────────────────────┐
│            what was true            │ what failed  │                   remedy                    │
├─────────────────────────────────────┼──────────────┼─────────────────────────────────────────────┤
│ policy existed and was delivered    │ the agent    │ correction, or the rule can't hold as prose │
├─────────────────────────────────────┼──────────────┼─────────────────────────────────────────────┤
│ policy existed and wasn't delivered │ the delivery │ adoption, routing, matches                  │
├─────────────────────────────────────┼──────────────┼─────────────────────────────────────────────┤
│ no policy existed                   │ nothing yet  │ write the rule                              │
└─────────────────────────────────────┴──────────────┴─────────────────────────────────────────────┘

**The third row is why this is not just a lighter incident.** A violation with
nothing to cite says *we want something we never wrote down*, and no register
that requires a `policy_violated` field can record it.

## Relationship to incidents

**A violation might result in an incident. Most incidents have nothing to do
with a violation.** Hardware fails, a credential leaks, an upgrade goes wrong,
somebody is attacked — none of those is an agent breaching a policy, and the
incident register exists for all of them.

So this is not a severity floor beneath incidents and not a lighter kind of one.
**They are different registers that occasionally connect**, and the arrow runs
one way and rarely.

Keeping them apart is also what keeps the incident register heavy enough to be
worth reading. Filing four routine violations an afternoon as `sev`-graded
incidents, with responders and an impact line, would empty the word out.

## The signal is in the aggregate

**One agent skipping one step is noise. The same step skipped forty times is a
procedure that does not work**, and no individual record would ever say so.
Governance is the output — which rules are followed, which are ignored, and
which turn out to be unwritable as prose at all.

## The evidence this already happens

One session of `luma-backlog` on 2026-09-07/08 produced four, by an agent that
had the rules in context throughout:

- a new policy wikilinked outside its own bundle, breaking self-containment
- a procedure named an internal package, which its own bundle forbids
- a policy was paraphrased until it drifted, promoting an example into a claim
- the agent asked for a criterion one turn after recording that asking for one
  gets in the way

**The fourth had no policy to cite** — it was an expectation stated in
conversation minutes earlier. Under a policy-citing register it is not
recordable, and it is the most interesting of the four.

**All were caught by a human reading every turn. Nothing mechanical caught any
of them**, and all four are now buried in one work item's journal where nothing
can count them.

## Open

- **Who files one.** An agent recording its own is the only version that scales,
  and is also self-reporting — the ones it does not notice are exactly the ones
  that matter.
- **What closes one.** An incident resolves; a violation may simply be counted.
  If nothing ever closes, the register grows forever and wants a retention
  answer rather than a lifecycle.
- **Whether severity applies at all**, or whether counting is the only measure a
  violation needs.
- **`created_using` applies here too** — the incident type notes the field
  *generalises* to audits, decisions and retirements, and this has the same
  blind spot.
