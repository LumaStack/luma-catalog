---
type: bundle
version: 0.1.0
published: 2026-08-18
consumers: [project, organization]
entry_point: policy/organizing-a-bundle
description: Creating, updating, auditing, repairing, migrating and retiring bundles — the layout they use and which catalog they belong in.
---

# Bundle manager

Bundles are cheap to write and easy to write badly, and the failures are quiet.
A broken link, an unquoted wikilink in frontmatter, a template with frontmatter
that a tool reads as a real document — none of these produce an error. The
bundle stays conformant, adopters copy it, and the defect travels.

This bundle carries the layout every bundle uses, the rule for which catalog one
belongs in, and a procedure for each thing you do to a bundle over its life.

## What is here

**Policy**

- [[organizing-a-bundle]] — the layout, and the three rules that decide whether
  something is a document, an asset, or a type. Read first.
- [[where-a-bundle-belongs]] — project, organization, or universal, and how a
  bundle moves between them.

**Workflows**

- [[create-bundle]] — scaffold a new one and get it publishable.
- [[update-bundle]] — change contents and version the change honestly.
- [[audit-bundle]] — the checklist for defects that fail silently.
- [[repair-bundle]] — fix findings in an order that avoids making it worse.
- [[migrate-bundle]] — promote between catalogs, or restructure in place.
- [[delete-bundle]] — retire one without stranding its adopters.

**Templates**

- [the bundle manifest](templates/bundle.md)
- [a Type Definition](templates/type-definition.md)

Both are assets carrying **fenced** examples rather than real frontmatter. A
manifest template with live frontmatter is a second bundle manifest inside this
bundle, and every tool reading it would believe that — which is the first thing
[[organizing-a-bundle]] warns about, so this bundle had better not do it.

## Loading

Only [[organizing-a-bundle]] is `preload: mandatory` — every workflow here
assumes it. The six workflows are `optional`: you load the one you are doing,
not all six.

That is the field working as intended. Marking every workflow mandatory would
impose the whole bundle on any consumer that touched it, which is the cost that
keeps `mandatory` meaning something.

## Consumers

Both levels. An organization curates a catalog and a project writes bundles it
may later promote, and the procedure is the same at either end.

## Version

`0.1.0`. These conventions were extracted from writing three bundles in one
afternoon — real practice, but not much of it, and the audit checklist in
particular has never been run against a bundle somebody else wrote.
