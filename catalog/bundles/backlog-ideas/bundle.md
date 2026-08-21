---
type: bundle
version: 0.4.0
published: 2026-08-20
consumers: [project, organization]
entry_point: policy/capturing-ideas
description: Ideas as individual files rather than one growing IDEAS.md — what earns a file, how capture stays fast, and how the list gets tended rather than accumulating.
---

# Backlog ideas

One file per idea — preferably in `.luma/backlog/ideas/`, and anywhere
consistent when luma is not installed — instead of a single `IDEAS.md` that
grows until nobody opens it.

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

**Templates** — [an idea](templates/idea.md) · [an idea review](templates/idea-review.md)

## Three ideas worth knowing before reading further

**Capture, then check.** Writing comes first because that is what is lost.
Searching for duplicates first interrupts the run of ideas and usually finds
nothing — so it is step three, and merging is proposed rather than performed.

**`contributors` is everyone actively in the exchange** — human and agent alike,
whoever suggested it and whoever wrote it down. Both count, and apportioning who
did more is a judgement nobody can make reliably.

**No human in `contributors` is the signal.** A session being open is not a
human being present: auto mode with nobody reading, or a subprocess whose output
never surfaced, is nobody there whatever the session claims. The test from an
agent's side is mechanical — *did I put this in front of them and get a reply?*
— which is what makes proposing before filing load-bearing rather than
courteous.

**Confirmation is separate, and open to agents.** `verified` records whoever
read an idea afterwards and vouched for it. An agent overseeing another agent's
work is real and worth recording, and is still not a human having seen it.

**Almost everything reuses a core field.** Growth stages are `lifecycle_status`
— seedling `draft`, budding `provisional`, evergreen `stable`, pruned
`archived`. Dates and authorship are `created`. Human review is `verified`. The
type declares only `horizon`, `scope` and `archived`, because those are the
three things the format genuinely does not have.

## It prefers `.luma/`, and does not require it

The backlog tier is the right home, but **not every repository has luma
installed and an idea still has to go somewhere.** What the practice actually
needs is one file per idea in one consistent place, with frontmatter — none of
which depends on the path.

**Never create `.luma/` in a repository that has not adopted it.** Filing an
idea is not a reason to bring a directory structure into somebody's project.

## Archive freely; delete carefully

Archiving needs nobody's permission. **Deleting somebody else's idea needs
theirs**, and an agent should never delete one it did not originate. How long
archived ideas are kept will become a setting, because some organizations will
keep everything forever and be right to — the `archived` date is the clock it
will measure from.

## What this cannot do yet

Three gaps, recorded rather than worked around, because each needs something
that does not exist.

**A graduated idea has nowhere to go yet.** The destination is settled — a
`stable` idea leans towards the proper backlog unless it is one of the kinds
that stay ideas, which are named. What is missing is the backlog. Until there
is one, such an idea stays here marked `stable` and somebody remembers, which
is not good enough.

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

`0.4.0` — what a messy `IDEAS.md` actually contains, and what to do about each
shape; new content, existing use unaffected.

**The governing rule is *surface, do not resolve*.** Every shape in that table is
a place an agent could quietly decide and produce something that looks clean —
reconstructing a dead entry, merging two that disagree, flattening an order that
meant something. Clean is not the goal. Nothing lost and nothing invented is the
goal, and a mess reported honestly beats a tidy file nobody agreed to.

`0.3.0` — `migrate-ideas` reads the headquarters declaration before inferring
anything, and takes the project list from the headquarters index where one
exists; new content, existing use unaffected.

**A fresh agent got this wrong on its first run**, concluding that a
similarly-named engine repository was the headquarters. The declaration it needed
was written by `create-internal-hq` and sitting unread. Reading it first is not a
replacement for asking — an organization with no headquarters yet is an ordinary
case — but a declaration beats a directory listing wherever one exists.

**The index is the better source for a different reason: it knows about
repositories that are not checked out.** Sibling-directory discovery can only
find what somebody happened to clone, so it does not merely produce a worse list
— it produces one that is silently incomplete and looks finished. The index also
carries `attention` and `in_scope`, which are routing signal nothing on disk
has.

**Step 3 also settles the denominator before the review starts.** The same test
run found sixteen reviewable ideas inside eight headings and had to raise it
unprompted — a heading is not necessarily a unit of thought.
Agreeing the count first keeps *3 of 8* meaningful and keeps the question away
from the middle of a content decision.

`0.2.0` — everything learned from the first real migration is new content;
existing use is unaffected. What counts as signoff. How briefly to report, and
where. A review template, because the shape drifted between the first idea and
the twelfth. Two triage tests — a topic is not an idea, and settled is *already
happened* however long the entry. `horizon` decided rather than defaulted.
Combining `contributors` when one idea absorbs another. A breakdown table with a
`Modifications` column. And the routing rules in [[where-an-idea-lives]], which
had scope but nothing about choosing between repositories.

**It was written after `migrate-ideas` failed twice in one session, both times by
appearing to work.** The agent recommended a destination and filed the idea in the
same turn; and separately, read agreement about the *process* as agreement about
an *idea*. Neither raised an error, and both replaced the user's judgement with
the agent's while looking collaborative. The mode table said "decide jointly" and
said nothing about what deciding looks like.

`0.1.0`. The capture path is drawn from established practice — capture widely,
judge later, prune deliberately — but **nothing here has been run on a real
backlog**, and the cadence for tending is deliberately undefined until a few
sessions have been done by hand.
