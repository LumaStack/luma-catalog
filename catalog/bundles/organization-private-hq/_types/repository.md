---
type: type_definition
defines: repository
extends: document
fields:
  url:
    obligation: mandatory
    field_type: uri
    desc: "where the repository is. The one fact that makes the entry resolvable"
  in_scope:
    obligation: recommended
    field_type: enum
    values: [true, false]
    desc: "whether this headquarters reasons about it. Absent means undecided, which is different from false"
  access:
    obligation: optional
    field_type: enum
    values: [readable, restricted]
    desc: "whether the indexing account can read it. Absent means readable"
---

# repository

One repository the organization reasons about, and the minimum a headquarters
has to hold in order to reason about it.

**It is a cache with judgements attached, not a description.** The repository
describes itself; this points at it and records what the organization decided.

## Three fields, because everything else is either core or derivable

`url`, `in_scope` and `access` are the only things the format does not already
supply and no scan can produce.

**`url` is mandatory** because an entry that cannot be resolved is worse than
absent — it names something without letting anybody check it, which is how a
stale index survives.

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
| `lifecycle_status` | `archived` when the repository is retired |
| `created` | when the entry was added, and by whom |

**`description` carries unusual weight**, for the same reason it does on a
workflow: it is what a consumer reads to decide whether this is relevant at all,
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
