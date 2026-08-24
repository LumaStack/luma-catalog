# Driving workflow template

The workflow that performs a tutorial. Copy the block into
`workflows/<tutorial>/<tutorial>.md`, beside a `steps/` directory. **Copy the
block, not this file.**

**Most of it is already written**, because most of it should not vary between
tutorials. What you supply is the subject, the harness, the hazards and the
running order — the four things that are genuinely different each time. Everything
else is the format, and a second tutorial rewording it in its own voice is how two
tutorials start behaving differently for no reason.

````markdown
---
type: workflow
title: CHANGE-ME — phrased as the reader would ask for it
description: CHANGE-ME — what it teaches, that it is paced a step at a time, and when to run it rather than the neighbouring reference.
---

# CHANGE-ME

**A tutorial, not a briefing.** The subject is CHANGE-ME. The material is split
into steps, each sized to be read in one go, with a pause after each — because an
idea somebody stopped and applied is one they keep, and a wall of good advice read
straight through is one they agree with and forget.

| | |
| --- | --- |
| **run it** | CHANGE-ME — when somebody wants to understand … |
| **ends with** | a quiz |

## Say what this assumes, before step 1

**The steps are written for CHANGE-ME**, and they name its commands directly —
CHANGE-ME. Tell the reader that up front, in a line, before you present anything.

**The mechanism underneath is not specific to any harness**, and will still be
true wherever they are running. **The operating instructions are** — command
names, panels, defaults. On another harness those are somewhere between renamed
and absent.

So if this is not CHANGE-ME, say so plainly rather than presenting commands as
though they will work: **the reasoning transfers and the keystrokes may not.**
Then run it anyway.

**Open with this, then go straight into step 1.**

> CHANGE-ME — one line naming the harness and that the commands will work.
>
> This is about CHANGE-ME. There's a short quiz at the end.

**Do not describe the pacing, and do not announce how many steps there are.** No
*one step at a time*, no *I'll pause after each*, no count. Saying a pause is
coming usually buys the reader nothing — they find out when it arrives, and
stopping there reads as natural because it is the obvious thing to do at that
point.

**Announce one only where it earns it**: when the reader must be mentally
prepared, or when hitting it unwarned would be jarring.

## Read one step at a time

**Read the file for the step you are presenting, and no others.** Not the next
one, not a batch, not all of them up front to plan ahead. If you need to know what
a later step covers, the running order has the titles.

A walkthrough that loads every step up front pays for all of them on every turn.

**Present the step in full.** Do not summarise, condense or paraphrase it, and do
not skip its `## Takeaways`.

**Then stop.** Never advance on your own, however brief the step was.

## How a step is presented

Head each one exactly like this, with the number and title from its frontmatter:

```
**Step 4 — CHANGE-ME**
```

Then the step's body verbatim, `## Takeaways` and all. **Then the closing block
below, and nothing else.** No summary of your own, no observation about what was
interesting, no preview of what is coming. The reader has just read it.

## The closing block, word for word

**Print the block matching the step's `pause` field, changing only the step
number.** These are written out rather than described because an improvised
version is where the tutorial stops sounding like it is talking to the reader and
starts sounding like it is talking to itself.

`apply_here`:

> **Practice this here.** It is safe to do in this window — go ahead, I'll wait.
>
> Ask questions, or say **next** for step 5.

`apply_elsewhere`:

> **Practice this elsewhere.** Don't run it in this window — it would cost or
> clear the session we are in. Open a second window if you want to do it now, and
> I'll be here.
>
> Ask questions, or say **next** for step 5.

`practice`:

> **Nothing to change here** — this one is how the thing works. If you want to go
> and watch it happen in another session, I'll wait.
>
> Ask questions, or say **next** for step 5.

`none`:

> Ask questions, or say **next** when you're ready.

**Answer questions from the steps already presented** and from what you can see of
their setup. If the answer is a later step, say which one is coming rather than
reading ahead.

**If they take the offer, wait.** Do not fill the silence with the next step.

## Sending somebody away, and getting them back

**A pause that strands the reader has done more damage than skipping it would
have.** CHANGE-ME — if anything this tutorial recommends would wreck the session
running it, the reader cannot know which, and **knowing that is your job, not
theirs.**

**Say where they are before they go, every time.** *"You're on step 8, CHANGE-ME —
say next when you're back."*

**Never do these in this session, however reasonably they are asked for:**

| | what it would do |
| --- | --- |
| CHANGE-ME | CHANGE-ME |

**When they ask for one, do not simply decline it.** Say what it would do, name
the step that covered it, and say where to do it instead.

## If it goes wrong anyway

**Recover; do not restart.** Ask which step they had reached and resume from
there. **Do not replay steps they have already sat through**, which is the
response that makes people abandon a tutorial for good.

## Running order

| | step | |
| --- | --- | --- |
| 1 | [[NN-slug]] | CHANGE-ME |

## The quiz

Read [[quiz]] once the last step is done and they have said they are ready. **Not
before** — it carries every answer, and having it in context while you are still
presenting steps is how a hint leaks.

**One question at a time**, through the harness's interactive picker if there is
one, otherwise a numbered list. **Never show or hint at the answer before they
have chosen.**

**Then say whether they got it right, and why.** If they were wrong, give the
right answer with its reasoning, and say what is wrong with the option they
picked. The quiz file carries all of it.

**Do not re-ask, do not keep score out loud, do not soften a wrong answer into
being sort of right.**

## Ending

CHANGE-ME — what the reader should do the moment the quiz is over, and why that is
the tutorial's last instruction rather than a hypothetical.
````

## The four things you actually supply

**The subject** — what it teaches, in the opening and the description.

**The harness** — which one, which commands, and what happens on another.

**The hazards** — what must never be run in the session performing the tutorial.
Some tutorials have none; say so rather than leaving the table empty.

**The running order** — the steps, in order, with their titles.
