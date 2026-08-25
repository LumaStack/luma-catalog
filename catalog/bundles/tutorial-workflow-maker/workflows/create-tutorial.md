---
type: workflow
title: Create a tutorial
description: Turn source material into a paced tutorial — split it into steps, classify what the reader can safely act on, write the steps and quiz, and wire up the workflow that performs it. Use when something needs teaching rather than documenting.
compliance: optional
---

# Create a tutorial

Takes whatever somebody already has — a script, a talk, a page of notes, a
practice living in one person's head — and produces a walkthrough an agent can
perform: steps, a quiz, and the workflow that drives them.

| | |
| --- | --- |
| **run it** | when a mechanism needs teaching, not documenting |
| **ends with** | a tutorial in the target bundle, tested in a clean session, and anything general fed back here |

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

**Put the steps that send somebody away as late as you can.** A step that hands
the reader a long job in another window is a step some of them do not come back
from — and early on they leave before they know enough for the job to be worth
doing. At the end it costs nothing, because there is nothing left to lose them
from. This is the ordering mistake that is hardest to see while writing, because
sending somebody to measure their own setup *first* sounds like obvious good
sense.

**Reordering later is expensive, so spend the time here.** Moving one step
renumbers every file after it, every `step` field, the running order, and any
prose that named a step by number.

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

## 9. Test it in a clean session, and bring the transcript back

**Every rule in [[what-makes-a-tutorial-land]] that matters came from a run, and
none of them came from review.** Reading a tutorial tells you whether it is
correct. Watching one performed tells you whether it works, and those are
different questions — the first run of the first tutorial found an invented
heading, an improvised transition, and twenty steps that argued well and left
nothing behind, none of which were visible on the page.

### Not in this session

**The session that wrote the tutorial is the worst available place to test it.**
Every step is already in context here, so the agent performing it knows what is
coming without reading anything, answers questions from the conversation you just
had rather than from the steps, and cannot experience the one-step-at-a-time
constraint at all because there is nothing left to load.

**It will go beautifully, and that result is worth nothing.** A tutorial is
written for somebody arriving with none of this, and that is the only condition
under which a gap in it shows up.

So: **a fresh session, pointed at the driving workflow and nothing else.** A
different person is better still, but a clean session is the part that is not
optional.

**Do not tell them what you are testing for.** Somebody watching for invented
headings reads differently from somebody learning the material, and it is the
second one you need. Ask them to go through it as though they wanted to know the
subject.

### Then have them paste the whole transcript back here

**The actual text, both sides, not an account of how it went.** The failures live
in exact wording — an invented heading, a transition that reads as the agent
talking to itself — and a summary is precisely the layer at which wording
disappears. *"It went fine"* is compatible with every defect listed below.

**Paste it into this session**, which already holds the tutorial, the templates
and the reasoning behind both. That is what lets one pass fix the step, the
driving workflow and the template together, instead of guessing at which layer
the problem came from.

If it is too long to paste, ask for the opening and the first few steps verbatim,
plus any moment that felt off — **verbatim for the parts you get**, since a
paraphrased transition is a transition you cannot review.

### What to read the transcript for

These are the ones that recur:

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

### Check the boundaries specifically

**An instruction can be right for every step and wrong at the edges**, and that
is the defect a read-through never finds, because it is correct everywhere you
look. Go to the edges deliberately:

- **The first step.** Does the opening arrive before it, once, and does the step
  work for somebody who has been told nothing yet?
- **The last step.** *Say next for step N+1* points at nothing here. It should
  send them to the quiz.
- **The handoff into the quiz**, and out of the quiz into whatever ends the
  tutorial. Both are transitions no step owns.
- **The first `apply_elsewhere`**, which is the first time anybody is asked to
  leave, and the first chance to strand them.

### And check what the files say about themselves

Cheap, mechanical, and each one has been wrong at least once:

- **`title` matches the step's `# heading`.** The reader sees both — the heading
  the workflow prints, then the one in the body — so a mismatch shows them two
  names for the same step. Editing one and forgetting the other is the normal way
  it happens.
- **`step` matches the filename's number**, and the running order lists every
  step exactly once.
- **`after_step` on the quiz is the last step's number.**
- **No step refers to another by number.** *The previous step*, *the earlier
  step* survive a reorder; *step 12* does not, and nothing reports it when it
  goes stale.

## 10. Publish it

Version the target bundle, run its checks, and record what is untested in the
version notes — **a tutorial that has been run once is not a tutorial that
works.**

## 11. Feed what you learned back into this bundle

**Skip this entirely unless both are true: you own a catalog, and this bundle
lives in it.** Ask, rather than assuming — most people running this workflow are
adopters, and for them the answer is no.

**Because a vendored copy is a snapshot.** Improve one and the edit survives
exactly until somebody re-adopts, at which point it is overwritten with no
warning — nothing in the format signals that a copy was edited. So an adopter's
improvement is not a small win that might get lost; it is a change that looks
applied and is not. If you have a path upstream, send it there. If not, record it
wherever your project keeps learnings, and stop.

### Only what would have helped a different tutorial

**The test is one question: would this have helped somebody teaching something
else?** If the improvement names your subject, your tool or your commands, it
belongs in the tutorial you just made.

| stays in your tutorial | comes back here |
| --- | --- |
| the wording of a step | wording the agent invented, because the template described an outcome instead of giving the text |
| a hazard specific to your tool | a *kind* of hazard nothing prompted you to look for |
| the order you chose | a question this workflow should have asked and did not |
| a quiz question that fell flat | a way the quiz feedback format falls flat |

**The recurring shape is a gap you had to fill yourself.** If you wrote something
the templates did not provide, and the next tutorial would have to write it
again, that is the thing to promote — and it is usually a template edit rather
than a new rule.

**Prefer strengthening a template over adding a rule.** A template gets copied; a
rule has to be remembered. The guidance that actually got followed here arrived
as text somebody was already editing.

### One observation is not a rule

**First time something has come up? Put it in [[lessons-from-the-first-tutorial]]
with what you actually saw**, and leave [[what-makes-a-tutorial-land]] alone.
Promote it to policy when a second tutorial hits the same thing.

**A rule written from one instance carries the authority of a pattern and the
evidence of an anecdote**, and nobody downstream can tell the difference — which
is how a bundle accumulates rules that were somebody's one bad afternoon.

### Nothing to promote is the normal outcome

**Say so and stop.** A step that has to produce something produces noise, and a
policy that grows every time somebody uses the workflow becomes one nobody reads.

If there is a change, version this bundle, run its checks, and say in the version
notes **which tutorial produced it and how many have now hit it** — that count is
what a later reader needs to judge whether the rule was earned.
