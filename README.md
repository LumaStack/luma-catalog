# luma-catalog

Universal bundles — standards, workflows, and types that any organization can
adopt, published so a project can pin one and not have it change underneath.

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
  project/         bundles that install into a repository
  organization/    bundles that install into an organization's headquarters
README.md          everything else here maintains the catalog
LICENSE
```

**Everything under `catalog/` is the catalog; everything outside it maintains
the catalog.** That boundary is structural rather than conventional so a program
consuming this repository has one unambiguous answer for where content starts,
and so a sparse checkout has one subtree to name. Documentation, contribution
guidance and continuous integration will accumulate at the root over time and
none of it is catalog content.

The inner split is not decoration either. A bundle describing how to argue a
standard into existence has nothing to install into a single repository; one
enforcing commit conventions has nothing to do at the organization level.
Keeping them in separate directories means adopting the wrong kind is impossible
rather than merely detectable, and it is why no bundle carries a field saying
which it is.

Nothing here declares how far it reaches, either. A bundle in this repository is
universal because this is the universal catalog. Promotion is a directory move
with nothing to edit and no way for a bundle to misstate its own reach.

`catalog/` is **not** a bundle, despite the shape. A bundle carries a mandatory
version, is copied wholesale, and contains documents; a catalog has no version,
is picked from rather than copied, and contains bundles.

## How this is consumed

Never resolved, always copied. There is no client, no API, and no version
solver — `luma-foreman` vendors a bundle into a project's `.hq/standards/`, and
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
configured with one catalog reads the chain, and what each list does when two
catalogs speak at once differs by list: vocabularies union, requirements resolve
most-restrictive-wins, and only starters carry an explicit `extends`, because
starters are the one list where subtracting something is a legitimate act.

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
