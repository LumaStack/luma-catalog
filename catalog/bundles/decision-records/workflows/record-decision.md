---
type: workflow
title: Record a decision
description: Find or establish where this project keeps decisions, then write one. Use when a position is settled, when an irreversible change is proposed, or when asked where decisions live.
preload: mandatory
---

# Record a decision

## 1. Find the store

Look in this order and take the first that exists:

1. `.luma/records/decisions/` — a namespaced directory of individual records
2. `.records/decisions/` — a generic directory of individual records
3. `docs/DECISIONS.md`
4. `DECISIONS.md`

`.luma/records/decisions/` wins when several exist, because it is the mature shape
and `DECISIONS.md` is what a project keeps before it needs a mature approach.

**If more than one exists, say so before doing anything else.** That is not a
preference to resolve quietly — decisions are in two places and no reader can
tell which is authoritative. Report it, and offer to consolidate into the
directory.

## 2. If none exists, ask

Do not pick for them. Present both options and what each costs:

> **A file** — `DECISIONS.md`, newest first. One thing to read start to finish
> and one thing to point an agent at. Best while there are only a handful of
> decisions.
>
> **A directory** — `.luma/records/decisions/`, one record per decision. Each gets
> its own history and can be linked to individually. Better once decisions
> accumulate, and the shape you will end up in eventually.

A project past brainstorming should generally take the directory. A project on
day one generally should not.

## 3. Write the record

**In a directory**, the filename is `ADR-NNNN-<slug>.md` — four digits, zero
padded, next unused number:

```
.luma/records/decisions/ADR-0007-catalog-not-registry.md
```

Two things to know about the numbering. It is sequential, so two branches can
both claim `ADR-0012` and someone has to renumber on merge — the cost of the
convention, accepted because a short handle to cite in conversation is worth
it. And the number is not the identity: the Document ID is the whole path, so
renumbering breaks inbound links exactly as any rename does.

**In a file**, append a section at the top rather than the bottom. Newest first,
so the most relevant thing is not at the end of a growing document.

Either way, the content is the same, and it is `type: decision` — see that type
for what a record carries and how status maps onto `lifecycle_status`.

## 4. Decide whether this is even a decision

Record a decision when a position is **settled**, not while it is being argued.
The test: could someone act differently tomorrow because of this? If not, it is
a note.

Record one **before** an irreversible or expensive change, not after. A record
written afterwards documents what happened; one written first is a decision.

## 5. Correcting and superseding

Do not silently edit a settled record.

- The **record** was wrong — a bad rationale, a claim that does not hold?
  Correct it in place, dated and visible.
- The **decision** changed? Write a new record, archive the old one, and point
  `superseded_by` at the replacement.

The second is the one people get wrong by reaching for the first, and the cost
is that the reasoning which produced the original position disappears.

## 6. Graduating from a file to a directory

When the file is genuinely painful rather than merely long:

1. One `decision` document per entry, `ADR-NNNN-<slug>.md`, numbered in the
   order they were originally settled.
2. `decided` comes from each entry's own settled date, not the date of the
   migration.
3. Delete `DECISIONS.md`. Leaving it behind is the split store from step 1,
   created deliberately.

**This is effectively one-way.** Once records exist separately they accumulate
their own `modified` and `verified` events, and collapsing them back discards
all of it.
