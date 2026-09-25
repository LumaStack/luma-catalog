---
type: work-item
type_version: "0.0.2"
key: CATA-0010
title: Should catalog.md be catalog.yaml?
description: Unsettled, and the weaker of the two manifest cases, which makes it the more likely to move. A markdown document with a manifest at the top is the format's best property when the body carries something, and a YAML file wearing a costume when it does not — and CATALOG.md is now a short instance note over a manifest. Weighs what YAML would buy, a JSON Schema and one obvious parse, against what markdown buys, one parser across every document foreman reads and a type that makes the file discoverable. Split at migration from the BUNDLE.md half, because this one is decidable unilaterally and on no clock.
workflow_status: captured
rank: 010.0100.000
kind: idea
stage: draft
created: { by: human:luma-founder, at: 2026-08-18T00:00:00Z }
---

# Should catalog.md be catalog.yaml?

**Unsettled, and the weaker of the two manifest cases** — which makes it the more
likely to move.

The doubt is about files that are almost entirely frontmatter. A markdown
document with a manifest at the top is the format's best property when the body
carries something; it is a YAML file wearing a costume when the body does not.
After the general prose moved into `_types/catalog.md` where it belonged,
`CATALOG.md` is a short instance note over a manifest — close to the point where
the extension stops being honest.

**A catalog is pure configuration** — an index with obligations, read by one
tool, correct or not according to cross-field rules. That is unlike a bundle,
whose body has a real job.

What YAML would buy: a JSON Schema, which brings editor validation and
completion that frontmatter never gets; no ambiguity about whether the body is
normative; and one obvious parse. What markdown buys: one parser across every
document foreman reads, a `type` that makes the file discoverable by the same
tooling that reads bundles, and the self-describing property the whole format
rests on.

## Notes

Migrated from `luma-foreman/docs/IDEAS.md` on 2026-08-21. `created.at` is a
day-level estimate from git history.

**Split at migration** from the same entry as *should `BUNDLE.md` be YAML*, now
filed in `luma-knowledge-format`. The original treated them as one question while
observing that *"they may deserve different answers, and forcing symmetry is part
of what makes this feel wrong"* — which is the symmetry the single entry was
imposing.

**This half is decidable unilaterally, and that is the point of the split.**
`CATALOG.md` appears nowhere in the specification's reserved files. It lives at
`catalog/CATALOG.md` in this repository with its type defined in
`catalog/_types/catalog.md`, so changing it needs no format change, no version
bump elsewhere, and no deadline. The `BUNDLE.md` half is a breaking spec change
on a clock that expires at `1.0`; this one is not on any clock.

**The shared argument lives in both files** — what a body has to carry to earn
markdown. Worth keeping the two in sync if either is revisited.

## Related work

- Born from the idea it replaces: [`catalog-manifest-as-yaml`](../../ideas/catalog-manifest-as-yaml.md)
