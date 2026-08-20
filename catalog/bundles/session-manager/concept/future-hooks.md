---
type: concept
title: Hooks into tools that do not exist yet
description: What this bundle would use if it existed, what it does instead today, and how to tell when each gap has closed. Read before adding a workaround.
---

# Hooks into tools that do not exist yet

**This bundle is wired to what exists.** Everything else is here, named, with the
fallback written down — so that a workaround is a recorded decision rather than
something somebody improvises and forgets.

Each entry says: **what is wanted**, **what happens today**, and **the signal**
that the gap has closed. The signal matters most. A dependency nobody is
watching for is one that arrives and gets used six months late.

## Session configuration

**Wanted.** `.luma/config/sessions.toml`, mapping a kind of knowledge to the
bundle that owns it, overriding the defaults in [[where-knowledge-goes]].

```toml
[knowledge]
log      = "luma/logging"
decision = "acme/architecture-decisions"
```

**Today.** The workflows check `.luma/config/` and fall through. The defaults
carry every case, which is correct for now — nothing has adopted anything, so
there is nothing to override.

**Signal.** Any project needing a destination the defaults get wrong. That is the
first real evidence about what the schema should hold, and it is worth waiting
for rather than guessing.

## A logging bundle, and a journaling bundle

**Wanted.** `luma/logging` and `luma/journaling`, each owning its format,
location and cadence. The workflows would find the bundle and do what it says.

**Today.** Both are conditional on being *established*, by the detection rule in
[[where-knowledge-goes]], and neither exists — so in practice both steps are
skipped everywhere.

**This is the right failure.** A session workflow inventing a log format would
be one bundle deciding another's business, and every project would get a
slightly different invented format depending on which agent ran first.

**Signal.** Somebody wanting a work log badly enough to define one. Then it is a
bundle, and this routes to it.

## A backlog tool

**Wanted.** Somewhere for unfinished work to go at [[session-close]] that is not
an idea. *Half-built, worth finishing* is a backlog item; filing it as an idea
overstates how speculative it is.

**Today.** It becomes an idea with a note saying it is further along than that,
or it is recorded as deliberately abandoned. Both are honest and neither is
right.

**Signal.** The backlog tool that `luma/backlog-ideas` is already waiting on.
One arrival closes both gaps.

## Memory tooling

**Wanted.** A luma-owned memory store, so *what is true of this operator*
survives a change of agent. Today's memories live in one agent's format and are
invisible to every other.

**Today.** Write in the running agent's own format and follow its own index
conventions, then **name in the session note where they went** — which is the
whole mitigation, and a thin one.

**Signal.** Foreman growing memory as a projection target. When it does, the
luma store becomes the destination and the agent-specific store becomes
generated output — the same relationship `CLAUDE.md` already has to `.luma/`.

## `luma-foreman where <kind>`

**Wanted.** The resolution order in [[where-knowledge-goes]] as a command, since
foreman is the thing that knows what a project adopted. Four steps of prose
become one call that is the same every time.

**Today.** The agent runs the procedure by hand, which costs context on every
routing decision and produces slightly different answers on different days.

**Signal.** Foreman's routing question settling — whether routing is prose or
data. That decision is open and this depends on it, so this waits.

## Automatic checkpointing

**Wanted.** A checkpoint fired by something other than remembering to —
elapsed time, context pressure, or a hook before an irreversible command.

**Today.** [[session-checkpoint]] is invoked by hand, which is a real weakness:
**compaction is usually unannounced**, and insurance you have to remember to buy
is not insurance. It is the largest known hole in this bundle.

**Signal.** Any host agent exposing a pre-compaction hook. Worth watching for
actively rather than waiting to stumble on.

## Adapters for other agents

**Wanted.** These four workflows available as `/session-checkpoint` and friends
in whatever agent is running, generated rather than hand-written per tool.

**Today.** Whatever the host agent does with a `workflow` document. That is the
projection problem foreman owns, and it is deliberately not solved here — a
workflow naming its harness has bound vendor-neutral knowledge to whichever
assistant happened to be current when it was written.

**Signal.** Foreman projecting workflows at all.

## What to do when one of these arrives

**Delete the workaround; do not leave both.** A fallback that stays after its
replacement lands is the more dangerous half — it still runs, it still looks
deliberate, and nothing announces that the real path exists now.

Then remove the entry from this document. **This file shrinking is the measure
of progress**, and one that never shrinks is a wish list rather than a plan.
