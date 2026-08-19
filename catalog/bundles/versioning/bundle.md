---
type: bundle
version: 0.1.0
published: 2026-08-19
consumers: [project, organization]
entry_point: policy/semantic-versioning
description: What a version number promises, when to bump which part, and the rules that get decided wrongly — for anything versioned, not only releases.
---

# Versioning

**A version is a promise about what upgrading costs.** Not a signal of how
significant the work felt, not a marketing decision — a statement about what
happens to somebody who upgrades without reading anything.

That single idea decides every hard case: a large release that breaks nothing is
a minor, and a one-line change to a default is a major.

## What is here

- [[semantic-versioning]] — the three parts, what breaking means for different
  kinds of artifact, the pre-`1.0.0` rules, the `v`-prefix boundary, and
  deprecating before removing.

## Why this is not part of the release bundle

It was, and that was a misfiling. **Releasing is one consumer of versioning, not
its owner.** A bundle carries a version whether or not anybody ever cuts a
release; so does a schema, a package, an API, a format.

Leaving it there meant a project that versions things but never publishes
releases had to adopt a release bundle to find out what a minor bump means. The
evidence that this was wrong is that another bundle re-derived the rules
independently rather than reach for it.

## How other bundles use this

**By pointing at it, never by needing it.** A bundle that versions something
keeps the operative rule — the three-line table, enough to act — and points here
for the reasoning, the edge cases, and the parts that get decided wrongly.

That is the line: **a bundle may reference another for depth, never for
capability.** Remove this bundle and every other one still works; readers just
lose the argument behind the rule. Three duplicated lines everyone already knows
cost nothing. A hundred lines of reasoning duplicated is where drift lives.

If you want adopters to get both, that is what a catalog's `requires` and
starters are for. Composition belongs to the catalog, not to bundles.

## Consumers

Both levels. An organization versions its published standards and its own
catalog contents; a project versions its packages, schemas and bundles. The
rules are identical.

## Version

`0.1.0`. Extracted from a release bundle where it had been working, so the
content is exercised — but it has never been read by somebody versioning
something that is not a release, which is the case the extraction exists for.
