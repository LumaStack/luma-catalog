---
type: bundle
version: 0.1.0
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

`0.1.0`. **The rules come from one tutorial and one run of it.** They are
well-motivated rather than proven — see [[lessons-from-the-first-tutorial]] for
what produced each, and for the list of what nobody has tested yet.

**Nothing here has built a second tutorial**, which is the only thing that will
show whether the templates generalise or whether they encode one subject's
accidents. The most likely correction is the driving workflow template being too
opinionated for a tutorial with no hazards at all — one that teaches something
outside the session it runs in, where the entire *sending somebody away* apparatus
is dead weight.
