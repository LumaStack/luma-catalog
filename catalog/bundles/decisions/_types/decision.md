---
type: type_definition
defines: decision
fields:
  decided:
    obligation: mandatory
    field_type: date
    desc: "when the decision was settled — not when the document was created"
  reopen_trigger:
    obligation: recommended
    field_type: text
    desc: "what would have to become true for this to be worth revisiting"
  superseded_by:
    obligation: optional
    field_type: wikilink
    desc: "the decision that replaced this one; set together with lifecycle_status: archived"
---

# Decision

One settled position and the reasoning that settled it. One file per decision.

Follows the [Architecture Decision Record](https://adr.github.io/) conventions
even where the decision is not architectural — the shape holds for any decision
worth keeping, and borrowing an established convention costs nothing.

## The fields it does not declare

`lifecycle_status`, `created`, `modified` and `verified` all arrive from the
root type, and between them they cover what an ADR calls *status*:

| ADR status | here |
| --- | --- |
| proposed | `lifecycle_status: draft` or `provisional` |
| accepted | `lifecycle_status: stable` |
| superseded | `lifecycle_status: archived` plus `superseded_by` |
| deprecated | `lifecycle_status: archived` |

Supersession is a **relationship, not a status** — §6 of the specification says
so directly — which is why `superseded_by` is a wikilink rather than a state.
That makes the successor reachable from the document a reader actually lands on.

## `decided` is not `created`

A decision can be drafted for a week and settled in a meeting. `created` records
when the file appeared; `decided` records when the position became binding. They
are frequently different and only one of them is the fact people cite.

## What a record contains

The frontmatter is the smaller half. The body carries the argument, and the
sections below are the working shape rather than a mandated template:

- **What was decided**, stated first and plainly.
- **Why it matters** — what breaks if this is got wrong.
- **How to apply it** — what someone does differently now.
- **Deferred alternatives**, each with a re-open trigger. A path not taken is
  **deferred, never rejected**: recording it as rejected discards the reasoning
  and invites the same argument again from scratch.
- **Standing consequences** — what this now forbids or requires elsewhere.

## Correcting versus superseding

The distinction that matters most in practice, because getting it wrong
destroys either the record or the reasoning:

**Correct in place when the *record* was wrong** — a mistaken rationale, a claim
that does not hold, an example that was never true. The decision still stands;
what was written about it did not. Leave the correction visible and dated rather
than editing silently, because the fact that it was wrong is often more
instructive than the fix.

**Supersede when the *decision* changed.** Write a new record, set the old one's
`lifecycle_status: archived` and point `superseded_by` at the replacement. The
old reasoning stays readable, which is what lets someone see why the position
moved rather than only that it did.

ADR convention says an accepted decision is immutable and everything is a
supersession. That is right for reversals and heavy for errata — a typo in the
rationale does not warrant a new record and a redirect.
