---
type: luma/project
title: luma-catalog
disclosure_level: public
description: The universal bundles any organization can adopt — standards, workflows and types. Open it to read, change or add a shipped bundle. Not for the format they are written in, nor the tool that installs them.
owns:
  - the universal catalog and everything published in it
  - the promotion path a bundle takes to reach it
  - what a bundle must contain to be publishable here
must_not_own:
  - the knowledge format itself
  - tooling that adopts, vendors or checks bundles
  - anything naming a specific organization's people or systems
---

## Why it exists

A standard nobody can pin is a standard that changes underneath its adopters.
This publishes them as versioned, self-contained directories — copy one, record
a checksum, and it cannot move without somebody noticing.

**Bundles never depend on one another**, which is the property everything else
rests on: adopting one is a directory copy, verifying one is a checksum, and
there is nothing to resolve. Composition belongs to a catalog, never to a
bundle.

## Boundaries

**Nothing here is specific to any organization.** The test for publishing is
whether a bundle would help an organization that shares nothing with this one —
not whether it can be phrased generally. Anything naming customers, internal
services or people belongs in that organization's own catalog, permanently.

**It does not install anything.** Adoption is `luma-foreman`'s job, and this
repository has no opinion about how a bundle gets from here into a project
beyond saying what a well-formed one looks like.

**Nothing has adopted anything yet.** Every bundle is `0.x` and most carry a
version note saying so plainly. Treat the reasoning as considered and the
practice as untested.
