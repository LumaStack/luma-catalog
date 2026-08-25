---
type: bundle
version: 0.2.0
published: 2026-08-25
consumers: [project]
entry_point: policy/merge-commits
description: How changes get integrated — merge commits rather than squash or rebase, and the repository settings that make it true.
---

# Git workflow

How changes land. Today that is one rule and the settings that enforce it;
branching and commit-message conventions are the obvious siblings and are not
here yet.

**It prescribes no branching model.** Nothing here says trunk-based, gitflow, or
anything between — only what happens at the moment a branch is integrated.

**It is not tied to a forge either.** The rule is a property of git: squash and
rebase produce commits that are ancestors of nothing, so merged-detection fails
on GitLab, Forgejo, Gitea and Bitbucket exactly as it does on GitHub. Only the
*enforcement* is host-specific, and the workflow says which host its commands
are for.

## What is here

- [[merge-commits]] — pull requests are integrated with merge commits, and why
  that survives the objection everyone raises. Read first.
- [[configure-merge-settings]] — disable squash and rebase at the forge, and
  verify they stayed disabled.

## Why this is a policy and not a preference

Squash and rebase merging **break the only reliable answer to "is this branch
merged?"** Both produce new commit SHAs, so a branch's commits never become
ancestors of the target, and every ancestry-based tool — `git branch --merged`,
forge auto-delete, every cleanup script — concludes it was never merged.

The branch then reads as unmerged forever, and stale branches accumulate until
somebody verifies each one by hand.

The cost is a non-linear `main`, which is the objection people actually have.
`git log --first-parent` recovers the linear view on demand — and that is the
asymmetry the policy rests on: **the prettier view is recoverable, and the
information squash destroys is not.**

## Consumers

`project` only. Merge strategy is a property of a repository, and an
organization's headquarters is a repository like any other rather than a level
this applies at.

## Version

`0.2.0` — **the manifest is `BUNDLE.md`.** Reserved markdown files are now
ALL CAPS across the estate, because nobody types all caps by accident: a file
becomes load-bearing only when somebody deliberately made it so, and writing
`bundle.md` now fails in the safe direction — ignored rather than silently wired
into machinery. Minor rather than patch, and pre-1.0 that is the tier for a
breaking change: anything naming the old path by hand stops resolving.

`0.1.0`. The reasoning comes from a repository that hit the stale-branch failure
twice in one week and changed strategy because of it — but this bundle has been
adopted nowhere, and the configuration workflow has been run against no forge
but GitHub.
