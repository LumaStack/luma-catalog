---
type: bundle
version: 0.1.0
published: 2026-08-20
consumers: [project, organization]
entry_point: policy/capturing-ideas
description: Ideas as individual files rather than one growing IDEAS.md — what earns a file, how capture stays fast, and how the list gets tended rather than accumulating.
---

# Backlog ideas

One file per idea, in `.luma/backlog/ideas/`, instead of a single `IDEAS.md`
that grows until nobody opens it.

**The goal is a list of mostly good ideas, not a record of every thought anyone
had.** Everything here serves that: a test for what earns a file, a capture path
fast enough not to interrupt the work that produced the idea, and a gardening
session that prunes.

## What is here

**Policy**

- [[capturing-ideas]] — the three-part test, what disqualifies an idea, and why
  evaluation is deliberately deferred. Read first.
- [[where-an-idea-lives]] — project, department or organization, and the default.
- [[tending-ideas]] — growth stages, when to prune, archive versus delete.

**Workflows**

- [[capture-idea]] — write, ask for more, check duplicates, *then* ask how much
  detail is wanted.
- [[tend-ideas]] — the gardening session.
- [[migrate-ideas]] — move an existing `IDEAS.md` across, once.

**Template** — [an idea](templates/idea.md)

## Three ideas worth knowing before reading further

**Capture, then check.** Writing comes first because that is what is lost.
Searching for duplicates first interrupts the run of ideas and usually finds
nothing — so it is step three, and merging is proposed rather than performed.

**`originated` answers *was a person involved*, not *who typed it*.** Agents
write up almost everything; attribution by authorship would mark every idea as
the agent's and destroy the only signal that matters. An `agent:` origin means
**no human has looked at this yet** — a state somebody can search for.

**Growth stages reuse `lifecycle_status`.** Seedling is `draft`, budding is
`provisional`, evergreen is `stable`, pruned is `archived`. No second vocabulary
for a ladder the format already has.

## Archive freely; delete carefully

Archiving needs nobody's permission. **Deleting somebody else's idea needs
theirs**, and an agent should never delete one it did not originate. How long
archived ideas are kept will become a setting, because some organizations will
keep everything forever and be right to — the `archived` date is the clock it
will measure from.

## What this cannot do yet

Three gaps, recorded rather than worked around, because each needs something
that does not exist.

**A graduated idea has nowhere to go.** When one becomes real work, the honest
destination is a backlog item. For now it stays here marked `stable` and
somebody remembers, which is not good enough.

**Nothing says when an idea stops being one.** Length is the symptom, not the
trigger, and the actual trigger needs the backlog tool to answer.

**Rejected and expired look identical.** Both are `archived`. That is the same
gap the decision type records, and it should be solved once for both.

## Provisional, and honestly so

**This exists because ideas are being lost while a proper backlog tool is
half-built.** It may be replaced by that tool, absorbed into it, or survive
beside it as the simpler option for projects that want files rather than a tool.

Which of those happens is genuinely unknown, and it is too early to decide. What
is not in doubt is that a single growing `IDEAS.md` does not scale, which is
enough reason for this to exist now.

## Consumers

Both levels. An organization has ideas about how it works; a project has ideas
about what it builds. The same shape holds, and `scope` records which.

## Version

`0.1.0`. The capture path is drawn from established practice — capture widely,
judge later, prune deliberately — but **nothing here has been run on a real
backlog**, and the cadence for tending is deliberately undefined until a few
sessions have been done by hand.
