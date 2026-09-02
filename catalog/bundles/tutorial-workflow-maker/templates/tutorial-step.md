# Tutorial step template

Copy the block below into `procedure/<tutorial>/steps/NN-<slug>.md`. **Copy the
block, not this file** — frontmatter here would make this a real step of this
bundle.

````markdown
---
type: luma/tutorial_step
title: CHANGE-ME — the same words as the heading below
step: 1
pause: apply_here
---

# CHANGE-ME — the same words as the title above

Open with the problem, the pitfall or the trap. Something the reader recognises,
or will recognise the next time it happens to them. Two or three sentences.

Say why it matters, if that is not already obvious from the problem. Skip this
where the cost speaks for itself.

**State the rule outright, then illustrate it.** Do not leave the reader to induce
it from a worked example — they will get it wrong, or get it slowly, and a rule
they assembled themselves is one they are not sure of. Say the thing, then show
it happening.

**Then walk to the solution, conversationally.** Take the time it needs. Bold the
sentence that carries the claim, so somebody skimming the prose still catches it.
Name the trade if there is one — a rule with no cost reads as marketing, and the
reader has already thought of the objection you left out.

## Takeaways

- The thing to do, stated as an instruction.
- The number or the mechanism worth remembering.
- The trap, phrased so it is recognisable in the wild.
- **Bold the operative words** — this list gets scanned, not read.
````

## Filling in the frontmatter

**`step`** — position in the running order, from `1`. Not taken from the
filename; renumber the field when inserting, which shows up in a diff.

**`pause`** — where the reader can act on this, and the field the whole type
exists for:

| | |
| --- | --- |
| `apply_here` | safe to do inside the session running the tutorial |
| `apply_elsewhere` | would cost or destroy that session — a second window |
| `practice` | a fact about how something works, nothing to change |
| `none` | a summary or a close, nothing to act on |

**Get this right before you write the prose.** It is the one field that can cost
somebody their session, and it has no default precisely so it cannot be guessed.

## What does not go in here

**No presenter notes and no instructions to the agent.** A step is read out very
nearly verbatim, so anything meant for the agent gets read out too. It belongs in
the driving procedure.

**No closing block.** *Practise this here, say next when you're ready* is
rendered by the procedure from `pause`, so its wording stays identical across
every step.

**No mention of the pacing.** Not how many steps there are, not that a pause is
coming. See `what-makes-a-tutorial-land` for the exception.

**No reference to another step by number.** *The previous step*, *the earlier
step*, *the audit at the end* all survive a reorder. *Step 12* does not, and
nothing warns you when it stops being true — inserting one step anywhere above
silently falsifies every number below it.

**No arithmetic the reader has to do.** *Read at the start of a forty-turn
session, so it costs forty times* lands; *read on turn four of forty, so
thirty-seven more times* makes them subtract before they can agree with you.

## The size rule

**Prose and takeaways together on one laptop screen** — about three hundred
words, thirty-odd lines, leaving room for the closing block. If it will not fit,
it is two steps.
