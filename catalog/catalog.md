---
type: catalog
description: Universal bundles — the starting set any organization can adopt.
tags:
  - service
  - library
  - infrastructure
  - design
  - docs
starters:
  project: []
  organization: []
requires: []
---

# The universal catalog

This file is the catalog's manifest. It declares three things, and nothing else
in this repository is authoritative about any of them.

## `tags` — the vocabulary projects may declare

A project states what it is in its own `.hq/standards/foreman.toml`, and
starters and requirements key on those values. The vocabulary is published here
rather than left free-form for one reason: if one repository declares `infra`
and another `infrastructure`, a requirement silently fails to apply to the
second, and everything still reports green. A requirement that does not fire is
the worst failure available here, so a tag outside this list is an error rather
than a miss.

An organization declares its own tags in its own catalog, and the two
vocabularies **union** — nothing is inherited and nothing needs declaring. A tag
nobody uses is inert, so subtracting one would buy nothing. An organization is
free to use none of these.

The list above is provisional. Nothing uses it yet, and the right vocabulary is
the one that falls out of real bundles rather than the one guessed at first.

## `starters` — what a new thing begins with

Two named lists, matching the two directories: what a new project starts with,
and what a new organization headquarters starts with.

Starters are **never retroactive**. Changing one changes what the *next* thing
begins with and touches nothing that already exists. That is what lets defaults
evolve without every edit becoming a fleet-wide migration — and it is why
anything meant to reach existing projects belongs in `requires` instead.

A starter entry may pin a version and usually does not. Unpinned takes the
latest at the moment of bootstrap, and the adopting project records what it got.

## `requires` — what projects must or should adopt

Each entry names a bundle, an obligation, an optional version constraint, an
optional `by` date, and optional tags limiting which projects it reaches:

```yaml
requires:
  - bundle: luma/change-review
    obligation: mandatory
    version: ">= 2.0.0"
    by: 2026-10-01
    tags: [infrastructure]
```

| obligation | effect |
| --- | --- |
| `mandatory` | must be adopted — a countdown until `by`, a failure after; with no date, a failure immediately |
| `recommended` | reported as a gap, never fails |
| `optional` | a curated shortlist; never reported as missing |
| `deprecated` | reported if still adopted |

A bundle may appear more than once. Every entry whose tags match a project
applies, and the strongest obligation among them is the one in force — so
"mandatory for infrastructure, recommended for everyone else" is two entries
rather than a conditional. The same rule resolves conflicts between this catalog
and an organization's: an organization may raise a recommendation, and may not
lower a mandate.

**Obligation governs whether a project must adopt a bundle. It never governs how
hard conformance is checked once it has.** A recommended bundle a project chose
to adopt is checked exactly as strictly as a mandated one.

## `upstream` — where else to look

Absent here, because this is the root of the chain. A downstream catalog names
the one it sits below:

```yaml
upstream: https://github.com/LumaStack/luma-catalog
```

It is a **source pointer, not inheritance.** A project configured with one
catalog reads the whole chain, which is why an organization's projects need
naming only their organization's catalog. Single-valued and acyclic — a linear
chain is cheap to walk, and a graph is the resolution problem bundles were
designed to avoid.

What happens when two catalogs speak at once differs by list, and there is no
catalog-level inheritance to declare:

| list | when two catalogs speak |
| --- | --- |
| `tags` | union — extra tags are inert |
| `requires` | most-restrictive-wins — extra requirements are the safe direction |
| `starters` | explicit `extends` / `adds` / `excludes` |

Only starters need declaring, because they are the only list where subtracting
something is a legitimate act. A starter fires once at bootstrap with no ongoing
check to catch a bad inclusion, so it needs an owner rather than a merge rule.

## Not settled

`type: catalog` has no Type Definition yet. That is legal — the Luma Knowledge
Format never rejects an unrecognized type — and deliberate: the shape should be
described once it has survived real use rather than specified from a guess.

Nothing here carries a version. A catalog version would imply its entries are
guaranteed against one another, which is what a distribution release buys and
only because its entries have dependencies. Bundles have none. "What did this
catalog hold on a given date" is a commit identifier.
