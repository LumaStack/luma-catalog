---
type: work-item
type_version: "0.0.2"
key: CATA-0008
title: No bundles exist for linting, tests, CI or independent review
description: A new project should get the standard tooling installed — linting, tests, continuous integration, independent review, a backlog — and four of those five have no bundle behind them. luma-foreman's outfit is the mechanism that installs tooling into a project and its scope is settled; what it would install does not exist, and a working mechanism with nothing to install is not a capability.
workflow_status: captured
rank: 010.0080.000
kind: idea
stage: draft
created: { by: human:luma-founder, at: 2026-08-09T00:00:00Z }
---

# No bundles exist for linting, tests, CI or independent review

A new project should get the standard tooling installed — linting, tests,
continuous integration, independent review, a backlog. Four of those five have no
bundle behind them.

## The problem it addresses

`luma-foreman`'s `outfit` is the mechanism that installs tooling into a project,
and its scope is settled. What it would install does not exist: of the fifteen
bundles in this catalog, none covers linting, tests, continuous integration, or
independent review. A working mechanism with nothing to install is not a
capability.

## Notes

Captured originally in `luma-foreman/docs/IDEAS.md` as the one-line entry
*"Install the standard tooling — linting, tests, continuous integration,
independent review, a backlog."* Retitled during migration, because the original
framing names a mechanism that is already scoped rather than the gap that is
actually open.

Checked at migration time:

- `luma-foreman/docs/scope.md` records *"outfit knows what tooling to install →
  now lives in `git-workflow`, `github-release`, `git-secrets`"*. Those three do
  not cover the five things this entry names.
- `audit-records` is adjacent to *independent review* but is a record format
  rather than a review practice.
- `backlog-ideas` covers the fifth item partially, and says in its own notes that
  the proper backlog does not exist yet.

## Related work

- Born from the idea it replaces: [`bundles-for-linting-tests-ci-and-review`](../../ideas/bundles-for-linting-tests-ci-and-review.md)
