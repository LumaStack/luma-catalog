---
type: policy
title: What makes a tutorial land
description: The rules a paced tutorial follows — how a step is shaped, how the agent presents it, what it must never do to the session it is running in, and what a quiz owes the reader. Read before writing or reviewing one.
preload: mandatory
---

# What makes a tutorial land

**A tutorial is not a document somebody reads. It is something an agent performs
at a person**, one piece at a time, inside a live session that the material is
often about changing. That is what makes it a different problem from a readme,
and every rule here comes from that.

**Each rule names what goes wrong without it.** A convention that cannot say what
it prevents is a preference, and a preference in a policy is something future
authors have to obey and cannot argue with.

The reasoning behind these, and the run that produced most of them, is in
[[lessons-from-the-first-tutorial]]. Read that when arguing with a rule, not
while following one.

## A step is one idea, and it fits on a screen

**Prose plus takeaways on a laptop screen without scrolling** — around three
hundred words, with room for the closing block the workflow adds.

A step is the unit of a stop. **Something too long to take in at once cannot be
paused after**: the reader is still working through the first half when the offer
arrives, so they wave it away, and the pause becomes a formality. If it will not
fit, it is two steps.

## Explanation first, takeaways second

**The prose opens with the problem, the pitfall or the trap.** Say why it matters
if that is not obvious, then walk to the solution conversationally. This part is
allowed to take its time.

**Then a takeaways list, and it is not optional.** The same content, formatted to
be scanned.

**Prose alone leaves nothing behind.** A step that argues well and buries its
instruction in a paragraph was agreed with and not retained — an hour later the
reader cannot say what they were meant to change. **If a takeaway cannot be
written, the step has not decided what it is for.**

## Every step declares where the reader can act on it

`pause` is `apply_here`, `apply_elsewhere`, `practice` or `none`, and it is
mandatory with no default.

**A tutorial is dangerous in a way an ordinary document is not**, because the
reader is inside a live session while being told what to do to one. Some of what
a walkthrough recommends would destroy the session delivering it. **The reader
cannot know which** — the step that says *clear between jobs* does not say
*except right now*.

**Knowing that is the author's job, and then the agent's.** The default that
would be guessed is the one that costs somebody their session, which is why there
is no default.

## The driving workflow names its own hazards outright

**List what must never be run in the session, with what each would do**, rather
than leaving the agent to work it out mid-run. And when the reader asks for one,
the agent says what it would do and where to do it instead — **a tutorial that
declines to break its own rule in front of somebody is far more convincing than
one that states the rule.**

**Never strand them.** Say where they are before they leave — a number and a
title — so coming back costs one word. Carry a recovery path, because somebody
will clear the session anyway: ask which step they reached and resume there,
never replay what they already sat through.

## The agent presents, it does not perform

**Give the exact heading format and the exact closing blocks, written out.**
Describing them is not enough; an agent told to *offer to wait* will invent
wording, and improvised wording is where a tutorial stops sounding like it is
talking to the reader and starts sounding like it is talking to itself.

**After a step: nothing of its own.** No summary, no observation about what was
interesting, no preview of what is coming. The reader has just read it.

## Do not narrate the pacing

**No *one step at a time*, no *I'll pause after each*, no step count.** Saying a
pause is coming usually buys the reader nothing — they find out when it arrives,
and stopping there reads as natural because it is the obvious thing to do at that
point. Announced in advance it is a procedure they have been enrolled in, and a
count turns the walkthrough into a queue to get through.

**The exception is real**: announce a pause when the reader must be mentally
prepared for it, or when hitting it unwarned would be jarring — a wait long
enough that silence would read as a failure. A step that ends with an offer and a
visible way to continue is not that.

## One step is loaded at a time, and never ahead

The agent reads the step it is presenting and no others. If it needs to know what
is coming, the running order carries the titles.

**A walkthrough that loads every step up front pays for all of them on every
turn.** For a tutorial about context cost that is self-refuting; for any other it
is still the reader's money.

## A quiz explains every option, and scores nothing

**Never show or hint at an answer before the reader has chosen.**

**Then say whether they were right, and why** — and when they were wrong, give the
correct answer with its reasoning *and* what is wrong with the one they picked.
**The wrong answers are the material**: a reader who picked one has just shown
exactly which model they are carrying, and it is the only moment it is cheap to
correct.

**Nothing branches on the result.** No re-asking, no running tally read aloud, no
record kept. A tally turns a check into an exam, and an exam changes what the
reader is willing to admit they did not understand.

## Say what harness it assumes

**Name it before the first step**, and say plainly which parts travel: the
mechanism usually does, the keystrokes usually do not.

A reader hitting a command that does not exist concludes the tutorial is wrong
about everything else too — and they have no way to tell which half was portable.
