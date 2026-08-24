---
type: type_definition
defines: luma/tutorial_step
version: "0.1.0"
extends: document
fields:
  step:
    obligation: mandatory
    field_type: number
    desc: "position in the running order — the sequence is data rather than a filename convention"
  pause:
    obligation: mandatory
    field_type: enum
    values: [apply_here, apply_elsewhere, practice, none]
    desc: "what to offer the reader once this step has been presented, and where they can act on it"
---

# luma/tutorial_step

**One step of a paced tutorial** — a single idea, presented on its own and
followed by a pause. It is the unit a walkthrough advances by, and the reason the
material is many documents rather than one long one: a step is loaded when it is
reached and never before, so the reader pays for what they are looking at rather
than for everything still to come.

A step is not a section. **A section can be skimmed in the presence of its
neighbours; a step is delivered alone, and the reader is expected to stop.**

## How long a step should be

**A rule of thumb for whoever writes one: it should fit on a laptop screen
without scrolling.** Roughly a couple of hundred words.

That is a sizing heuristic and nothing else — **call them steps everywhere a
reader can see.** *Screen* describes the constraint an author is writing against;
it is not what the reader is being walked through, and using it in the prose
makes the tutorial sound like it is about the display rather than the material.

The constraint matters because a step is the unit of a stop. **Something too long
to take in at once cannot be paused after** — the reader is still working through
the first half when the offer to answer questions arrives, so they decline it, and
the pause that the whole format exists for quietly becomes a formality. If a step
will not fit, it is two steps.

## `pause` is the field the type exists for

**A tutorial that recommends changing something is dangerous in a way an ordinary
document is not**, because the reader is inside a live session while being told
what to do to one. Some of what a walkthrough recommends would destroy the very
session delivering it — clearing it, compacting it, switching its model, or
filling it with the output of a long-running command.

**The reader cannot possibly know which.** The step that says *clear between
jobs* does not say *except right now*, and nothing in prose reliably flags it. So
the step carries the answer, and the agent presenting it does not have to judge:

| | what it means | what to offer |
| --- | --- | --- |
| `apply_here` | safe in the session running the tutorial | *go ahead, I'll wait* |
| `apply_elsewhere` | would cost or destroy this session | *open a second window and do it there* |
| `practice` | a statement about how something works, with nothing to change | *try it in another session sometime* |
| `none` | a summary or a close — nothing to act on | nothing; move on |

**Mandatory, with no default.** An omitted `pause` would have to be guessed at,
and the guess that costs somebody their session is the one a default would make.
Requiring it puts the decision with the author, who knows what the step is asking
for, rather than with the agent, which does not.

**`apply_here` is not the safe choice.** It is the specific claim that acting now,
in this session, will work — and on the step that teaches naming the session, it
is the only correct value, because sending the reader elsewhere would name the
wrong session. Neither direction is the conservative one.

## `step` is data, not the filename

Files sort by name, and a walkthrough that gets its order from `01-`, `02-` is
one rename away from a silently reordered tutorial. **Nothing reads the
directory**, so the sequence belongs in the document that occupies the position.

It also survives insertion. Adding a step means renumbering the field on the
steps after it — visible in a diff, and reviewable — rather than renaming files
and hoping every reference moved with them.

## Running a tutorial made of these

**The obligations a driving workflow has to honour**, gathered here so a second
tutorial does not have to reverse-engineer the first. The workflow still states
them — it is what runs — but this is the source they are copied from.

- **Read one step at a time, never ahead.** A walkthrough that loads every step
  up front pays for all of them on every turn, and a tutorial about context cost
  refutes itself by doing it.
- **Present it in full.** A step is already short; summarising it saves the
  reader nothing and discards the wording that was chosen.
- **Stop after every step**, however brief. Never advance unprompted.
- **Offer what `pause` says**, and say plainly how to continue.
- **Say where they are before they leave** — a number and a title, so coming back
  costs one word.
- **Recover rather than restart.** Somebody will lose the session. Ask which step
  they reached and resume there; never replay what they already sat through.

**And know which of your own recommendations would destroy the session running
the tutorial.** That is what `apply_elsewhere` is for, and the driving workflow
should name the specific hazards outright rather than leaving the agent to infer
them mid-run.

## What the body should carry

**The prose the reader sees, and nothing else.** No presenter notes, no answer
keys, no instructions to the agent — a step is read aloud more or less verbatim,
and anything in it that was meant for the agent will be read aloud too.

Everything aimed at whoever is running the walkthrough belongs in the workflow
that drives it, or in these fields.

## When to reach for this over a plain document

**When it is delivered rather than consulted.** A reference page a reader opens
when they need it is a `document`. A step is pushed at somebody in a fixed order,
one at a time, with a stop after it — and the stop is what needs describing,
which is what `pause` does and no plain document has anywhere to put.
