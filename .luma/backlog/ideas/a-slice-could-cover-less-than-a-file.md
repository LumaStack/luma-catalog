---
type: luma/idea
title: A slice could cover less than a file
created: { by: human:benlinton, at: 2026-08-29T00:00:00Z }
contributors: [human:benlinton, agent:claude-opus-5]
horizon: later
scope: project
stage: draft
---

# A slice could cover less than a file

**A sweep advances one file, or a batch of them, and nothing smaller.** `slice`
declares `covers` as *"the repository-relative paths read in this slice"*, so the
unit is baked into the field: a file is either read or it is not.

**That should stay the default.** Whole files are the right grain nearly always,
they need no parsing, and coverage stays a set of paths that anybody can check by
eye.

**But a review should be able to get much more targeted than that** — a section
of prose, a function, a range of lines. *Re-read only what changed. Review one
function after a bug. Sweep a section of a specification without re-reading the
specification.*

## What a finer unit would mean

**`covers` entries stop being paths and become selectors.** Something like
`src/parser.py#parse_header` or `docs/SPEC.md#section-10`, alongside plain paths
which keep meaning *the whole file*.

**Coverage arithmetic changes shape, and this is the hard part.** Today coverage
is set membership: a path is in the union of `covers` or it is not.
Sub-file units make **partial** a third state, and *is this file covered* becomes
*is every part of it covered*, which needs to know what the parts are.

## The two candidate units are not equally good

| | durable? | needs a parser? |
| --- | --- | --- |
| **`path:line-line`** | **no** — a line range rots the moment anything above it moves | no |
| **`path#function`, `path#heading`** | **yes** — survives edits that move it | **yes, per language** |

**Line ranges are cheap and rot.** A slice recorded in March pointing at lines
120–180 describes something else by May, silently, and a sweep that trusts it
reports coverage it does not have.

**Named units survive edits and cost a parser per language.** That is a large
thing to take on — this estate already treats *three frontmatter parsers* as a
cost worth naming, and this is that problem multiplied by every language a
project uses.

*A cheap middle exists and is worth thinking about first:* headings in prose need
no parser, since Markdown already names its own sections. **Prose could get finer
units long before code does**, and would answer the specification case on its
own.

## What it must not break

**Silence still has to mean *read and nothing found*.** The `slice` policy is
explicit that every file read is listed, including where nothing was found —
because a slice naming only the interesting files makes *examined and clean*
indistinguishable from *never opened*.

**Sub-file units make that easier to get wrong**, not harder: reading one
function and recording the file would claim coverage nobody has. Whatever
selector arrives has to make partial coverage *visible* rather than roundable up.

## Why not now

**Nothing has asked for it yet.** The sweep works at file grain and no sweep has
run long enough to find the grain painful. **The unit to build is the one
somebody has hit a wall on**, and this is a design that would be a guess.

**Worth deciding before the first big sweep, though**, because `covers` is
already load-bearing: `charter.md`'s index is a cache rebuilt from it, so the
field's meaning is depended on in more than one place and widening it later is a
migration rather than an addition.
