---
type: workflow
title: Migrate an IDEAS file
description: Move ideas out of a single IDEAS.md into individual files, verify nothing was lost, and only then remove the original. Use once per project that has one.
---

# Migrate an IDEAS file

A one-off per project. The risk is not the moving — it is **removing the
original before anybody has checked**, so verification is a step rather than a
feeling.

## 1. Ask how involved they want to be

**Before reading anything**, because it changes how every step below is run.

| | |
| --- | --- |
| **delegated** | run the whole thing and record what happened. They read the result |
| **reviewed** | propose in batches — a table of title, one-line explanation, and where each would go — take feedback, and repeat until they are ready to sign off |
| **together** | one idea at a time: show what is needed to judge it, recommend where it goes, and decide keep-or-prune jointly |

**Ask rather than assume.** A long `IDEAS.md` is somebody's accumulated
thinking, and running `delegated` over it uninvited is how a migration becomes
something that happened *to* them.

**`together` and `reviewed` both present ideas one way** — see
[the idea review template](../templates/idea-review.md). Run without it the shape
drifts, and somebody reading a dozen reviews in a row has to relearn where the
recommendation is each time.

**Use it again whenever the thread is lost.** If they ask *what is next*, or the
migration has been interrupted for more than a round of discussion, the answer is
the template with the next idea in it — not a status paragraph. They are trying
to get back to deciding, and a summary of where things stand does not let them.

**`delegated` still stops at step 10.** Deleting the original always needs their
confirmation, whichever mode is chosen — the mode governs how much they are
consulted along the way, never whether they consent to the destructive step.

**Only an explicit decision advances a step.** A question, a request for more
detail, a correction to something unrelated, or agreement to a different point is
**not** signoff. Neither is silence, and neither is interest.

**If they open another topic mid-migration, nothing advanced.** Answer it, then
return to the idea that was on the table and ask again — naming which one it is,
because they will have lost the thread and the agent is the one holding it.

**Propose and stop.** In `together` mode especially, the recommendation and the
writing are two turns and never one. An agent that recommends a destination and
files it in the same breath has replaced their judgement with its own while
appearing to collaborate — and because the output looks identical either way,
nobody notices until an idea is somewhere they never agreed to put it.

## 2. Find out where ideas can go

**Before deciding where anything belongs, establish what *where* can mean.**
Migrating into the wrong place is the failure that matters here, and it is
silent — an idea filed under the wrong organization is one the people who would
act on it never see.

At minimum, ask. Four questions:

- **Which organization is this repository under**, and is there more than one in
  play? Somebody working across two is the case that goes wrong.
- **What other projects exist** that an idea might belong to?
- **Is there a headquarters** for any of those organizations?
- **If there is no headquarters**, where do private ideas belong?

**That last one is the only question here whose wrong answer cannot be undone.**
An organization-scoped idea often names customers, people, or strategy, and the
tempting move with nowhere obvious to put it is whichever repository happens to
be open. If that one is public, the idea is published permanently — deleting it
afterwards no more unpublishes it than deleting a committed credential does.

**With no private destination, do not file sensitive or private ideas.** Say so,
hold the idea, and ask. A private repository that already exists, or somewhere
outside git entirely, both beat the nearest convenient place.

Ordinary ideas are unaffected — most are not sensitive, and the absence of a
private home is no reason to stop migrating the ones that were never private.

Cheap discovery that narrows the questions rather than replacing them:

```sh
git remote -v                       # which organization this repository belongs to
ls -d ../*/.git 2>/dev/null         # sibling repositories, if they are checked out side by side
```

**Confirm what you find rather than acting on it.** Sibling directories are a
hint about what somebody has cloned, not a statement about what exists — and a
remote tells you where this repository lives, not where an idea should.

**A destination may not exist yet, and may not want to.** A repository with no
ideas directory needs one created and said so. A repository with **no luma at
all** is a different case: do not install `.luma/` there to make room for an
idea — ask, and if the answer is no, use whatever that repository already keeps
prose in. If a user agrees to adding `.luma/`, ask if it's their intention to
conform all affected repositories to using the standardized `.luma/` layout.

