# luma-catalog

> **Policies, workflows and knowledge that give your agents superpowers.**<br>
> Drop in best practices, move faster together, and get things right the first time.

A catalog of shared bundles containing policies, workflows, and knowledge
that any organization can adopt — versioned and vendored, so you're in control.
Use our catalog, or run your own alongside it.

[Browse the bundles](catalog/bundles).

## What a bundle is

A [Luma Knowledge Format](https://github.com/LumaStack/luma-knowledge-format)
Bundle: a self-contained directory of typed markdown documents, plus whatever
assets they reference, describing itself at its root with a `version`.

**No bundle here depends on another**, so adopting one is copying a directory —
there is nothing to resolve and no order to install in. That is the current
model rather than a promise about the future: whether bundles should ever
declare dependencies is
[an open design question](https://github.com/LumaStack/luma-leader), and the
position is *not yet* rather than *never*.

**Verifying is three things, and only one of them is the checksum.** The
checksum says the vendored copy is byte-for-byte what was adopted. Whether the
bundle is internally sound, and whether the catalog holding it is
self-consistent, are separate checks that run before anything is published —
see below.

A policy, a workflow, and a set of type definitions are all bundles. They
differ in what they contain, not in how they travel.

## Layout

```
catalog/
  catalog.md       the namespace, the vocabulary, the starters, the requirements
  bundles/         one directory per bundle, flat
.github/           the checks that gate a merge — see Contributing
docs/
README.md          everything else here maintains the catalog
LICENSE
```

**There is no `_types/` beside `catalog.md`.** The contract for
`type: luma/catalog` is published in the `luma/luma-types` bundle and referenced
from here rather than copied — *reference within a repository, vendor across
them*. A second copy in this repository would have nothing keeping it in step,
and the one that briefly existed had already drifted a version before it was
removed.

`catalog.md` holds only what is true of *this* catalog. Everything general —
what each field means, how two catalogs resolve, what `mandatory` does — lives
in [`catalog/bundles/luma-types/_types/catalog.md`](catalog/bundles/luma-types/_types/catalog.md), so it is written
once rather than copied into every catalog that ever exists.

**Everything under `catalog/` is the catalog; everything outside it maintains
the catalog.** That boundary is structural rather than conventional so a program
consuming this repository has one unambiguous answer for where content starts,
and so a sparse checkout has one subtree to name. Documentation, contribution
guidance and the continuous integration that gates this repository live at the
root, and none of it is catalog content.

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
solver — `luma-foreman` vendors a bundle into a project's
`.luma/bundles/<org>/<name>/`, and the vendored copy is the lockfile. That is
the whole distribution model, and it is deliberate: a project must keep working
from a bare clone with no network.

## Where this sits

| repository | kind | |
| --- | --- | --- |
| [`luma-leader`](https://github.com/LumaStack/luma-leader) | engine | argue policies into existence |
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
[`catalog/bundles/luma-types/_types/catalog.md`](catalog/bundles/luma-types/_types/catalog.md) for how each list
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

### Merging is publication

There is no release step and no tag. **A bundle becomes available by being on
`main`**, which is why everything that could refuse it has to run before the
merge rather than after.

Every pull request runs two tools, and a red run blocks the merge.

[`luma-catalog-curator`](https://github.com/LumaStack/luma-catalog-curator)
checks whether the catalog **agrees with itself** — a bundle both mandated and
deprecated, a starter naming something nobody publishes, a requirement tagged
outside the published vocabulary. Those are contradictions no single project
could ever detect.

[`luma-foreman`](https://github.com/LumaStack/luma-foreman) checks whether **any
one bundle is broken in a way the format tolerates** — a dangling link, an
unquoted wikilink in frontmatter, a template carrying live frontmatter. All
three are conformant, so without this they publish cleanly and travel to every
adopter.

**The one that catches most contributors: change a bundle and its version has to
move.** The check compares your branch against its base and reports any bundle
whose files changed while `version` in its `bundle.md` did not. An adopter
decides whether to take a change by comparing versions, so a change that does
not move the number is a change nobody downstream can see.

The tier is yours to judge. A patch that edits a normative sentence, or a
non-major release that removes a document, is **surfaced as a notice rather than
refused** — a second reader, not a gate.

## License

Licensed under the [Apache License, Version 2.0](LICENSE).
