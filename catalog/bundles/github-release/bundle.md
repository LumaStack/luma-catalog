---
type: bundle
version: 0.1.2
published: 2026-08-18
consumers: [project]
entry_point: workflows/publish-release
description: Cutting and publishing GitHub releases — choosing the version, the changelog, release titles and contents, and the gh workflow.
---

# GitHub release

Releasing is where a project's care becomes visible to people who will never
read its source. A version number is a promise about what upgrading costs, and
release notes are usually the only account of a change anyone ever reads.

Both are easy to get wrong in ways that are invisible at the time and expensive
later — a breaking change shipped as a minor, a tag pushed with no release
against it, notes that list commits instead of consequences.

## What is here

- [[publish-release]] — the workflow. Verifies `gh` is installed,
  authenticated and working *in this repository* before anything is tagged.
- [[release-versions]] — which part to bump, and the two cases that must be said
  out loud. Enough to cut a release; the reasoning is in the **versioning**
  bundle, worth adopting alongside and not required by this one.
- [[release-notes]] — what a release is called and what it must contain.
- [[changelog]] — `CHANGELOG.md`, following Keep a Changelog, and how it differs
  from release notes.
- [the release notes template](templates/release-notes.md) — the required
  sections in order, with the reasoning in comments.

## Project only

`consumers: [project]` — releasing is a repository activity. An organization's
headquarters is a repository too, but it is not something you cut versions of.

## Loading

Only [[publish-release]] is `preload: mandatory`. The two policies are
`optional`: they are read when the workflow points at them or when someone
questions a version number, not held in context against the possibility.

## The one hard requirement

The workflow **stops** if `gh` is missing rather than falling back to the web
interface or a raw API call. The first produces a release nobody can reproduce;
the second needs a token that then has to live somewhere.

When it stops it **asks** whether to install `gh` or leave that to you, and
waits. Installing software is outside what "publish a release" implies, harder
to undo than anything else in the workflow, and on a managed machine it may not
be yours to do.

## Version

`0.1.2` — a heading no longer says how many things are beneath it. Wording only.

Patch: no normative sentence moved and a reader who correctly understood
`0.1.1` behaves identically. See `writing-style` in `luma/project-documentation`
for the rule and the failure it prevents.

`0.1.1` — *standard* becomes *policy*. Wording only: `policy` is the document
type the format defines and the word this estate uses everywhere else, and
`standard` was deliberately freed for the organization level rather than left
doing double duty.

Patch because a reader who correctly understood `0.1.0` behaves identically.
The subject noun changed; nothing it requires, permits or forbids did.

`0.1.0`. The conventions here are drawn from releases actually cut rather than
imagined, but the workflow's `gh` handling has not yet been run against a
machine that does not have it — which is the case it exists for.