*The better version is not implemented: asking foreman or a headquarters for
this on the user's behalf.* A headquarters has the breadth to answer properly,
where a single checkout can only guess from what happens to be nearby.

## 3. Read the whole file first

Not every entry deserves to survive. A long-lived `IDEAS.md` accumulates things
that were done, abandoned, or overtaken, and **migrating them unchanged
launders stale material into the place people are told to trust.**

For each entry, decide: *migrate*, *drop*, or *already happened*.

**Record what you drop and why**, in the commit if nowhere else. *We
deliberately stopped wanting this* is worth keeping; silence is not.

Two tests catch most of what should not survive:

**A topic is not an idea.** *Competitive analysis*, *observability*, *developer
experience* — these name a subject without saying what would be built or what is
wrong now. Migrating one produces a file nobody can act on, in the list people
are told holds actionable wants. Prune it: if a real want appears later it will
be a better idea than the placeholder was.

**Settled is *already happened*, however long the entry is.** A design
conversation with a decision behind it has stopped being a wanted capability.
Length is not evidence it survived — the longest entries are often the ones that
got resolved most thoroughly. Check whether its conclusion is recorded somewhere
before assuming it is still open.

## 4. Decide where each one lives

Per entry, against the destinations from step 2: **who would act on this?**
[[where-an-idea-lives]] has the scope call.

**This is the step most worth slowing down for.** Everything before it was
preparation; this is where an idea gets put somewhere it will or will not be
found.

**Ask for guidance, or lean towards `project`, when it is unclear.** A
project-scoped idea is cheap to promote later; one filed under an organization
nobody checks is the kind that goes quiet.

**When nothing fits, say so rather than forcing it.** The three scopes are a
first guess, and a migration is the first time many ideas meet them at once —
which makes it the best opportunity to find out where they are wrong.

Record the mismatch: *this belongs to a customer, a product line, a
community, something that is not a project and not the organization.* That note
is the evidence the list needs to grow, and **the `project` default is what
destroys it** — an awkward idea quietly filed as `project` looks exactly like a
well-placed one, and the signal is gone.

## 5. Check whether a version already exists

```sh
grep -ril "<a distinctive word>" <ideas-directory>/
```

**If one does**, do not create a second. Read both, decide what this entry adds
that the existing idea lacks, propose the merge, get agreement, then append.

**Combine `contributors` — the union of both, not just the author.** An absorbed
idea may have had several people and agents in the exchange that produced it, and
carrying only whoever wrote it down discards the rest. Absorbing is the one
operation that edits an already-filed idea, so it is worth doing completely.

## 6. Otherwise create it

Follow [[capture-idea]] from step 1, with two differences:

- **`created.at` is when the idea was written, not today** — if the file or its
  history says. Backdating to today erases how long something has been waiting,
  which is exactly what a tending session reads.
- **`created.by` is whoever actually had it.** If that is unrecoverable,
  `unknown:unknown` is honest and far better than guessing — a name attached to
  an idea somebody never had is the one error here worth avoiding outright.

**And `horizon` gets decided, not defaulted.** Absent means `someday`, which is
indistinguishable from *nobody judged this* — so the one pass that reads every
idea in the file is the pass that should set it. **Ask rather than guess**: the
horizon is a claim about their priorities, and it is the one field an agent has
no standing to invent.

## 7. Mark it migrated, in the original

In `IDEAS.md`, against each entry:

```markdown
> *Migrated to `<ideas-directory>/<slug>.md`.*
```

**Do not delete anything yet.** The marker is what makes step 6 possible, and a
half-finished migration with no markers is worse than one not started.

**Then say where it landed, in one line, carried into the next idea rather than
sent on its own.**

```
**11 → luma-leader, persona-templates.md.**

## 12 of 14 — <title>
```

The frontmatter was proposed and agreed before anything was written, so restating
it is noise — and noise between ideas is what makes a long migration feel longer
than it is.

