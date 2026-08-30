---
type: luma/idea
title: No bundles exist for linting, tests, CI or independent review
created: { by: human:benlinton, at: 2026-08-09T00:00:00Z }
contributors: [human:benlinton, agent:claude-opus-5]
horizon: later
scope: project
lifecycle: draft
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
