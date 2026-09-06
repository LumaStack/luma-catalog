---
type: policy
title: ASCII style guide
description: The marks a command line uses to show state — six glyphs, what each one means, and the rules that keep them readable when colour, fonts or width are not available.
matches: eager
---

# ASCII style guide

**A state is shown as a mark, not a word.** One glyph in a fixed first column
scans in a single pass; a word per row has to be read, and a column of read
words is a paragraph nobody asked for.

```
┌─────┬──────────────────────────────────┐
│ ○   │ not started, empty               │
│ ◐   │ under way, in progress, working  │
│ ✔   │ delivered, success, proven       │
│ ↪   │ superseded, replaced             │
│ ⊘   │ cancelled, missing, not found    │
│ ✘   │ failed, error, disproven         │
└─────┴──────────────────────────────────┘
```

## Why these six

**Unfinished work shares the circle; finished work changes shape.**

`○` and `◐` differ only by fill, which is right — they are the same thing at
two points, and the fill is the progress. A filled circle for *done* would join
that family and be mistaken for an empty one down a column, so the finished
states leave the circle entirely. **Done and not-done separate before anything
is read**, and the fill only has to distinguish the two unfinished states from
each other.

**`✔` and `✘` are a matched pair** — *it came out* and *it did not come out*.
They are the same weight and the same size, because an ending that went badly
should read as an ending, not as an interruption.

**`↪` and `⊘` are the endings that are neither.** Superseded work did not fail;
it moved, and something else covers it now. Cancelled work did not fail either;
somebody chose. Marking either `✘` reports a loss where there was a decision.

**`⊘` also carries absence** — missing, not found. A thing that is not there and
a thing switched off are the same to a reader: **nothing will come of looking
here**, and neither is anybody's failure.

**`↪` invites what should always accompany it.** The hook says *picked up over
there*, so name what superseded it on the same line. A supersession with no
successor named is the one shape of it that is genuinely lost.

## The rules that keep it readable

**Use the heavy marks — `✔` U+2714 and `✘` U+2718, not `✓` U+2713 and `✗`
U+2717.** The light pair is visibly thinner than the circles beside it, so a
finished row reads as fainter than an unfinished one. That is backwards:
finished work is what a scan skips past, and it should be the easiest thing to
skip.

**One fixed order, endings last: `○ ◐ ✔ ↪ ⊘ ✘`.** Best outcome first among the
endings and the bad one last of all — it is worth arriving at deliberately
rather than meeting halfway down a list. **A view whose order changes between
readings cannot be scanned**, which is the whole reason to fix it.

**Within a state, keep the order the data arrived in.** Do not re-sort. Any
ordering the records carry is one somebody chose, and re-sorting discards it.

**The mark is the meaning; colour is a shortcut.** Where colour is available —
`○` dim, `◐` yellow, `✔` green, `↪` blue, `⊘` dim, `✘` red — it is deliberately
redundant with the glyph. Output stays correct in a pipe, in a log, and for
anybody who cannot distinguish the hues. **Colour makes a scan faster; it never
makes one possible.**

**These are not ASCII, and that is the trade.** They are Unicode, and a terminal
without them shows tofu. Every one is from an old, widely covered block, chosen
over prettier alternatives for that reason — `◐` U+25D0 rather than a quarter-
filled variant, `↪` U+21AA rather than a curving arrow from a later block. Where
even that is too much to assume, fall back to `[ ]`, `[~]`, `[x]`, `[>]`, `[-]`,
`[!]`, and not to words.

## Do not invent a state the record does not claim

**A mark is a claim about what happened**, so use the one the data supports and
no stronger. Most systems cannot distinguish every state here: *cancelled* and
*abandoned* are usually one field, *failed* and *unproven* usually the same
absence of a pass.

**Absence is `○`, not `✘`.** Nobody having looked is not a bad result — it is no
result. **The distinction worth building toward** is between *not checked* and
*checked and undecidable*: the second is a defect in what was asked, it never
improves by waiting, and collapsing the two hides it. Test frameworks keep
*inconclusive* separate from both *failure* and *not run* for exactly that
reason.
