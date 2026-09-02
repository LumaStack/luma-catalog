---
type: type_definition
defines: repository
extends: document
fields:
  url:
    field_presence: required
    field_type: uri
    desc: "where the repository is. The one fact that makes the entry resolvable"
  in_scope:
    field_presence: recommended
    field_type: enum
    values: [true, false]
    desc: "whether this headquarters reasons about it. Absent means undecided, which is different from false"
  access:
    field_presence: optional
    field_type: enum
    values: [readable, restricted]
    desc: "whether the indexing account can read it. Absent means readable"
  attention:
    field_presence: optional
    field_type: enum
    values: [investing, steady, reducing, winding-down, undecided]
    desc: "how much the organization is putting in, and which way that is moving. Absent means nobody has said; `undecided` means somebody looked and could not say"
---

# repository

One repository the organization reasons about, and the minimum a headquarters
has to hold in order to reason about it.

**It is a cache with judgements attached, not a description.** The repository
describes itself; this points at it and records what the organization decided.

## What this adds, because everything else is core or derivable

`url`, `in_scope` and `access` are the only things the format does not already
supply and no scan can produce.

**`url` is mandatory** because an entry that cannot be resolved is worse than
absent — it names something without letting anybody check it, which is how a
stale index survives.

## `attention` is direction, and `lifecycle` is position

**They are two axes and neither substitutes for the other.** `lifecycle`
— core, from the format — says how far along a thing is: `draft`, `provisional`,
`stable`. `attention` says how much the organization is putting in: `investing`,
`steady`, `winding-down`.

**The combinations are the point.** *Stable and winding-down* is a successful
product being sunset; *draft and winding-down* is an experiment that did not work.
Fused into one field those are the same word, and they call for opposite
decisions.

**The scale measures what goes in, not what the repository is.** People, budget,
attention — more of it, level, less of it, or none:

| | |
| --- | --- |
| `investing` | more going in |
| `steady` | level |
| `reducing` | less going in, and staying |
| `winding-down` | going to zero |
| `undecided` | nobody has said which |

**`trimming` and `winding-down` differ by destination, not by rate.** Trimming has
no endpoint: still yours, still running, costing less. Winding-down is aimed at
zero. Something can be trimmed for years and be healthy, and can be wound down
gently and still be dying. **Filing a trimmed thing as winding-down reads as a
death sentence to everyone downstream**, which is the mistake this value exists
to prevent.

**`reducing` and `winding-down` differ by destination, not by rate.** Reducing has
no endpoint: still yours, still running, costing less. Winding-down is aimed at
zero. Something can be reduced for years and be healthy, and can be wound down
gently and still be dying. **Filing a reduced thing as winding-down reads as a
death sentence to everyone downstream**, which is the distinction this value
exists to protect.

**`reducing` rather than `trimming` or `narrowing`, deliberately.** Those name
*what* shrinks — resources for one, scope for the other — and the field does not
need to know: what is being reduced is whatever was going in. Saying less
carried more, and it removed a caveat about scope and resources being
independent axes.

**It names what the organization is doing, not what the repository is.** That is
why `investing` rather than `growing`: the other values describe decisions —
withdrawing, holding, not having decided — and a value describing the artifact
instead breaks the set. `investing` is also the true antonym of `winding-down`,
resources going in against resources coming out. *`building` was the other
finalist and lost on collision: in a repository index, beside a language and a
description, it reads as build status before it reads as intent.*

**`undecided` is the value that earns the field.** Absent means nobody has
looked. `undecided` means somebody looked and could not say — which is a real
state, often the most common one, and the only one that is actionable as a
question. A repository nobody has decided about is invisible without it.

**Terms that look like values and are not.** *Life support* is `stable` plus
`winding-down`, and adding it as a value would re-fuse the axes. *Retired* is
`lifecycle: archived`, which already exists. *Deprecated* is neither — it
is a public declaration to consumers, independent of both, and would be its own
field with a date if it is ever needed.

**A gap in the format, recorded rather than worked around.** `lifecycle`
is not purely position: `draft`, `provisional` and `stable` are points on a path,
but `archived` is a direction that already completed. So the format carries the
same conflation in miniature, and *stable, and being wound down* has no
representation there — you either misreport it as `stable` or jump to `archived`
before it is true. That is the gap this field fills.

**`in_scope` is what the index is actually for.** Nothing outside the
organization knows whether a repository matters to it, and no amount of scanning
will work it out. It is also what makes indexing idempotent: **a repository
excluded once stays excluded**, so the scan stops asking about the same forty
forks every time it runs.

**Absent is not `false`.** Undecided means nobody has looked, which is a state
worth finding; `false` means somebody looked and said no. Collapsing them turns
a backlog into a decision that was never made.

## `access` exists so that silence is never mistaken for absence

**An organization running least privilege will have repositories the indexing
account cannot read.** That is the permission model working. `access: restricted`
records the one thing that is still knowable: **it exists, and we cannot see
inside it.**

Without the field, an entry with no description is ambiguous in a way that
matters — *nobody has written one* and *nobody here may read it* call for
opposite responses. The first is a gap to offer to fill; the second is a
boundary to leave alone.

```yaml
access: restricted     # do not fetch, do not describe, do not conclude absence
```

**Absent means `readable`**, because it is mechanically true: if the description
was fetched, the repository could be read. There is no undecided state here.

**What it obliges a reader to do** is not conclude that a capability is missing.
An agent that cannot see a billing service and decides there is none proposes
building a second one — which is a worse outcome than knowing there is a door it
may not open. See [[knowing-without-access]] for the full argument, and for why
this is a default a security owner may overrule.

## The core fields carry the rest

| | holds |
| --- | --- |
| `description` | **when to load this repository's context** — the sentence that decides whether it is relevant |
| `sources` | where each derived value came from |
| `modified` | when it was last refreshed, and by which process |
| `stale_after` | when it should be rechecked |
| `lifecycle` | `archived` when the repository is retired |
| `created` | when the entry was added, and by whom |

**`description` carries unusual weight**, for the same reason it does on a
procedure: it is what a consumer reads to decide whether this is relevant at all,
before anything else is loaded. A repository whose description says *"internal
tooling"* will never be selected correctly.

Write it as the answer to **when should somebody open this?** — not as a summary
of what the code does.

## Derived values are cached, never authored

A repository's own facts belong to the repository. Description, language,
visibility, default branch, whether it is archived — every one has an
authoritative source elsewhere, and **a copy with no source is
indistinguishable from something somebody typed.**

So a cached value carries `sources`, and `modified.by` is the process that
fetched it:

```yaml
sources: [{ from: "github:acme/acme-web", field: description }]
modified: { by: process:index-repositories, at: 2026-08-20T09:00:00Z }
stale_after: 2026-11-20
```

That is what makes refreshing safe. Without it nobody can tell a fetched value
from a considered one, so nobody dares overwrite it and it ages into fiction.

## What does not go here

**Anything a pointer would answer.** If following the `url` gives it in ten
seconds, the entry does not need it. An index carrying everything is an index
nobody refreshes, because refreshing it becomes a project.

**Anything that belongs to the repository.** A rule about how it is built, its
changelog, its own decisions — those live there, and duplicating them here
creates two answers that will disagree.

The test: **would a wrong value here cause a wrong decision at the organization
level?** If not, leave it out.
