---
type: workflow
title: Review the next unit
description: One sweep session — reconcile the index, orient without judging, let the person read first, then act on what they say. Use to continue an open sweep, including after a break.
---

# Review the next unit

**This is the whole loop.** Resuming a sweep is running it again; there is no
separate resume procedure, because step 1 is the reconciliation a resume would
have done.

## 1. Reconcile the index against the tree

The code moved since the index was built — by your own fixes, if nothing else.

```sh
git diff --name-status <indexed_at>..HEAD
```

- **Added** files in scope get rows, marked pending.
- **Deleted** files are struck through rather than removed, so the index still
  explains itself.
- **Renamed** files keep their status. A move is not a reason to re-read
  something.
- **Substantially rewritten** files already marked reviewed go back to pending,
  and say why in the row.

Update `indexed_at` to the current commit.

**If the sweep sessions and the index disagree, the sweep sessions win** — they
are the source and the index is a cache. Rebuild the row rather than trusting
it.

## 2. Pick the next cluster

Follow the recorded order. **If the recorded order is not working, change it
deliberately** — a dated line in `sweep.md` saying what changed and why. Not
one convenient sweep session at a time.

**Three to eight files.** Fewer means a file read without its collaborators;
more means a skim.

## 3. Orient — facts only, no verdicts

**Read the cluster, then say what it is.** What these files do, how they
connect, what calls in and what they call out, what changed here recently and
how often.

**No judgement**, and this is the load-bearing constraint of the whole practice
— see [[the-pairing-turn]]. *This is called from three places, one holding no
lock* is orientation. *This is over-engineered* is a verdict, and saying it now
means the person spends the sweep session reviewing your opinion instead of
their code.

**A live hazard is the exception** and is said immediately.

## 4. Hand over, and let them speak first

Say what you would like from them — *read these four, tell me what you make of
the retry logic* — and then stop.

**Wait.** If they ask you to go first, decline once with the reason and offer
the read afterwards; if they ask again, do it and note it in the sweep session.

## 5. Respond

Now the judgement. Where you agree, where you do not and why, and what they did
not raise.

**Disagree where you disagree**, including when they have just called something
fine. An agent that only ratifies has added nothing to a sweep session they
could have run alone.

**Say what this cluster makes you doubt about an earlier one.** A sweep learns
as it goes and the ninth sweep session routinely falsifies the third; that is
not a failure, it is the compounding the order was chosen for.

## 6. Act, and route everything out

Fix what you both understood here. Capture the rest where it belongs — see
[[what-a-sweep-session-produces]]. Nothing worth keeping stays in the sweep
session note.

**Propose before applying.** A change the person has not seen turns their
review into a diff review of yours.

## 7. Write the sweep session and update the index

[The sweep session template](../templates/sweep-session.md). It is a working
note, not a report — what was covered, what was concluded, what left the sweep
and where it went.

Mark every file in the cluster reviewed, including the ones where nothing was
found. **Reviewed and clean is a result**, and an index that records only
problems has unexplained gaps in place of evidence.

## 8. Commit, and land the fixes

One commit for the sweep session note and the index. The fixes go as one pull
request for the sweep session, whose body is the note.

**Land it before the next sweep session.** Otherwise the next one reviews code
that is about to change.
