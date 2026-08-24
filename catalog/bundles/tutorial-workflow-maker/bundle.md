---
type: bundle
version: 0.5.0
published: 2026-08-24
consumers: [project, organization]
entry_point: policy/what-makes-a-tutorial-land
description: Making paced tutorials — the standard a walkthrough is held to, a workflow that turns source material into one, and templates for the steps, the quiz and the workflow that performs them.
---

# Tutorial workflow maker

**A tutorial is not a document somebody reads. It is something an agent performs
at a person**, one step at a time, inside a live session the material is often
about changing. That makes it a different artefact from a readme, with failures a
readme cannot have — and the failures are quiet: the tutorial runs, the reader
nods along, and nothing they were meant to change gets changed.

This bundle carries what a walkthrough is held to, the procedure for building
one, and the parts that should not be rewritten each time.

## What is here

**Policy**

- [[what-makes-a-tutorial-land]] — the rules, each naming what goes wrong without
  it. Read first.

**Workflow**

- [[create-tutorial]] — source material in, a working tutorial out.

**Templates** — [a step](templates/tutorial-step.md) ·
[a quiz](templates/tutorial-quiz.md) ·
[the driving workflow](templates/driving-workflow.md)

**Types** — [[tutorial_step]] · [[tutorial_quiz]], vendored from
`luma/luma-types`. Copy them into whatever bundle you are building a tutorial
in; the contract has to travel with the documents.

**Concept**

- [[lessons-from-the-first-tutorial]] — where the rules came from, and what is
  still untested. Read it when arguing with a rule, not while following one.

## Most of the driving workflow is already written

**The parts of a tutorial that vary are the subject, the harness, the hazards and
the running order.** Everything else — how a step is headed, what the agent says
after one, what it must never do to the session it is running in — is the format,
and the template ships it complete.

**That is the main thing this bundle is for.** A second tutorial rewording those
in its own voice is how two tutorials start behaving differently for no reason
anybody chose, and the difference is invisible until somebody runs both.

## Specify the text, or describe the goal — never confuse them

The most transferable thing learned so far, and it is why the templates look
over-specified.

**Where a tutorial has a consistent surface — a heading, an offer, a transition —
write the literal words.** An agent told to *offer to wait* composes a sentence
every time, and improvised wording is where a tutorial stops sounding like it is
talking to the reader and starts sounding like it is talking to itself.

**Where it needs judgement, describe the outcome and trust it.** Answering a
question, deciding whether something is a hazard, reading whether somebody is
lost — none of that can be scripted, and scripting it produces a worse result
than saying what good looks like.

**Getting this backwards is the standard failure.** Prose describing a heading
produces an invented one; a script for a judgement call produces an agent that
cannot handle the case the script missed.

## It is meant to be improved by being used

**[[create-tutorial]] ends by testing the tutorial and feeding general learnings
back here**, which is the only mechanism this bundle has for getting better — the
rules it carries came from running a tutorial, not from reasoning about one, and
there is no reason to expect that to change.

**The test has to happen in a clean session**, because the one that wrote the
tutorial already holds every step and will perform it flawlessly from memory. A
tutorial is written for somebody arriving with none of that, and that is the only
condition under which a gap in it appears.

**Two guards keep that from becoming noise.** It runs only for somebody who owns
the catalog this lives in, because a vendored copy is a snapshot and an
improvement to one is overwritten, unannounced, on the next adopt. And only
learnings that would have helped a *different* tutorial come back — anything
naming the subject just taught belongs in the tutorial that taught it.

**Nothing to promote is the expected answer most times.** A workflow whose last
step must produce something produces noise, and a policy that grows on every use
becomes one nobody reads.

## The bet, stated as a bet

**Most tools should eventually ship a tutorial beside their reference material** —
the reference for people who know what to ask, the walkthrough for people who do
not yet know what they are choosing between.

That is a belief rather than an observation, and this bundle is deliberately
usable without it: one tutorial makes the templates worth having, and nothing
here assumes a second.

## Consumers

Both levels. A project teaches its own tooling; an organization teaches practices
that outlive any one repository, and *how we explain things to newcomers* is
exactly the kind of thing worth deciding once.

## Version

`0.5.0` — the driving-workflow template says what the **last** step's closing
block does.

**Every block takes the step number and adds one**, which is correct for every
step except the one that matters most to get right. The template now says the
final step points at the quiz rather than at a step number that does not exist.

**Found by a tutorial reaching its own ending**, which is the class of defect
review does not catch: the instruction was correct in general and wrong exactly
once, at the boundary.

`0.4.0` — the closing blocks in the driving-workflow template now open with
**Ask questions** rather than *Questions*.

**Because a closing line should tell the reader what to do.** *Questions, or say
next* names a topic; *Ask questions, or say next* offers an action, and the
difference matters at exactly the moment somebody is deciding whether to speak up
or move on.

Kept in step with `luma/token-manager`, whose tutorial carries the same blocks —
that text is meant to be byte-identical across tutorials, so it is not a place
where two bundles get to differ.

`0.3.0` — the test step now says where to run it and what to bring back.

It had asked for a run without saying **not in the session that wrote it**. That
session holds every step already, so the agent performing it knows what is coming
without reading, answers from the authoring conversation rather than the
material, and never meets the one-step-at-a-time constraint because nothing is
left to load. **It goes beautifully and proves nothing.**

**And the transcript comes back verbatim, both sides.** The defects worth finding
are exact wording — an invented heading, a transition that reads as the agent
talking to itself — and a summary is the layer at which wording disappears.
Pasted into the authoring session, which still holds the tutorial, the templates
and the reasoning, one pass can fix all three rather than guessing which layer
produced the problem.

Also: **do not tell the tester what you are testing for.** Somebody watching for
invented headings reads differently from somebody learning the subject.

`0.2.0` — [[create-tutorial]] gains a final step: feed what you learned back into
this bundle.

**Because the rules here came from running a tutorial rather than reasoning about
one**, and nothing else was going to keep that happening. Without a step for it,
the second tutorial's lessons stay in the second tutorial.

**Guarded twice.** Only for somebody who owns the catalog this bundle lives in —
an adopter's improvement to a vendored copy is silently overwritten on the next
adopt, so it is a change that looks applied and is not. And only for learnings
that would have helped a tutorial about something else; the test is whether the
improvement names the subject just taught.

**With a bias against writing rules.** A first observation goes to
[[lessons-from-the-first-tutorial]], not to [[what-makes-a-tutorial-land]]. A
rule written from one instance carries the authority of a pattern and the
evidence of an anecdote, and nobody downstream can tell which they are reading.

`0.1.0`. **The rules come from one tutorial and one run of it.** They are
well-motivated rather than proven — see [[lessons-from-the-first-tutorial]] for
what produced each, and for the list of what nobody has tested yet.

**Nothing here has built a second tutorial**, which is the only thing that will
show whether the templates generalise or whether they encode one subject's
accidents. The most likely correction is the driving workflow template being too
opinionated for a tutorial with no hazards at all — one that teaches something
outside the session it runs in, where the entire *sending somebody away* apparatus
is dead weight.
