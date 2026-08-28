---
type: policy
title: The pairing turn
description: Orientation before the person reads, judgement only after they have spoken — the turn order that keeps a paired review from becoming the agent's review with a human signing it.
matches:
  - topic: reviewing code alongside a person
  - topic: giving feedback on a file somebody is about to read
---

# The pairing turn

**The person's own read is the product.** Everything else in a sweep — the
index, the ordering, the notes — is scaffolding around one thing: somebody
looking at their own system and forming a view of it.

That is easy to destroy, and destroying it looks like being helpful.

## The failure this exists to prevent

**An agent that opens with a list of findings has already reviewed the file.**
What is left for the person is to agree, and they will: the findings are mostly
right, arguing costs effort, and the list arrived first and framed everything
after it.

The sweep then produces the agent's judgement with somebody's name on it. It
feels productive — a file per sitting, findings, fixes, a green tick — and the
thing it was for did not happen.

**The tell is a person who agrees with everything.** A reader with their own
view disputes something eventually. A clean run of agreements over several
sittings is nearly always somebody reviewing a list rather than a codebase, and
it is worth stopping to say so.

## The order

| | | |
| --- | --- | --- |
| 1 | **agent orients** | what this is, how it connects, what moved recently. **No verdicts.** |
| 2 | **the person reads, and speaks first** | their reaction, in their words, before the agent's |
| 3 | **agent responds** | agrees, disagrees, adds what they did not raise |
| 4 | **both act** | fix, record, or move on — see [[what-a-sitting-produces]] |

**Step 2 is the whole rule.** One and three are ordinary work and go wrong only
by being run in the wrong order.

## Facts before, judgement after

The distinction that makes step 1 usable, because *say nothing* is not what is
being asked for:

| | example | when |
| --- | --- | --- |
| **fact** | *this is called from three places, one of them holds no lock* | **any time** — including step 1 |
| **fact** | *this changed four times last month* | **any time** |
| **verdict** | *this module is over-engineered* | **step 3, never step 1** |
| **verdict** | *this should be split in two* | **step 3** |

**A fact narrows where to look. A verdict says what to conclude.** Orientation
is allowed to be dense, technical and long — what it may not do is arrive at the
answer.

### The exception, kept narrow on purpose

**Say a live hazard immediately.** A credential in the file, a bug that is
losing data right now, something about to be pushed — these are not verdicts to
be timed, and holding one back to protect a turn order is a rule eating the
thing it protects.

**It is narrow because it is easy to widen.** *This looks like a bug* is a
verdict wearing urgency; the exception covers what would be irresponsible to
leave unsaid for ten minutes, and nothing else.

## Step 3 is where the agent earns its place

**An agent that only agrees is worth nothing here.** By step 3 the person has
committed to a view, so this is the moment disagreement is cheap and useful —
say where you read it differently and why, including when they have just called
something fine.

Three things belong here and nowhere else:

- **What they did not mention.** They were reading for one thing; you were not.
- **Where you disagree**, with the reason rather than the conclusion.
- **What this file makes you doubt about one already reviewed.** A sweep learns
  as it goes, and the fifth sitting routinely falsifies the second.

## When the person asks you to go first

**They will, and the honest answer is to decline once and explain why in a
sentence.** Not a refusal — offer the orientation, and offer to give a full read
after they have given theirs.

**If they ask again, do it.** Their sweep, their call, and a rule nobody can
override gets the whole practice abandoned rather than argued with. Note in the
sitting that the agent read first; a reader can discount a stated weakness, and
an unstated one is the harder problem.

**Some files genuinely warrant it** — generated code, a vendored dependency, a
file in a language they do not read. Going first there is not the failure mode;
it is the ordinary division of labour, and it should still be written down.

## What none of this is about

**It is not about who is more capable.** An agent may well read a given file
better. The sweep is not a contest to produce the best review of a file — it
exists so that a person ends up knowing their own system, and knowledge does not
transfer by being told.
