---
type: luma/idea
title: review-sweeps could be named for the pairing instead
created: { by: human:benlinton, at: 2026-08-29T00:00:00Z }
contributors: [human:benlinton, agent:claude-opus-5]
horizon: later
scope: project
lifecycle: draft
---

# review-sweeps could be named for the pairing instead

**The proposal is `paired-review`.** The bundle is named for its traversal — a
sweep — and the thing it actually protects is the pairing. `the-pairing-turn`
puts it plainly: **"the reader's own read is the product."** Everything else
described here is scaffolding around that.

**The name currently advertises the scaffolding.** Somebody reading
`review-sweeps` cold learns that something gets swept, and learns nothing about
the one property the bundle exists to defend.

## What the current name is doing, which is not nothing

**`sweep` carries the completeness contract**, and there is a whole concept
document defending it: *an audit answers a question, a sweep covers a
territory.* **Coverage is what a sweep sells; a verdict is what an audit sells.**

**That distinction is under active pressure.** `sweeps-and-audits` opens by
saying the two *"look alike from a distance and the resemblance is getting
closer"* — which is why it was written down rather than re-derived each time.

**So `paired-review` has a specific cost: it makes them look more alike, not
less.** An audit is also a review, and also paired more often than not. The word
that currently keeps them apart is the word the rename removes.

## The name has two jobs and neither candidate does both

| | says how it is done | says what it owes |
| --- | --- | --- |
| `review-sweeps` | **no** | yes — coverage of a territory |
| `paired-review` | yes — the reader reads | **no**, and collides with `audit` |
| `paired-sweep` | yes | yes |

**`paired-sweep` is the obvious third option and is not obviously right either.**
It is accurate and slightly awkward, and *sweep* still needs the concept document
to explain it to anybody arriving cold. **A name that still needs a glossary has
not solved the problem the rename was for** — which is the same test that
retired `outfit`: a verb that always travelled with a translation was not doing
its work.

## What it would cost

**A bundle rename changes its ID**, so every adopter re-adopts under a new name
and every reference in prose moves. That is cheap today — the bundle is at
`0.25.0`, `lifecycle: draft`, `survival: experimental` — and it stops being cheap
the moment anything outside this catalog depends on the name.

**Which argues for deciding it soon rather than deciding it now.** The cost curve
is rising and the argument is not settled.

## What would settle it

**Watch which word people reach for when they are not reading the bundle.** If
they say *"do a sweep of the parser"* the current name is carrying its weight; if
they say *"let's pair on the parser"* it is not. **That is observable and nobody
has looked yet.**

*Related:* [[a-slice-could-cover-less-than-a-file]] — if a sweep can cover a
function rather than a file, the territory it sweeps gets smaller and less
territorial, which weakens `sweep` further and is worth deciding alongside this.
