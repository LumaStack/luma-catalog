---
type: luma/catalog
namespace: luma
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
    - luma/organization-internal-hq
requires:
  - bundle: luma/git-secrets
    obligation: recommended
---

# The universal catalog

Bundles useful to an organization with no connection to Luma. What each field
means and how it resolves is in [`bundles/luma-types/_types/catalog.md`](bundles/luma-types/_types/catalog.md) — the one canonical copy, published in the `luma/luma-types` bundle rather than duplicated beside this file.

No `upstream`: this is the root of the chain.

`namespace: luma` is what makes `luma/decision-records` addressable by something
other than a person. It had been written throughout the starters below and
declared nowhere, which a reader absorbs without noticing and a tool cannot.

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
nagging report or an empty one. Four bundles for a new project, three for a new
headquarters — enough to have somewhere to put decisions and a rule about
secrets, without deciding how anybody releases or merges.

`luma/organization-internal-hq` is a starter rather than a requirement on
purpose. A headquarters is worth having and **not worth creating before there is
cross-project reasoning to put in it**, which is a judgement only the
organization can make. What the bundle buys a new headquarters is the recurring
check that it is still private, which is the part nobody remembers to do.

**`private` is in the name deliberately.** A bundle name is the one thing read
before anything is loaded, so it is the only warning that survives an agent
skimming a listing — and publishing a headquarters is the most damaging thing
available at this level.

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
