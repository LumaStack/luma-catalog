---
type: bundle
version: 0.1.0
published: 2026-08-20
consumers: [organization]
entry_point: policy/what-a-headquarters-holds
description: The private repository where an organization records what outlives a single project — how to name it, create it, and keep checking it is still private and still readable by more than one person.
---

# Organization headquarters

Some decisions outlive the project that prompted them. *We do not use that
vendor.* *That team owns authentication.* Each gets decided once, in whichever
repository happened to raise it, and then binds four others that cannot see it.

**A headquarters is one private repository where those live.** It is a
repository like any other, so the same `.luma/` tiers apply — an organization has
a headquarters, and so does each project.

## What is here

**Policy**

- [[what-a-headquarters-holds]] — the boundary between project, organization and
  upstream, and the rule that it stays private. Read first.

**Workflows**

- [[create-headquarters]] — derive the name, find out whether it exists, create
  it with agreement.
- [[verify-headquarters]] — still there, still private, still readable by more
  than one person.

**Concept** — [[why-a-headquarters]], read when deciding whether to have one.

**Template** — [the headquarters readme](templates/headquarters-readme.md)

## The name

```
<organization-slug>-hq        →  https://github.com/acme/acme-hq
```

Legal suffixes are dropped **by proposal, not silently** — `LLC` sometimes
disambiguates two organizations sharing a name, and their answer decides it.
Ask for what people say out loud rather than what is on the incorporation
papers: *Alphabet Inc.* is the entity, *Google* is what anybody would search for.

**Where a hosting account already exists, its login wins.** `github.com/acme`
gives `acme-hq` even if the name slugs to `acme-widgets` — a derived slug that
disagrees with the account is confusing in every future reference and cannot be
corrected later without breaking links.

**The organization name is repeated on purpose.** A repository is cloned into a
directory that has lost all context: `~/code/acme-hq` says what it is and
`~/code/hq` says nothing. The same holds for a tab, a search result and a pull
request notification.

## Private is the point, and nothing enforces it

A headquarters accumulates what should not be published — vendors, internal
service names, which projects are struggling, who argued for what. **None of it
is a secret a scanner would catch.** No credential, no key, nothing a tool will
flag, which is exactly what makes it dangerous: the automated guard that stops a
project publishing a token does not exist for this.

**And publishing is not reversible.** Flipping visibility back leaves every
fork, clone and cache holding what it took — the leaked-credential argument with
no rotation available.

**So the check recurs.** Visibility can be changed by anybody with admin rights
and nothing announces it, which is why [[verify-headquarters]] exists rather
than the rule being stated once at creation.

**A public headquarters is reported, never quietly fixed.** The exposure already
happened, somebody may have had a reason, and silently reverting it destroys the
record of a decision.

## Two failures this is built around

**One reader.** An organization's reasoning behind a single account, recoverable
right up until it is not. Access lists get updated when somebody joins and
forgotten when somebody leaves, so the count drifts downward in silence.

**Leaking outward.** The direction nobody checks. Promotion is the likely path —
a bundle moving from here to the universal catalog is exactly when an internal
name travels with it, and the copy to inspect is the promoted one.

## Recommended, and genuinely optional

**An organization with one project does not need one.** Creating a headquarters
before there is cross-project reasoning to put in it produces an empty
repository that makes the practice look like ceremony.

**The signal is the second occurrence** — the same argument had twice in two
repositories, or a decision in one project that quietly binds another. Until
then the nearest home is right, which is the same rule that decides where a
bundle belongs.

## Consumers

`organization` only. A project does not adopt how to run a headquarters; it just
occasionally needs to know one exists.

## Version

`0.1.0`. **The naming rules have been run once and the workflows not at all.**
The suffix list is drawn from common legal forms rather than from anything
encountered, and it will be missing entries — treat it as a starting set, not a
specification.

**The location question is the least settled part.** A headquarters is recorded
as configuration rather than named in public repositories, but nothing reads
that configuration yet, so where it belongs has been reasoned rather than
demonstrated.
