---
type: luma/idea
type_version: "0.1.0"
title: catalog and project become ruleset bundles
created: { by: human:benlinton, at: 2026-09-20T00:00:00Z }
contributors: [human:benlinton, agent:claude-fable-5]
horizon: next
scope: organization
stage: draft
---

# `catalog` and `project` become ruleset bundles

**Pull `luma/catalog` and `luma/project` out of `luma-types` into their own
bundles: `catalog-ruleset` and `project-ruleset`.** Each one owns everything
needed to keep its file the way it should be — the Type Definition, the
template, the create/update practice, and the checks a linter enforces. Not a
description of the file; the rules the file is held to.

## The word, and how it was reached

**`ruleset`, settled provisionally on 2026-09-20.** The hunt matters more than
the winner, so the trail is recorded: *descriptor* undersold it — a descriptor
sounds like something you cannot mess up, and this exists to be followed.
*Definition* collides fatally with `type_definitions/` and `DEFINITION.md`,
which the estate made load-bearing the same week. *Standard*, *policy*,
*contract*, *mandate*, *protocol*, *charter*, *canon* were bearings, not
names — policy and contract are already estate vocabulary, and the rest turn
ceremonial in the compound. The register that fit was the working document —
spec, ruleset, standard — and `ruleset` won because it is binding by
definition (rules are followed or violated, never explained), natural in the
compound, collision-free, and operationally real: it is literally what a
linter loads and enforces, so `luma-foreman inspect` reading its checks from
`project-ruleset` makes the name a description of the mechanism.

## The taxonomy this instantiates

Bundles come in kinds: **manager bundles** (help use tooling or act as it —
`bundle-manager`, `session-manager`, `catalog-manager` when it is built),
**policy/procedure bundles** (adopted judgment — `git-workflow`,
`versioning`), and **ruleset bundles** — the kind that helps manage a file:
its contract, why it exists, how it is formatted and used, and the hooks for
keeping it that way. The seven `*-records` bundles and `backlog-ideas` already
have this shape (type + policy + procedure + templates); `project-documentation`
already plays the role for `PROJECT.md`. `CATALOG.md` is the one root file
with no ruleset bundle at all — its type sits on the `luma-types` shelf with
no practice around it.

## What executing this decides

- **Two bundles, not one.** The adopter sets are disjoint: a project needs
  `project-ruleset` and never `catalog-ruleset`; a catalog the reverse.
- **They live in this catalog, never in a tool's repo.** foreman, curator and
  leader are all consumers; a shared contract under one consumer's roof is the
  "whichever needed it first" problem `luma-types` was built to avoid.
- **Whether a ruleset bundle owns its contract.** If `catalog-ruleset` owns
  `luma/catalog` rather than vendoring it, the same logic dissolves
  `luma-types` entirely — `backlog-ideas` owns `luma/idea`,
  `tutorial-workflow-maker` owns the tutorial types,
  `project-documentation` (or `project-ruleset`) owns `luma/project`, and
  "shared type" comes to mean "vendored from its ruleset bundle." That
  contradicts the neutral-shelf doctrine `luma-types` states; the taxonomy is
  a real answer to it, but dissolving `luma-types` is its own decision with
  its own record.
- **`project-documentation`'s fate** — it already carries the `luma/project`
  practice. Either it is renamed/refit as `project-ruleset`, or the ruleset
  bundle is split out of it and it keeps the README-writing practice.
- **Validation rules ride along.** The foreman linter brief wants per-kind
  checks written against the LKF spec's validation table; a ruleset bundle is
  where those checks travel with adoption.

**`catalog-manager/` remains reserved** (ruled 2026-09-20): it becomes the
manager bundle for running catalogs. `catalog-ruleset` would sit beside it —
the practice and the law of the file are different bundles of different kinds.

Sequenced after the `type_definitions` migration wave, which completed
2026-09-20 across all six estate repositories.