**Carried rather than separate, because correction latency is identical either
way.** Their next chance to interject is their next message, whether or not a
confirmation turn was spent first. A separate turn costs a round trip and buys
nothing, while a lead-in line keeps each idea readable as one block.

The exception is narrow: **anything in the file that was not in the proposal gets
a sentence.** A clarification recorded, a duplicate found, a caveat added — those
are new information. Everything else, they have already read, and silence means
it went in as proposed.

## 8. Report the breakdown

**Every fifteen decisions, and always when a source file is finished** —
whichever comes first. End of file is the stronger trigger, because it is when
somebody decides whether to delete the original. The interval exists only so a
sixty-entry file does not arrive as one enormous table with cold early rows.

Two tables, because a pruned entry needs a reason where a migrated one needs
metadata.

```markdown
**Migrated**

| # | Title | Landed | Modifications | Metadata |
|---|---|---|---|---|
| 1 | <title> | `<repo>` · <file> | none | someday · project |
| 8 | <title> | `<repo>` · <file> | retitled · context added | someday · project |
| 5 | <title> | `<repo>` · <file> | absorbed into <file> | *target's* |
| 14 | <title> | `<repo>` · <file> | split 1 of 2 | someday · project |

**Pruned**

| # | Title | Why |
|---|---|---|
| 6 | <title> | Already happened — settled in `DECISIONS.md` |

`<repo>` 8 · `<repo>` 3 · pruned 3
```

**`Modifications` is the column that earns the table.** Its vocabulary is
`none` · `retitled` · `notes added` · `split N of M` · `absorbed into X` ·
`absorbed #N` · `new capture`. Scanning it answers the only question worth asking
in bulk: *did my idea go in as I wrote it?*

**One → many is a split; many → one is an absorb**, and both are visible from the
same column. An absorbed row names the file that swallowed it; the receiving row
gains `absorbed #N`, so the table never claims a file was unchanged while an idea
disappeared into it. Where the target existed before this migration it has no row
of its own, and the absorbed row is the only trace — which is why it must name
the file.

**An absorbed idea's metadata is the target's.** It does not get its own
`horizon` or `scope`; it inherits what the file it joined already declares.
Writing its proposed metadata there would be fiction.

**Name an internal repository generically.** If a destination is an
organization's internal headquarters, the table says so and gives the path within
it — never the repository name, because these tables get pasted into places the
name should not reach.

### Write it into the original, not just the chat

**The breakdown goes at the top of `IDEAS.md` before anything is deleted.** Show
it in the conversation too — that is what they respond to — but the file is where
it has to live.

**Because the chat is not the paper trail.** A migration ends with somebody
deciding whether to delete the original, and that decision should be made against
a file that says what happened to every entry. Markers alone do not do it: they
are scattered through the file, they say nothing about what was modified, and
nobody reads a hundred of them to reconstruct a summary.

**And deletion is what makes it permanent.** Once the file is gone, its last
committed version is the only record — so that version should be the complete
one. A half-marked file frozen in history is a worse artifact than no file at
all, because it looks like a record and is not.

Deleting is still step 10, and still needs their confirmation. This only ensures
that whatever they decide, the evidence outlives the conversation.

## 9. Verify before removing anything

**Both a person and an agent, if you can get both.** They miss different things:
an agent catches an entry with no marker, a person catches an entry whose
meaning did not survive the rewrite.

- Every entry has a marker, or an explicit note that it was dropped
- Every named file exists
- Nothing acquired detail that was not in the original — **migration is not
  the moment to improve an idea**, and an idea silently enlarged during a move
  is one nobody agreed to

## 10. Archive, then delete on confirmation

**Archiving needs nobody's permission. Deleting needs the user's.**

The same rule as pruning, for the same reason: the original is somebody's work,
and a migration that ate it silently is the version of this that goes wrong.

Once confirmed, **delete the original.** Leaving it is the worst outcome — two
places holding the same ideas, drifting apart, with nothing saying which is
current. The history keeps it.
