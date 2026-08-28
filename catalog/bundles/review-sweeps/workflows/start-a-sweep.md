---
type: workflow
title: Start a sweep
description: Settle what is being read and what is not, choose an order, and build the index that makes coverage checkable. Use when beginning a file-by-file review of a project.
---

# Start a sweep

## 1. Check that a sweep is what they want

**Three things get asked for in the same words**, and two of them are cheaper:

| what they said | what they may want |
| --- | --- |
| *review my changes* | a diff review. Minutes, not weeks — whatever this project already uses |
| *find out whether X is a problem* | a targeted audit. Answers one question, and somebody else can respond to it |
| *I want to read this whole thing properly* | **a sweep** |

**Say the cost out loud before agreeing** — see step 5 for how to arrive at it.
Somebody who wanted an afternoon's reassurance should find out at the start
rather than at file nine, and nobody is offended by being asked.

## 2. Settle the scope, and what is excluded

**Ask; do not infer.** The obvious scope is *the repository*, and it is usually
wrong — vendored code, generated files, lockfiles, a subtree somebody else owns
and a test corpus are all things a person will happily exclude when asked and
will silently resent reviewing when not.

**Write both halves down.** What is in, and what was deliberately left out —
separating what they excluded from what you did. A sweep that does not say what
it skipped cannot make its own coverage mean anything later.

## 3. Choose an order and record why

See [[choosing-an-order]]. Narrative is the usual answer for a first sweep;
directory order is right more often than it sounds.

**One sentence of reason is enough**, and it is what makes the order survive
the sitting where a different one would be more convenient.

## 4. Build the index

Enumerate every file in scope, in the chosen order, and record the commit you
enumerated at.

```sh
git rev-parse --short=12 HEAD
git ls-files <paths> | grep -vE '<exclusions>'
```

**Every file in scope gets a row, even the boring ones.** The index is a
coverage ledger — a file left out of it is a file nobody can later prove was
read or not read, and the ones omitted for being trivial are exactly where a
stale copy of something hides.

**Group the rows into the clusters you expect to review together**, but do not
over-plan it: the clustering is a first guess and every sitting will revise the
one after it.

## 5. Say how long this will actually take

**Give a band, say it is a guess, and replace it with a measurement after two
sittings.** A number said at the start is what stops a sweep dying at 15% with
somebody concluding they were slow rather than that it was long. A number said
*confidently* at the start is usually wrong.

### Estimate from the material, never from the file count

**File count is the wrong denominator**, and using it is how a sweep gets
mis-sold in both directions at once. What costs time is the reasoning a file
demands, and that varies by more than an order of magnitude across a single
repository.

| material | a sitting is roughly | so |
| --- | --- | --- |
| **prose, docs, config** | a dozen files, sometimes thirty | **a hundred short documents is days, not months** |
| **ordinary application code** | three to eight files | the middle case, and where the guess is safest |
| **dense logic** — concurrency, parsing, anything with real invariants | one or two files, and sometimes half of one | a small directory can outlast a large one |

**Say which of these the scope actually is**, and split the estimate when it is
several. *Roughly four sittings for `docs/`, and fifteen for `src/`* is a useful
sentence. *Nineteen sittings* is not, because the two halves are not made of the
same stuff and the person will plan against the wrong one.

### Then stop guessing

**After the second sitting you have a rate.** Use it, say what it was, and
revise the number in `sweep.md`.

That revision is worth more than any care taken over the initial guess — it is
measured on this material, by these people, at whatever depth they actually
settled into. **Do not defend the original estimate against it.**

### If the number is unacceptable, cut the scope now

Not by quietly reviewing faster later. **A sweep of the four subsystems that
matter, finished, beats a sweep of everything, abandoned** — and cutting at the
start is a scope decision anybody can see, while cutting by acceleration is one
that only shows up as coverage nobody trusts.

## 6. Write `sweep.md` and commit it

[The sweep template](../templates/sweep.md) has the shape. Commit before the
first sitting — the index is the thing that makes the sweep resumable, and a
sweep that only exists in a conversation is one crash from gone.
