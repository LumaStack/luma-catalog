---
type: policy
title: Organizing a bundle
description: The layout every bundle uses, what each directory is for, and the two rules that decide whether something is a document, an asset, or a type.
preload: mandatory
---

# Organizing a bundle

```
<bundle>/
  bundle.md        the manifest — version, consumers, entry_point
  _types/          Type Definitions (reserved by the format)
  workflows/       procedures — type: workflow
  policy/          adopted courses of action — type: policy
  scripts/         ... (fill this in)
  templates/       assets to copy — no frontmatter
```

Only `bundle.md` and `_types/` are required, and only `_types/` is reserved by
the format. **The rest is convention, not specification** — the format leaves
placement deliberately unspecified, and a bundle that puts a workflow at its
root is perfectly conformant.

Follow it anyway. A reader opening any bundle should see its shape in one
glance, and a bundle with three documents at the root becomes a bundle with
fifteen at the root.

## Directories group documents; the `type` identifies them

**Nothing reads the directory.** A tool looking for procedures matches
`type: workflow`, not `workflows/`. Path-based scanning silently misses a file
somebody moved, and a capability that quietly fails to be found is worse than
one that errors.

So the directory is for humans and the frontmatter is for tools, and when they
disagree the frontmatter wins.

This is the opposite of the rule for **catalogs**, which do *not* sort bundles
into directories by kind. The difference is that a bundle can be several kinds
at once — this one is workflows *and* policy — while a document is exactly one.

## What goes where

**`workflows/`** — procedures a person or agent follows. One document per
procedure. If a workflow carries scripts or templates of its own, give it a
directory: `workflows/<name>/<name>.md` beside its material. That matches the
shape a harness wants when the workflow is projected into a skill.

**`policy/`** — courses of action this bundle's adopter takes on. Rules,
conventions, boundaries, definitions of done.

**`templates/`** — files meant to be copied and filled in. **Assets by
default**: no frontmatter, no `type`, outside validation, linked with ordinary
markdown links rather than wikilinks.

Real frontmatter in a template is legitimate only when the type it declares
**cannot be confused with a real member of the bundle** — and that is a narrower
exception than it sounds. A manifest template never qualifies, because a bundle
has exactly one manifest and a second `type: bundle` makes which one is real a
guess. A template for a type the bundle holds many of is safer, but it will
still be indexed, counted, and validated as though it were one of them.

When in doubt, carry the example **fenced** inside an asset and copy the block
rather than the file. It costs a paste and removes the ambiguity.

**`_types/`** — Type Definitions. Reserved by the format, so the name is not
ours to change.

## Three rules that decide where something goes

**Frontmatter with a `type` makes it a document. No frontmatter makes it an
asset.** There is no third category — and frontmatter *without* a `type` is the
one shape the format has no name for, so it is always a mistake.

**A type earns its name by changing validation, loading, or behaviour.** Declare
one only when a consumer must do something differently — not because a
distinction reads well. A label costs a name every future bundle has to avoid.

**Links: `[[…]]` for documents, `[…](…)` for everything else.** In frontmatter a
wikilink **must be quoted** — `[[…]]` is YAML flow-sequence syntax, so an
unquoted one parses as a nested array and the link silently never resolves.

## Bundles may carry executables; adopting one runs nothing

A workflow that ships `scripts/check.sh` is ordinary, and often necessary — it
is what travels into a harness when the workflow is projected into a skill.
Put such a script beside the workflow that owns it.

**What a bundle must never do is run something as a side effect of being
adopted.** `foreman adopt` copies files; nothing executes. A script here runs
when a person or an agent deliberately invokes it, having seen what it is.

The difference is who chose. Code you ran on purpose is a script. Code that ran
because you fetched something is a supply chain, and the promotion path —
project to organization to universal — would be one.

## When two bundles care about the same thing

Bundles have no dependencies, so there is no mechanism to say *this one needs
that one*. Two bundles will nevertheless end up caring about the same file, the
same directory, or the same convention. **Acknowledge, do not depend.**

**Name the boundary in prose.** A bundle may say *the changelog is owned by the
release bundle* without requiring it to be adopted. Nothing breaks if it is
absent — the adopter simply has no policy about their changelog, and a reader
can tell the omission is a boundary rather than a gap.

**Never link across bundles.** A wikilink or a path into another bundle breaks
self-containment and will be reported. Refer to the other bundle by name, as
text.

**Agreeing on a location is not a conflict.** Two bundles both saying prose goes
in `docs/` is a convention holding, not a collision. A collision is two bundles
requiring *different* things of the same path — and that is a real conflict that
no resolution rule should paper over, because a project cannot satisfy both and
somebody has to choose.

**Where several bundles need the same rule, each carries its own copy**, exactly
as they carry their own copies of shared types. Copies that drift are a finding,
not a merge.

### The limit, stated honestly

This works while bundles overlap in what they *mention*. It stops working the
day two bundles must genuinely agree on a value — a shared path, a shared
format, a shared identifier — and there is no place to put the agreement.

At that point the choice is a foundation bundle both vendor from, or dependency
resolution. **Neither is built, and the trigger is worth recognising rather than
solving early:** it is the first time two bundles cannot both be correct, not
merely the first time they mention each other.

## Bundles are self-contained

Every path a bundle references resolves inside it. A link that escapes breaks
the property the entire distribution model rests on: you can copy the directory,
ship it, and have it still work.

This is why a bundle that needs the `workflow` or `policy` type **carries its
own copy** rather than referencing another bundle's. Bundles have no
dependencies, and vendoring is the mechanism.

## Directory names in Document IDs

A Document's ID is its path within the bundle, so moving a document between
directories changes its ID and breaks inbound links. Choose the directory when
the document is created; reclassifying later is a rename with consequences.

`entry_point` in `bundle.md` carries the **full ID** —
`workflows/publish-release` — because it must be unambiguous. Wikilinks in
prose use the slug alone. Where two documents in different directories share a
slug, that ambiguity is currently unresolved by the format; avoid it.
