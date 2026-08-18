---
type: type_definition
defines: catalog
fields:
  tags:
    obligation: recommended
    field_type: list of text
    desc: "the vocabulary a project may declare about itself"
  starters:
    obligation: optional
    desc: "named lists of bundles a new project or hq begins with — see below"
  requires:
    obligation: optional
    desc: "obligations, with optional version constraints, deadlines and tags — see below"
  upstream:
    obligation: optional
    field_type: uri
    desc: "the catalog this one sits below; where else to look, not content to inherit"
---

# Catalog

A catalog publishes bundles and says how strongly projects should adopt them. A
document with `type: catalog` sits at the root of a catalog's content directory
and is the only thing in that repository authoritative about any of the four
fields above.

**Two of them are declared without a `field_type`, deliberately.** `starters`
and `requires` are nested records, and §10.2 has no user-definable object shape —
`actor_event` is a fixed built-in, not a pattern to follow. Declaring the fields
without describing their shape is legal and buys the half that matters:
discovery. What the shapes are is documented here instead.

Whether the format should gain a structured field type is an open question
raised from this case, not a defect in this definition.

## `tags`

A project states what it is in its own `foreman.toml`, and both `starters` and
`requires` key on those values.

The vocabulary is published rather than free-form for one reason: if one
repository declares `infra` and another `infrastructure`, a requirement silently
fails to apply to the second and everything still reports green. **A requirement
that does not fire is the worst failure available here**, so a tag outside the
published vocabulary is an error rather than a miss.

A tag list means *any*. `tags: [design, infrastructure]` matches a project
tagged either one, never both-and-only-both. When both are genuinely required
the answer is a new tag the project declares, not a boolean the catalog
evaluates — that way the composite category acquires a name, someone must claim
it in a committed file, and it can be argued with.

## `starters`

Named lists, conventionally `project` and `organization`, matching the two
content directories.

```yaml
starters:
  project:
    extends: luma/project
    adds:
      - bundle: acme/deploy-checks
        version: "0.2.3"
      - bundle: acme/incident-response
    excludes:
      - luma/adr-workflow
```

**Starters are never retroactive.** Changing one changes what the *next* thing
begins with and touches nothing that already exists. That is what lets an
organization evolve its defaults freely, and it is why anything meant to reach
existing projects belongs in `requires` instead.

They are called starters rather than defaults for that reason: a default is an
ongoing fallback consulted every time, and this fires once.

**Pins are optional and unpinned is the common case.** An entry with no version
takes the latest at the moment of bootstrap, and the adopting project records
what it got. Pinning uses the same constraint syntax as `requires`, because the
motivating case — holding new projects back from a bad upstream release — wants
a ceiling rather than a freeze.

## `requires`

```yaml
requires:
  - bundle: luma/change-review
    obligation: mandatory
    version: ">= 2.0.0"
    by: 2026-10-01
    tags: [infrastructure]
```

| `obligation` | effect |
| --- | --- |
| `mandatory` | must be adopted — a countdown until `by`, a failure after; with no date, a failure immediately |
| `recommended` | reported as a gap, never fails |
| `optional` | a curated shortlist; never reported as missing |
| `deprecated` | reported if still adopted |

A bundle may appear more than once. Every entry whose tags match a project
applies and the strongest obligation among them is in force, so "mandatory for
infrastructure, recommended for everyone else" is two entries rather than a
conditional.

**Obligation governs whether a project must adopt a bundle. It never governs how
hard conformance is checked once it has.** A recommended bundle a project chose
to adopt is checked exactly as strictly as a mandated one — drift is drift. What
`recommended` buys is the freedom not to adopt it at all.

## `upstream`

A source pointer: where else to look, not content to inherit. A project
configured with one catalog reads the whole chain, which is why an
organization's projects name only their organization's catalog.

Single-valued and acyclic. A linear chain is cheap to walk; a graph is the
resolution problem bundles were designed to avoid, arriving through a side door.

**There is no catalog-level inheritance**, and what happens when two catalogs
speak at once differs by list:

| list | resolution |
| --- | --- |
| `tags` | union — extra tags are inert |
| `requires` | most-restrictive-wins — an organization may raise a recommendation, never lower a mandate |
| `starters` | explicit `extends` / `adds` / `excludes` |

Only starters need declaring, because they are the only list where subtracting
is a legitimate act. Merge additively where more is safe; require explicit
inheritance where subtraction is legitimate.

## No version

A catalog carries none. A version would imply its entries are guaranteed against
one another, which is what a distribution release buys and only because its
entries have dependencies. Bundles have none. "What did this catalog hold on a
given date" is a commit identifier.

## What validation does not cover

A catalog can be internally contradictory in ways no per-field check reaches: a
bundle both mandated and deprecated, or a starter pinning a version the same
catalog's own mandate forbids, which would make every new project born failing.
These are cross-field rules, belong to the tool reading the catalog, and are
caught where the catalog is published rather than where it is applied.
