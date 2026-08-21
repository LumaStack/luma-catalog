# luma-catalog

**Standards, workflows and knowledge that give your agents superpowers.**
Drop in best practices, move faster together, and get things right the first time.

A catalog of universal bundles containing standards, workflows, and knowledge
that any organization can adopt, published so a project can pin one and not have
it change underneath. Use our catalog, or run your own alongside it.

> **Status:** seed. The shape is settled; the shelves are empty.

## What a bundle is

A [Luma Knowledge Format](https://github.com/LumaStack/luma-knowledge-format)
Bundle: a self-contained directory of typed markdown documents, plus whatever
assets they reference, describing itself at its root with a `version`. Not a
package — bundles never depend on one another, so adopting one is copying a
directory and verifying one is a checksum over it.

A standard, a workflow, and a set of type definitions are all bundles. They
differ in what they contain, not in how they travel.

## Layout

```
catalog/
  catalog.md       the vocabulary, the starters, and the requirements
  _types/          Type Definitions — what `type: catalog` declares, and why
  bundles/         one directory per bundle, flat
README.md          everything else here maintains the catalog
LICENSE
```

`catalog.md` holds only what is true of *this* catalog. Everything general —
what each field means, how two catalogs resolve, what `mandatory` does — lives
in [`catalog/_types/catalog.md`](catalog/_types/catalog.md), so it is written
once rather than copied into every catalog that ever exists.

**Everything under `catalog/` is the catalog; everything outside it maintains
the catalog.** That boundary is structural rather than conventional so a program
consuming this repository has one unambiguous answer for where content starts,
and so a sparse checkout has one subtree to name. Documentation, contribution
guidance and continuous integration will accumulate at the root over time and
none of it is catalog content.

Inside, bundles are **flat**, and each declares in its `bundle.md` which kinds
of consumer may adopt it:

```yaml
consumers: [project, organization]
```

An earlier layout sorted bundles into `project/` and `organization/`
directories. That was wrong: some bundles genuinely belong at either level
depending on the adopter — a decision record or an incident process is wanted
centrally by one organization and per-repository by another — and a directory
can only ever say one. It also put a choice that belongs to the adopter in the
hands of the publisher, permanently.

**A bundle's path is its identity for adoption.** Anything in the path becomes
unchangeable without breaking every pin, manifest entry and adopt command that
refers to it — so the path carries only what is single-valued and permanent.
Which catalog a bundle sits in qualifies, and that is why a bundle declares
nothing about its own origin: it is universal because this is the universal
catalog, and promotion is a directory move with nothing to edit.

`catalog/` is **not** a bundle, despite the shape. A bundle carries a mandatory
version, is copied wholesale, and contains documents; a catalog has no version,
is picked from rather than copied, and contains bundles.

## How this is consumed

Never resolved, always copied. There is no client, no API, and no version
solver — `luma-foreman` vendors a bundle into a project's `.luma/policy/`, and
the vendored copy is the lockfile. That is the whole distribution model, and it
is deliberate: a project must keep working from a bare clone with no network.

## Where this sits

| repository | kind | |
| --- | --- | --- |
| [`luma-hq`](https://github.com/LumaStack/luma-hq) | engine | argue standards into existence |
| [`luma-foreman`](https://github.com/LumaStack/luma-foreman) | engine | apply them, one repository at a time |
| `luma-catalog` | content | this repository — universal bundles |
| your organization's hq | content | your governance, learnings, analysis |
| your organization's catalog | content | your bundles, and what you mandate |

Engines are installed and pinned. Content is owned. **Nothing here is forked** —
an organization's catalog is its own repository that names this one as its
`upstream`, not a copy of it that drifts. If adopting something appears to
require a fork, that is a defect worth reporting rather than a workflow.

`upstream` points at where else to look; it does not inherit content. A project
configured with one catalog reads the whole chain — see
[`catalog/_types/catalog.md`](catalog/_types/catalog.md) for how each list
resolves when two catalogs speak at once.

## Contributing

A bundle reaches this catalog by promotion, one step at a time: it is written in
a project, promoted to an organization's catalog once a second project wants it,
and offered here once it is useful to organizations that share nothing with
yours. Skipping the middle step means bundles arrive that nobody has stood
behind.

What belongs here is anything that would help an organization with no connection
to Luma. Anything naming your customers, your systems, or your people belongs in
your own catalog.

## License

Licensed under the [Apache License, Version 2.0](LICENSE).
