---
type: workflow
title: Review the next unit
description: One slice — reconcile the index, orient without judging, let the person read first, then act on what they say. Use to continue an open sweep, including after a break.
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
- **Substantially rewritten** files are the one case needing a decision, and it
  is not yours to make alone — see below.

Update `indexed_at` to the current commit.

**If the slices and the index disagree, the slices win** — they are the source
and the index is a cache. Rebuild the row rather than trusting it.

### Re-covering is asked for, never applied

**Slices partition the sweep**, so in the ordinary case a file is read once.
**Never silently return a row to `pending`.**

Say what changed and ask — *`src/gate.py` was covered in slice 004 and has been
substantially rewritten since; do you want it re-covered, or does the earlier
read still stand?* Both answers are common, and the person who read it is the
one who can tell.

**When a file is re-covered the row records it** — the earlier slice, the new
one, and why. That is what makes drift visible as something accumulating rather
than as a ledger quietly resetting itself.

**If rows keep going back to pending, the sweep is losing to the codebase.**
Say so rather than absorbing it: either the scope is too large for the rate of
change, or too much is being fixed mid-sweep.

## 2. Pick the next cluster

Follow the recorded order. **If the recorded order is not working, change it
deliberately** — a dated line in `sweep.md` saying what changed and why. Not
one convenient slice at a time.

**Three to eight files.** Fewer means a file read without its collaborators;
more means a skim.

## 3. Orient — facts only, no verdicts

**Read the cluster, then say what it is.** What these files do, how they
connect, what calls in and what they call out, what changed here recently and
how often.

**No judgement**, and this is the load-bearing constraint of the whole practice
— see [[the-pairing-turn]]. *This is called from three places, one holding no
lock* is orientation. *This is over-engineered* is a verdict, and saying it now
means the person spends the slice reviewing your opinion instead of their code.

**A live hazard is the exception** and is said immediately.

## 4. Hand over, and let them speak first

Say what you would like from them — *read these four, tell me what you make of
the retry logic* — and then stop.

**Wait.** If they ask you to go first, decline once with the reason and offer
the read afterwards; if they ask again, do it and note it in the slice.

## 5. Respond

Now the judgement. Where you agree, where you do not and why, and what they did
not raise.

**Disagree where you disagree**, including when they have just called something
fine. An agent that only ratifies has added nothing to a slice they could have
run alone.

**Say what this cluster makes you doubt about an earlier one.** A sweep learns
as it goes and the ninth slice routinely falsifies the third; that is not a
failure, it is the compounding the order was chosen for.

## 6. Act, and route everything out

Fix what you both understood here. Capture the rest where it belongs — see
[[what-a-slice-produces]]. Nothing worth keeping stays in the slice note.

**Propose before applying.** A change the person has not seen turns their
review into a diff review of yours.

## 7. Write the slice and update the index

[The slice template](../templates/slice.md). It is a working note, not a report
— what was covered, what was concluded, what left the sweep and where it went.

Mark every file in the cluster reviewed, including the ones where nothing was
found. **Reviewed and clean is a result**, and an index that records only
problems has unexplained gaps in place of evidence.

## 8. Commit the slice

One commit for the slice note and the index. That is the sweep's record and it
lands whether or not anything was fixed.

**The fixes are on their own schedule** — batched by kind rather than by where
they were found, and landed however this project lands changes. See
[[what-a-slice-produces]].

**The one thing to watch is staleness.** If a large pile of unlanded fixes is
building up, land it before the next slice; otherwise you are reading your own
work in progress.
