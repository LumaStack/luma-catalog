---
type: luma/catalog
description: Universal bundles — the starting set any organization can adopt.
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

**Nothing is required, and that is the point.** A catalog is a shelf things are
published on, not a body that governs the people who take from it. Obligations
belong to an organization, which its projects have agreed to be part of — this
catalog serves organizations with no connection to Luma, and has no standing to
oblige any of them.

**The argument for one exception did not survive being written down.**
`git-secrets` was recommended here on the grounds that a published credential
cannot be unpublished, which is true and is still not this catalog's call to
make. An organization that agrees with it can require it of its own projects,
where the obligation has somebody behind it. Recommending it from a shelf is
asserting the same authority in a quieter voice.

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

**No tag vocabulary either.** It existed for `requires` to narrow an obligation
to some consumers and not others, and with nothing required there is nothing to
narrow. It was already provisional and already keyed on by nothing; the right
vocabulary is the one that falls out of real projects declaring what they are,
not the one guessed at first.

## Proposing a bundle

By promotion, one step at a time — written in a project, promoted to an
organization's catalog once a second project wants it, offered here once it is
useful to organizations that share nothing with yours. Skipping the middle step
means bundles arrive that nobody has stood behind.

Anything naming your customers, your systems, or your people belongs in your own
catalog instead.
