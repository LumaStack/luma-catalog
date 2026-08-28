---
type: luma/catalog
description: Universal bundles — the starting set any organization can adopt.
tags:
  - service
  - library
  - infrastructure
  - design
  - docs
requires:
  - bundle: lumastack/luma-catalog/git-secrets
    obligation: recommended
---

# The universal catalog

Bundles useful to an organization with no connection to Luma. What each field
means and how it resolves is in [`bundles/luma-types/_types/catalog.md`](bundles/luma-types/_types/catalog.md) — the one canonical copy, published in the `lumastack/luma-catalog/luma-types` bundle rather than duplicated beside this file.

No `upstream`: this is the root of the chain.

**No `namespace`, deliberately.** It derives from where this catalog lives:
`github.com/LumaStack/luma-catalog` gives `lumastack/luma-catalog`, so a bundle
here is `lumastack/luma-catalog/decision-records`.

Declaring one is allowed and wins wherever it appears. Do not, unless you need
a name your address cannot give you. A declaration is a line a fork inherits by
copying the file, and it is the only way a fork of this catalog could publish
under this catalog's name — deriving costs nothing and cannot be inherited,
because a fork lives somewhere else.

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

**Nothing says what a new consumer begins with.** `starters` did, and it is
withdrawn — see `luma-leader`'s archived idea. It was written before anything
could use it: a catalog cannot key a starter on a consumer's kind while no
consumer declares one, so the lists sat here describing a bootstrap nothing
performed. Bringing it back needs that gap closed first and a reason beyond
symmetry with `requires`.

**What that costs is real and is accepted.** A new project adopting from here
gets no suggested set, so somebody has to choose — which is what happened
anyway, since nothing read the lists.

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
