---
type: bundle
version: 0.1.0
published: 2026-08-20
consumers: [project, organization]
entry_point: policy/session-continuity
description: Ending an agent session without losing what it learned — checkpoint while working, hand off to a successor, or close for good, each writing for a different reader.
---

# Session manager

An agent session ends and takes its context with it. What survives is whatever
somebody wrote down — and by default that is a summary, which keeps conclusions
and quietly discards the expensive part: **what was already tried and did not
work.**

Three ways to end one, and **the only thing separating them is who reads what you
leave behind, and when.**

| | means | reader |
| --- | --- | --- |
| [[session-checkpoint]] | *continue here* | you, minutes later |
| [[session-handoff]] | *continue somewhere else* | a named successor, soon |
| [[session-close]] | *we are done* | a stranger, at an unknown time |

[[session-resume]] is the arriving side, and the only thing that ever deletes a
note.

## What is here

**Policy**

- [[session-continuity]] — the three endings, the note invariant, and the
  confidence rule. Read first.
- [[where-knowledge-goes]] — how to find the durable home for something,
  without this bundle containing the list.

**Workflows**

- [[session-checkpoint]] — snapshot and keep working.
- [[session-handoff]] — transfer to a named successor.
- [[session-close]] — wind down, apply what was learned, leave nothing behind.
- [[session-resume]] — pick up what another session left, and destroy it.

**Concept** — [[future-hooks]], what this would use if it existed.

**Type** — [[session_note]] · **Template** —
[a session note](templates/session-note.md)

## The four ideas worth knowing before reading further

**A note is a pointer, never the only copy.** Anything in a session note that
would hurt to lose means an earlier step was skipped. That is what makes notes
safe to delete routinely — and deleting them is what keeps them from going
stale and being believed.

**Confirmed earns a durable home; believed stays in the note.** A mid-session
learning is often a hypothesis that gets falsified an hour later, and writing it
into an append-only record commits the project to something you were wrong
about. A successor inherits everything you write with no way to tell tested from
assumed.

**The routing table is what the project adopted.** This bundle carries a
procedure, not a list of destinations, because the list is different in every
repository — and a hardcoded one would look authoritative while being wrong.
Each adopted bundle already declares where its own kind of knowledge lives, so
`adopted.toml` answers the question.

**Cost is a constraint, not a footnote.** These workflows run inside the context
they are protecting. A checkpoint that costs more than it saves has done harm,
which is why it has a budget, a stopping rule, and permission to defer anything
ambiguous rather than ask.

## Handoff and close are not the same workflow

The distinction most likely to be argued with, so: **handoff builds for a
successor; close builds for nobody.**

Handoff knows who is next and produces things aimed at them — a note in their
idiom, a prompt to paste, context tailored to what they will and will not
already have. Close has nobody to aim at, so everything it produces has to stand
on its own in the repository, and its effort goes into shutting things down
rather than setting them up.

Two consequences follow. **Close gets the strongest exit test** — *could someone
with only this repository pick this up?* — which the other two cannot pass and do
not need to. And **close cannot leave the mess a handoff can**: a handoff may
pass over a running process with an explanation, because there is somebody to
explain it to.

## Close is where the practice improves

It is the only one of the three that sees the whole arc — checkpoint is
mid-flight, handoff is aimed forward. So the retrospective lives there, and so
does applying what came out of it: **fix it now if there is time, and queue it as
work rather than as an observation if there is not.**

It is also the step most likely to be skipped, because the session is ending and
everybody wants to leave.

## What it hooks into, and what it waits for

**Wired to what exists**; everything else is named in [[future-hooks]] with its
fallback and the signal that the gap has closed — session configuration, a
logging bundle, memory tooling, `luma-foreman where <kind>`.

That file shrinking is the measure of progress here. One that never shrinks is a
wish list.

**The largest known hole: compaction is usually unannounced**, and
[[session-checkpoint]] has to be remembered. Insurance you have to remember to
buy is not insurance, and no host agent currently exposes a hook that would fix
it.

## Consumers

Both levels. Sessions happen in projects; how a session should end is the kind
of thing an organization has an opinion about, and `.luma/config/` will
eventually let it hold one.

## Version

`0.1.0`. **Nothing here has been run.** The reasoning is drawn from real losses
— dead ends re-run after a compaction, learnings recorded and never applied,
notes found months later and believed — but the workflows themselves are
untested.

**The boundary between handoff and close is the thing most likely to move.**
They share most of their steps and differ in who reads the result, and it will
take a few real sessions to know whether that difference earns two workflows or
one with a switch. The case for two is that they were argued from genuinely
different situations rather than from symmetry.

This bundle is also the catalog's **first `concept`**, used deliberately:
whether that type survives is an open question in the format, and it will not be
settled by anybody reasoning about it further.
