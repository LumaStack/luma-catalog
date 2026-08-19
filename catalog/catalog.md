---
type: catalog
description: Universal bundles — the starting set any organization can adopt.
tags:
  - service
  - library
  - infrastructure
  - design
  - docs
starters:
  project:
    - luma/luma-layout
    - luma/git-secrets
    - luma/project-documentation
    - luma/decision-records
  organization:
    - luma/luma-layout
    - luma/decision-records
requires:
  - bundle: luma/git-secrets
    obligation: recommended
---

# The universal catalog

Bundles useful to an organization with no connection to Luma. What each field
means and how it resolves is in [`_types/catalog.md`](_types/catalog.md).

No `upstream`: this is the root of the chain.

## What is claimed, and what is not

**Nothing is mandatory.** A mandate fails a project's checks, and this catalog
has no adopters — mandating anything now would be asserting authority over
projects that have never agreed to it. The first mandate should follow evidence
that something genuinely must not be skipped, not a belief that it should not
be.

**One recommendation.** `git-secrets` is the only bundle here whose absence
causes harm rather than inconvenience: a published credential cannot be
unpublished, and a leaked identity is permanent in every clone. Everything else
is quality of life, and reporting five gaps at a project that just adopted its
first bundle is how a report gets ignored.

**Starters carry the rest.** What a new project begins with is a different
question from what every project owes, and conflating them produces either a
nagging report or an empty one. Four bundles for a new project, two for a new
headquarters — enough to have somewhere to put decisions and a rule about
secrets, without deciding how anybody releases or merges.

Nothing here is `optional`. Every bundle in this catalog is available by being
in it, so an `optional` entry would restate the directory listing. `optional`
earns its place only where a catalog is pointing at a curated subset of
something larger.

The tag vocabulary is still provisional and nothing keys on it yet. The right
vocabulary is the one that falls out of real projects declaring what they are,
not the one guessed at first.

## Proposing a bundle

By promotion, one step at a time — written in a project, promoted to an
organization's catalog once a second project wants it, offered here once it is
useful to organizations that share nothing with yours. Skipping the middle step
means bundles arrive that nobody has stood behind.

Anything naming your customers, your systems, or your people belongs in your own
catalog instead.
