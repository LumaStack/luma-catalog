---
type: workflow
title: Create a tutorial
description: Turn source material into a paced tutorial — split it into steps, classify what the reader can safely act on, write the steps and quiz, and wire up the workflow that performs it. Use when something needs teaching rather than documenting.
---

# Create a tutorial

Takes whatever somebody already has — a script, a talk, a page of notes, a
practice living in one person's head — and produces a walkthrough an agent can
perform: steps, a quiz, and the workflow that drives them.

| | |
| --- | --- |
| **run it** | when a mechanism needs teaching, not documenting |
| **ends with** | a tutorial in the target bundle, and a first run booked |

[[what-makes-a-tutorial-land]] is the standard this works to. Read it first — the
steps below assume it.

## 1. Check that a tutorial is the right shape

**A tutorial teaches a mechanism whose consequences have to be ranked. A
reference answers a question somebody already knows to ask.**

The test: **could the reader act correctly on a bullet list?** If yes, write the
list. A tutorial earns its cost when the material has a *why* that changes what
somebody does in a case the list did not anticipate — which is exactly when a rule
obeyed without being understood goes wrong.

**Say so if it fails.** A tutorial nobody needed is worse than a readme, because
it demands twenty stops from somebody who wanted a paragraph.

## 2. Get the material, and cut it

Ask for everything in one piece rather than interviewing for it — people explain
better in one pass than in answers.

Then cut. **Anything that is not teaching goes**: preamble, promotion, asides,
the parts that only made sense out loud. What survives is claims and the
reasoning under them.

**Write it in your own words.** A transcript read aloud sounds like a transcript.

## 3. Split it into steps

**One idea each, and a step ends where the reader could stop.**

Two failures, in both directions. **Too fine** and the pauses become a metronome
somebody waves through. **Too coarse** and the step cannot be paused after at
all, because the reader is still digesting the first half.

Then order them, and group them if a grouping is real — *what to do* then *what
not to do*, or setup then mechanism then consequences. **Do not manufacture
symmetry**; an invented grouping makes the reader look for a distinction that is
not there.

**Six to ten per group is comfortable, fifteen is a stretch.** If it does not fill
that, do not pad it.

## 4. Classify every step's `pause` — before writing the prose

**This is the step of this workflow most likely to be skipped and the one that
costs the most.** For each, ask: *if the reader does this right now, in the
session running the tutorial, what happens?*

| | |
| --- | --- |
| `apply_here` | nothing bad — they can act now |
| `apply_elsewhere` | it would cost or destroy this session |
| `practice` | there is nothing to do; it is a fact |
| `none` | a summary or a close |

**`apply_here` is not the cautious answer.** It is a positive claim that acting
now will work, and sometimes it is the only correct one — a step teaching somebody
to name their session has to run *here*, or they name the wrong one.

**Then collect the `apply_elsewhere` reasons into the hazard table** for the
driving workflow. That table is what stops an agent cheerfully clearing the
session it is teaching in.

## 5. Write the steps

Template: [a tutorial step](../templates/tutorial-step.md).

**Problem, why it matters, then the solution, conversationally.** Then
`## Takeaways`, which is not optional — same content, formatted to be scanned.

**Write the takeaways first if a step is fighting you.** If the list will not
come, the step has not decided what it is for, and no amount of prose will fix
that.

## 6. Write the quiz

Template: [a tutorial quiz](../templates/tutorial-quiz.md).

**Situations, not definitions**, and every option explained — including the wrong
ones, on their own terms. **Make the last question the action the reader should
take the moment the quiz ends**, so answering it is the instruction rather than a
hypothetical about it.

## 7. Wire up the driving workflow

Template: [a driving workflow](../templates/driving-workflow.md).

**Most of it is already written.** Supply the subject, the harness, the hazard
table and the running order. **Do not reword the rest into your own voice** —
that text is deliberately identical across tutorials, and a second one phrasing
its offers differently is how two tutorials start behaving differently for no
reason anybody chose.

## 8. Vendor the types

Copy `_types/tutorial_step.md` and `_types/tutorial_quiz.md` from this bundle into
the target bundle, keeping `vendored_from` and updating `at`.

**Bundles are self-contained and have no dependencies**, so the contract has to
travel with the documents rather than being referred to across a boundary.

## 9. Run it, at a person

**Every rule in [[what-makes-a-tutorial-land]] that matters came from a run, and
none of them came from review.** Reading a tutorial tells you whether it is
correct. Watching one performed tells you whether it works, and those are
different questions — the first run of the first tutorial found an invented
heading, an improvised transition, and twenty steps that argued well and left
nothing behind, none of which were visible on the page.

**Watch for these specifically**, because they are the ones that recur:

- **wording the agent invented** where the workflow described an outcome rather
  than giving the text
- **anything said about the pacing** — step counts, warnings that a pause is
  coming
- **a step the reader waved through**, which means it was too long or the offer
  was wrong
- **a takeaway that turned out to be the whole step**, which means the prose was
  padding

**Fix the workflow, not the transcript.** Each of those is a gap in what the
driving workflow specified, and fixing it once is what stops the next tutorial
inheriting it.

## 10. Publish it

Version the target bundle, run its checks, and record what is untested in the
version notes — **a tutorial that has been run once is not a tutorial that
works.**
