---
type: bundle
version: 0.7.0
published: 2026-08-25
consumers: [project, organization]
entry_point: policy/organizing-a-bundle
description: Creating, updating, auditing, repairing, migrating and retiring bundles — the layout they use and which catalog they belong in.
---

# Bundle manager

Bundles are cheap to write and easy to write badly, and the failures are quiet.
A broken link, an unquoted wikilink in frontmatter, a template with frontmatter
that a tool reads as a real document — none of these produce an error. The
bundle stays conformant, adopters copy it, and the defect travels.

This bundle carries the layout every bundle uses, the rule for which catalog one
belongs in, and a procedure for each thing you do to a bundle over its life.

## What is here

**Policy**

- [[organizing-a-bundle]] — the layout, and the three rules that decide whether
  something is a document, an asset, or a type. Read first.
- [[where-a-bundle-belongs]] — project, organization, or universal, and how a
  bundle moves between them.
- [[an-index-of-what-exists]] — load the index, never the content. How a bundle
  stays large without being expensive, and why the alternative fails silently.

**Workflows**

- [[create-bundle]] — scaffold a new one and get it publishable.
- [[update-bundle]] — change contents and version the change honestly.
- [[audit-bundle]] — the checklist for defects that fail silently.
- [[repair-bundle]] — fix findings in an order that avoids making it worse.
- [[migrate-bundle]] — promote between catalogs, or restructure in place.
- [[delete-bundle]] — retire one without stranding its adopters.

**Templates**

- [the bundle manifest](templates/bundle.md)
- [a Type Definition](templates/type-definition.md)

Both are assets carrying **fenced** examples rather than real frontmatter. A
manifest template with live frontmatter is a second bundle manifest inside this
bundle, and every tool reading it would believe that — which is the first thing
[[organizing-a-bundle]] warns about, so this bundle had better not do it.

## Loading

Only [[organizing-a-bundle]] has no `applies_to` — every workflow here
assumes it. The six workflows are `optional`: you load the one you are doing,
not all six.

That is the field working as intended. Marking every workflow mandatory would
impose the whole bundle on any consumer that touched it, which is the cost that
keeps `mandatory` meaning something.

**The three document directories are three disclosure tiers**, which is the
point of filing by type at all:

| tier | what belongs there | when it loads |
| --- | --- | --- |
| **`policy/`** | what to do, and what outranks what | **standing** |
| **`workflows/`** | the procedures | **invoked** |
| **`concepts/`** | background that explains — rationale, models, open questions | **when relevant** |

The test is whether the reader is working **through** the bundle or **on** it.
Following a procedure is *through*; deciding whether to keep it is *on*.

Getting it wrong is expensive in one direction and dangerous in the other:
rationale in a mandatory policy is charged to every consumer in every session,
and something operational filed as background is never loaded by the agent about
to violate it.

This bundle has no `concepts/`, and **most bundles should not.** One is earned
when a policy grows an argument longer than the rule it justifies.

## Consumers

Both levels. An organization curates a catalog and a project writes bundles it
may later promote, and the procedure is the same at either end.

## Version

`0.7.0` — **`compliance` is gone.** A policy binds because it is a policy —
that is what the type means — and what happens when it is broken is what
`on_violation` says. The field between them restated the type on documents that
bind, and offered a soft tier to documents that arguably should not be policies
at all.

Minor. Nothing a reader is obliged to do has changed.

`0.6.0` — **vocabulary.** `moment` becomes `event` — a moment is a point in
time and `applies_to` takes nouns. `compliance` is dropped wherever it was
saying nothing: a policy binds unless it says otherwise, so only a strong
default declares `recommended`, and a workflow's steps bind by being steps.
Type Definitions use `field_presence: required` for what was
`obligation: mandatory`, matching the format.

Minor. Nothing a reader is obliged to do has changed; what declares it has.

`0.5.1` — the naming rule gains a plain-English restatement beneath the precise
one. The abstract wording is what makes the rule exception-free, so it stays;
the plain wording is what a person meeting it cold can act on. Patch: no rule
changed, only how it is said.

`0.5.0` — **`preload` is replaced by `compliance` and `applies_to`.** An author
now says how strongly a rule binds and when it governs; *when it is delivered* is
computed from those and never declared. Every rule here could state when it
applies, so **nothing in this bundle is loaded unconditionally any more** — it
arrives when the work matches and costs nothing before then.

Minor: a consumer reading `preload` finds nothing, and the loading behaviour of
every document changes.

`0.4.0` — **the naming rule is written down**: ALL CAPS names a file that
speaks for the thing containing it, lowercase names one of the things contained.
With the case a document owns a directory, which is how a workflow carrying its
own steps keeps them out of every consumer's standing surface.

Minor, because an author who correctly understood the previous version would now
lay a bundle out differently.

`0.3.0` — **the manifest is `BUNDLE.md`.** Reserved markdown files are now
ALL CAPS across the estate, because nobody types all caps by accident: a file
becomes load-bearing only when somebody deliberately made it so, and writing
`bundle.md` now fails in the safe direction — ignored rather than silently wired
into machinery. Minor rather than patch, and pre-1.0 that is the tier for a
breaking change: anything naming the old path by hand stops resolving.

`0.2.2` — a heading no longer says how many things are beneath it. Wording only.

Patch: no normative sentence moved and a reader who correctly understood
`0.2.1` behaves identically. See `writing-style` in `luma/project-documentation`
for the rule and the failure it prevents.

`0.2.1` — a wikilink in [[an-index-of-what-exists]] pointed into another bundle
and therefore at nothing. Named in prose instead. **Found by `luma-foreman
inspect` the first time anything ran it across the whole catalog**, which is the
defect class this bundle's opening paragraph warns about.

`0.2.0` — adds [[an-index-of-what-exists]]. New content; existing use unaffected.

**Named because it had been rediscovered three times.** It is the answer in
`find-decision`, in situational mandates, and in conditional loading generally,
and it existed only inside those three discussions — so the next person to hit a
context budget would have invented it a fourth time.

**And it turns out to be an assembly rather than an invention.** `description` on
every document, the `index.md` the format already reserves as *derived
navigation*, and `preload` on that index. Three existing parts nobody had put
together.

`0.1.0`. These conventions were extracted from writing three bundles in one
afternoon — real practice, but not much of it, and the audit checklist in
particular has never been run against a bundle somebody else wrote.
