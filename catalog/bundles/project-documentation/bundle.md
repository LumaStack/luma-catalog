---
type: bundle
version: 0.1.0
published: 2026-08-19
consumers: [project]
entry_point: policy/readme
description: The prose a repository publishes — where it lives, what a README is for, and which documents are worth having at all.
---

# Project documentation

The documentation a repository publishes about itself: the front door, the guide
for a newcomer, the explanation of why it is shaped this way. Not the store, not
the records, not the changelog — those belong to other bundles and this one says
so out loud.

**Every document is a liability until somebody reads it.** It has to be kept
true, and a stale document is worse than a missing one — missing is honest,
stale is confidently wrong. So the governing question here is never *what should
we have*, it is **what condition have we hit**.

## What is here

- [[readme]] — what a README is for, the four-section default, and what belongs
  somewhere else. Read first.
- [[which-document]] — the documents most projects can have, and the condition
  that earns each one.
- [[documentation-layout]] — prose goes in `docs/`; what stays at the root and
  why.
- [[add-document]] — the workflow: is it needed, is it ours, which kind, where.
- [the README template](templates/readme.md)

## The README default

A strong suggestion, not a rule: **a hook and what it is · why it exists · an
optional example · links to everything else.** Four sections, in that order.

A README is a front door, not a manual. Most people who open one are deciding
whether to keep reading at all — so the limit is the feature, and everything
past those four earns its place individually.

## What this bundle does not own

| | owned by |
| --- | --- |
| `CHANGELOG.md` | the release bundle |
| decision, audit and log records | the record bundles, under `.luma/records/` |
| everything in `.luma/` | the directory-structure bundle |
| `AGENTS.md`, `CLAUDE.md` | nothing — generated projections |

**Named, not depended on.** Nothing here breaks if those bundles are absent; you
simply have no policy about a changelog. A bundle may point at another to mark a
boundary — it may never require one to be present, because bundles have no
dependencies and an unresolved link is legal.

That is the working answer to a problem this catalog is starting to feel: two
bundles caring about the same file, the same directory, or the same convention.
**Acknowledge, do not depend.** See the bundle-manager bundle for the general
stance.

## Consumers

`project` only. An organization's headquarters is a repository too and has a
README, but what an organization publishes about itself is a different question
from what a project publishes about its code.

## Version

`0.1.0`. The README shape and the document matrix are drawn from practice; the
conditions in the matrix have not been tested against a project that had none of
these documents and needed to be talked through acquiring them.
