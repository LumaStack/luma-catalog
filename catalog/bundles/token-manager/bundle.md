---
type: bundle
version: 0.3.0
published: 2026-08-24
consumers: [project, organization]
entry_point: workflows/token-tutorial/token-tutorial
description: Where an agent session's tokens actually go — a paced tutorial on the mechanism and the fixes that follow from it, and an audit that measures a real setup instead of guessing at it.
---

# Token manager

**People run out of tokens and conclude they asked for too much.** Almost always
they did not. The model has no memory, so every turn resends the entire
conversation from the top — and what the human typed turns out to be a rounding
error next to the agent re-reading things it was already sent.

That single fact reorders everything. It makes the cheapest fix free and five
letters long, and it makes the move people reach for when they are trying to save
money — switching to a smaller model mid-session — the most expensive keystroke
available to them.

## What is here

**Workflows**

- [[token-tutorial]] — the mechanism and what follows from it, presented a step
  at a time with a pause after each, ending in a quiz.
- [[token-audit]] — measures one real setup and reports what is costing what.
  Changes nothing.

**Types** — [[tutorial_step]] · [[tutorial_quiz]], both vendored from
`luma/luma-types` rather than invented here. They describe any paced walkthrough,
not this one, and the next tutorial takes the same copies.

The tutorial carries its steps beside it as documents of those types, read one
at a time and never all at once — both the cheap way to run a tutorial and the
only way this particular tutorial can run without contradicting itself.

**`tutorial_step` exists for one field.** A step declares whether the reader can
act on it here, must go elsewhere, or has nothing to act on at all, because
several of the recommendations would destroy the session delivering them and the
reader has no way to tell which. That is a behaviour a consumer dispatches on,
which is what earns a type rather than a label.

## Measure first, then learn what to do about it

**The workflows answer different questions, and the order matters.** *What is
wrong with my setup* is answered by numbers from your own machine; *what should I
do about it* is answered by the tutorial. Run the audit first and the tutorial
stops being general advice and starts being a ranked list of your own problems —
which is why the tutorial sends you to the audit near the start, before it has
recommended anything.

Going the other way round works too, just less well. You learn the mechanism, and
then have to guess which consequence of it is biting you.

## Nothing here changes a setting

The audit measures and reports; it edits no file and flips no switch. The
tutorial explains and waits; it applies nothing on the reader's behalf.

**That is deliberate, and it is not caution.** Every fix in here is a trade
against something the person actually wants — the tools they connected, the
schedule they chose, the model they prefer — and a bundle that quietly turned
those off would be optimising a number nobody asked it to optimise. The reader
makes the trade. This bundle makes sure they can see it.

## The numbers in here have a shelf life

Token costs, cache lifetimes, which servers are expensive, whether tool deferral
is on by default: all of it moves, and some of it has moved since these
workflows were written. The figures are here because a claim with a number
attached is one somebody can check, and a claim without one is one nobody ever
tests.

**So the mechanism is what to trust, and the figures are illustration.** If a
number here disagrees with what `/context` and `/usage` say on the machine in
front of you, the machine is right — and the tutorial ends by pointing at those
meters for exactly that reason.

**The same split applies to the harness.** Both workflows are written for Claude
Code and name its commands directly. The reasoning holds anywhere — no memory,
everything resent each turn, a cache a model switch invalidates — while the
keystrokes are between renamed and absent elsewhere. The tutorial says so before
its first step rather than letting somebody discover it at a command that does
not exist.

## Consumers

Both levels, because the fixes split across them. The output-filtering hook, the
memory files and the set of connected servers belong to a repository. The habits
— clear between jobs, choose the model once, check what fires overnight — are the
kind of thing an organization has an opinion about once rather than every person
rediscovering at their own expense.

## Version

`0.3.0` — the tutorial types moved to `luma/luma-types` and are vendored back.
They are now `luma/tutorial_step` and `luma/tutorial_quiz`, and every step and the
quiz declare the namespaced names.

**Because they were never token-specific.** They describe a paced walkthrough,
and this bundle happens to be the first one. Left here, the second tutorial would
either link across bundles — which breaks self-containment — or declare its own
`step` under a different name, and both copies would validate cleanly while
meaning subtly different things. That is the failure that is invisible until
somebody has to reconcile them.

**Breaking, and shipped as a minor under the `0.y.z` permission.** Anything
dispatching on the un-namespaced `tutorial_step` must now match
`luma/tutorial_step`. No deprecation cycle, because nothing uses the old names —
they were published hours ago and this bundle has no adopters. Saying that
plainly is the condition on taking the exception; a dead name kept to protect
nobody would be worse.

`0.2.0` — the tutorial's steps became documents. They were assets with no
frontmatter; they are now [[tutorial_step]] and [[tutorial_quiz]], and the
walkthrough reads the same.

**The change worth knowing about is where the pause kind lives.** It was a column
in the workflow's running order and is now a `pause` field on each step. That
removes the copy that could drift, and it puts the answer in the document the
agent is already reading at the moment it needs it — rather than in a table it
has to look back at, one step removed from the thing being described.

**They are steps now, not screens.** The reader is walked through steps; *screen*
survives only as the sizing rule an author writes against, in [[tutorial_step]].
The directory moved with the word, so every Document ID under it changed from
`.../screens/…` to `.../steps/…`. Wikilinks address the slug alone and are
unaffected; anything referring to a full ID is not.

**Minor rather than patch**, because an adopter reading the running order for the
pause kind will no longer find it there, and because those IDs moved. Nothing
they must fix, so not major: re-adopt and it works.

`0.1.0`. **Untested as a walkthrough.** The material is drawn from real session
logs and holds up, but nobody has yet sat through the paced version of it, and
pacing is the thing most likely to be wrong: the steps may be too small, the
pause may come to feel like ceremony, and the *apply* offers on the middle
steps may interrupt more than they help.

**The split between what to do and what not to do is the structural bet.** It
reads well and it duplicates one idea across the halves — choosing a model at the
start and not switching mid-session are the same fact told twice. That is
defensible while the second half is where the surprises live, and it is the first
thing to collapse if the tutorial turns out to run long.
