---
type: policy
title: The .luma directory
description: The four directories every luma tool honours, what belongs in each, and the one invariant that makes the whole thing trustworthy.
preload: mandatory
---

# The `.luma` directory

```
.luma/
  backlog/            what we intend
  bundles/            what is in force — adopted, or written here
    adopted.toml      what this project took, and proof of what it looked like
    luma/git-secrets/
  config/
    foreman.toml      how a tool behaves here
  records/            what happened, and why
```

**This describes what the tools already do.** Adopting this bundle does not make
the layout apply to you — anything writing into `.luma/` is bound by it whether
you adopt or not. You adopt it so an agent working here can read the contract
locally, without reaching for anything remote.

## Why one directory, and why hidden

**One root.** A repository root is contested space — source, tests, manifests,
continuous integration config, licence, readme — and four more entries is real
clutter. One root also means an agent arriving cold does a single lookup and
cannot half-find the store.

**Hidden**, because the store is not the product. It is how the project is run,
sitting beside the thing the project *is*, and a visible `luma/` next to `src/`
reads as a source module. The dot says *infrastructure, not shipped output*.

**Vendor-named**, because this layout is one product's opinion rather than a
universal truth. A generic name would claim a universality nothing has earned,
and `.luma/` is collision-proof by construction.

## The tiers are cut by lifecycle

Not by topic, and not by who wrote it:

| | |
| --- | --- |
| `backlog/` | **what we intend.** Churns — items are created and destroyed |
| `bundles/` | **what is in force.** Adopted whole, or written here |
| `records/` | **what happened, and why.** Append-only, dated, never edited |
| `config/` | how a tool behaves here |

A glossary and a guardrail live in the same place not because they are similar,
but because they have the same lifecycle: both are live, both are currently in
force. That is the only axis. Sorting by topic as well would mean two questions
deciding one location, and every new item needing both answered.

## Everything in the store is committed. No exceptions.

If uncommitted files can live here, a reader cannot distinguish an authoritative
rule from somebody's local tweak, and **two agents on two machines read
different rules for the same project.** That is a correctness failure in the one
system whose entire job is saying what the rules are.

Machine-local settings — timeouts, cache locations, per-operator choices — live
in `~/.config/luma/`, never here. The test: **if deleting it loses a decision
somebody made, it is not local state.**

## `bundles/` holds both what you adopted and what you wrote

The namespace tells them apart, and it is more reliable than a directory would
be:

```
.luma/bundles/luma/git-secrets/     adopted — never edit it
.luma/bundles/acme-web/deploy/      ours — this project wrote it
```

`adopted.toml` is authoritative anyway, since only adopted bundles carry a
source and a checksum. A `vendor/` directory would put the same fact in the path
as well, and two copies of one fact can disagree.

**Editing an adopted bundle is drift**, and a check will say so. If you need it
to be different, that is a different bundle in your own namespace.

## `adopted.toml` is written by a tool, never by hand

```toml
["luma/git-secrets"]
version  = "0.1.0"
source   = "https://github.com/LumaStack/luma-catalog"
checksum = "sha256:9f2c…"
```

The checksum is the point: drift-checking compares it against the vendored files
to detect an edited copy. **A hand-edited checksum makes that check silently
start passing**, which is why the value lives nowhere near a file you are invited
to edit — and why it is not in `config/`.

It is **not a lockfile**, though it resembles one. Bundles are committed, so
nothing is ever restored from it. It answers two questions only: has anyone
edited this copy, and is a newer version available.

## Generated files are never the source

`.claude/`, `AGENTS.md`, `CLAUDE.md` and whatever replaces them live wherever
their tool looks, are generated from what is in `.luma/`, and are disposable.

Editing a generated file is editing something that will be overwritten. If the
content should be different, change what generated it.
