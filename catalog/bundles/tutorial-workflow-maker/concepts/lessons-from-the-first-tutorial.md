---
type: document
title: Lessons from the first tutorial
description: Where the rules in this bundle came from — what a real run of the first paced tutorial exposed, and which mistakes were only visible once an agent performed it at somebody. Read when arguing with a rule, not while following one.
preload: optional
---

# Lessons from the first tutorial

**The rules in [[what-makes-a-tutorial-land]] are not derived from a theory of
teaching.** They are what a single walkthrough got wrong, in order, and most of
them were invisible until an agent actually performed it at a person.

That is the honest summary of this bundle's evidence base: **one tutorial, one
run.** Treat the rules as well-motivated rather than proven, and expect the next
run to add to them.

## Reading the workflow was not enough

Every mistake below survived careful authoring. The workflow said the right thing
in prose, and the agent did something else — not from disobedience, but because
**prose describing an outcome leaves the wording to be invented, and invented
wording is where the seams show.**

**It headed each step *Screen 1 —*.** The word *screen* had been deliberately
removed from every reader-facing sentence, and the workflow said plainly to call
them steps. The agent still coined a label, because nothing had told it what the
heading looked like. The fix was to write the heading out.

**It ad-libbed the closing line into gibberish**: *"This one runs here, in this
window — the whole point is mak I'll wait. Tell me what you called it and we'll
move toscreen 2."* Told to *offer to wait*, it composed a sentence each time. The
fix was four closing blocks, word for word, selected by `pause`.

**It announced the step count**, turning a walkthrough into a queue.

**The general lesson is worth more than the three fixes.** Anywhere the tutorial
has a consistent surface — a heading, an offer, a transition — **specify the
literal text.** Anywhere it needs judgement, describe the goal. Confusing the two
produces exactly this: correct behaviour, wrong voice.

## The steps argued well and left nothing behind

The larger gap was not the agent's. Every step made its case, and none of them
were skimmable — the instruction sat in a sentence, in the middle of a paragraph
that read beautifully.

**A reader who agrees with every sentence and cannot restate one has learned
nothing**, and that failure is invisible while writing, because the author knows
what the point was. Takeaways are the cheapest available test: **if the list
cannot be written, the step did not have a point.**

## Two framings that were wrong, and why they mattered

**"The pause is the point."** It is not. The point is whatever the tutorial
teaches; the pause is how the material is delivered so it lands. Saying otherwise
put the emphasis on the mechanism, which is the sort of error that quietly shapes
every later decision — a tutorial optimised for its pauses is a different and
worse artefact than one optimised for what the reader ends up knowing.

**"A pause you had to be briefed about is one you are waiting for rather than
using."** A good line, and false. It was doing the work of justifying an absolute
rule, and the honest version is narrower: **announcing a pause usually buys the
reader nothing, and sometimes it does** — when they must be mentally prepared, or
when hitting it unwarned would be jarring.

**Both are the same failure.** A rule that has earned a default gets written as a
law, because the law is easier to state and sounds more confident. The cost lands
later, on somebody who has a genuine exception and no permission to take it.

## The second pass found different things than the run did

**The run found what the agent did wrong. A read-through by the author found what
the writing did wrong**, and they barely overlap — which is an argument for doing
both rather than treating either as the review.

**An explanation that makes the reader derive the rule.** The mechanism step
described a worked example and left *each message re-buys everything before it*
to be induced from it. Every reader would get there; some slowly, none certain.
Stating the rule and then illustrating it is strictly better and costs nothing.

**Arithmetic the reader has to perform.** *A file read on turn four of a forty-turn
session costs thirty-seven more times* asks for a subtraction before anybody can
agree with it. *Read at the start, so it costs forty times* is the same fact with
the work already done.

**A step that sends people away, placed early.** The audit was step three. It is
a long job in another window, before the reader knows enough for its findings to
mean anything — so it is both the least useful place for it and the point they
are most likely not to come back from. It is now last. **This one was argued for
in `BUNDLE.md` before it was argued against**, which is worth knowing: *measure
first* is a genuinely appealing principle that happens to be wrong inside a
walkthrough.

**Cross-references by number.** Moving one step falsified every *step 12* in the
prose, silently. The references that used *the previous step* and *the earlier
step* survived untouched. That is a clean natural experiment, and the rule falls
out of it.

## Boundaries are where correct-everywhere instructions fail

**The closing block said *next for step 21*.** The instruction — take the step
number, add one — is right nineteen times out of twenty, and reading it will
never tell you about the twentieth. Only arriving at the end does.

**This is the general shape worth carrying**, not the specific bug. An
instruction that holds across a range usually has an edge it does not hold at,
and the edges of a tutorial are enumerable: the first step, the last step, the
handoff into the quiz, the handoff out of it, and the first time the reader is
asked to leave. Checking them takes a minute and is not something a careful
read-through substitutes for.

## What is still untested

**Whether twenty steps is too many.** Nobody has been through the whole thing in
one sitting, and attention is the obvious limit.

**Whether the `apply_here` offers earn their interruption**, or whether readers
wave them through and the pause becomes ritual — the exact failure the sizing
rule is meant to prevent, arriving by a different route.

**Whether the do/don't split is the right cut.** It reads well and it says one
thing twice: *choose a model at the start* and *do not switch mid-session* are
the same fact in both halves.

**And whether a tutorial should be a bundle's job at all.** The bet in this
bundle is that most tools eventually ship a walkthrough beside their reference
material. That is a bet, not an observation.
