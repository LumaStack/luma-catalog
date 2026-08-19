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
    desc: "the decision that replaced this one — quoted (§8); set together with lifecycle_status: archived"
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
| retired | `lifecycle_status: archived`, no `superseded_by` |
| **rejected** | **no distinct expression — see below** |

Supersession is a **relationship, not a status** — §6 of the specification says
so directly — which is why `superseded_by` is a wikilink rather than a state.
That makes the successor reachable from the document a reader actually lands on.

`lifecycle_status` also governs **what you may edit**, not only how settled the
decision is. That ladder is in [[decision-guidelines]].

## Open: rejected has nowhere to live

**A decision that was considered and never adopted cannot be distinguished from
one that was adopted and later withdrawn.** Both are `archived`, and the only
difference is prose.

That gap matters more than it looks. **A rejected decision is the one that most
prevents re-litigation** — it is the record that answers *we thought about that
and here is why we did not*, which is exactly the question that returns every
few months. Filing it identically to something that was once in force loses the
distinction a reader needs first.

Three ways out, none chosen:

- A `rejected` value on `lifecycle_status`, which is a change to the format's
  core rather than to this type.
- A field on `decision` alone — cheap, and it means a general question gets a
  local answer that nothing else can reuse.
- `archived` with the rejection stated in the body. No new mechanism, and lossy:
  nothing can find rejected decisions without reading them.

Recorded rather than solved, because the right answer depends on whether other
document types need the same distinction — and none exist yet to ask.

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

The distinction that matters most in practice, because getting it wrong destroys
either the record or the reasoning. [[decision-guidelines]] covers what each
`lifecycle_status` permits; this is the field mechanics.

**Correct in place when the *record* was wrong** — a mistaken rationale, a claim
that does not hold, an example that was never true. The decision still stands;
what was written about it did not. Leave the correction visible and dated.

**Supersede when the *decision* changed.** Write a new record, set the old one's
`lifecycle_status: archived` and point `superseded_by` at the replacement:

```yaml
lifecycle_status: archived
superseded_by: "[[ADR-0012-catalogs-do-not-inherit]]"
```

**Quote it.** `[[…]]` is YAML flow-sequence syntax, so an unquoted wikilink
parses as a nested array rather than a string and no parser complains — the
record stays valid and the redirect simply never resolves. §8 of the
specification carries the warning; this is the field in this bundle most likely
to meet it.

The old reasoning stays readable, which is what lets someone see why the
position moved rather than only that it did.

ADR convention says an accepted decision is immutable and everything is a
supersession. That is right for reversals and heavy for errata — a typo in the
rationale does not warrant a new record and a redirect.
