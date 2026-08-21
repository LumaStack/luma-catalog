---
type: bundle
version: 0.4.0
published: 2026-08-20
consumers: [organization]
entry_point: policy/what-a-headquarters-holds
description: The internal repository where an organization records what outlives a single project — naming it, creating it, indexing the repositories it reasons about, and rechecking that it is still private.
---

# Organization internal headquarters

Some decisions outlive the project that prompted them. *We do not use that
vendor.* *That team owns authentication.* Each gets decided once, in whichever
repository happened to raise it, and then binds four others that cannot see it.

**A headquarters is one internal repository where those live.** It is a
repository like any other, so the same `.luma/` tiers apply — an organization has
a headquarters, and so does each project.

## `internal` is in the name on purpose

A bundle name is **the one thing read before anything is loaded** — the only
warning that survives an agent skimming a listing and picking a workflow. So the
audience is in the name.

**`organization-` leads because a catalog is a flat directory**, and the subject
is what groups related bundles in a listing. `internal` sits where somebody
reading the name will still see it.

**It was `private` until 2026-08-20, and the swap costs something worth naming.**
*Private* is the louder word, and a louder warning is not nothing. But it names
a **hosting setting** rather than an audience — ambient, true today, and
changeable by anybody with admin rights without announcement. A bundle named for
a setting is wrong the moment the setting changes, and it leaves no way to say
*this is ours, and we have deliberately chosen to show it to people*. **Internal
is what the content is; private is how it is currently stored.** The name should
carry the durable half.

The warning that was doing the real work is kept where it cannot be skimmed
past — here, and at the top of every workflow that writes.

**Publishing a headquarters is the worst outcome available at this level.** Not
an embarrassment — a handover of trade secrets and institutional knowledge to
anybody who wants them: what an organization worked out over years, why it beat
a competitor, what it learned the expensive way, all in one place and easier to
read than the systems it describes. **And it does not reverse**: every fork,
clone and cache keeps what it took.

**So a headquarters is private by default and strongly recommended to stay
private.** Internal does not mean casually shareable; it means the audience is
this organization, and privacy is how that is normally enforced.

**Publishing one takes more than one round of signoff, and an agent never
initiates it.** Not a confirmation prompt, and never inferred from a
`disclosure_level` edit, a visibility setting, or a person saying yes once while
thinking about something else. The bar is deliberately higher than anything else
in this bundle:

- **A person asks for it explicitly** — never an agent proposing it, and never a
  step reached by following this workflow.
- **The contents are reviewed first**, in full, by somebody who would recognise
  what should not leave. Publishing unreviewed is publishing blind.
- **They confirm again afterwards**, separately, knowing what the review found.

A few organizations will publish theirs and some are right to. That is a
decision taken once, in the open, by people who own the consequences — never a
default anybody drifts into.

## What is here

**Policy**

- [[what-a-headquarters-holds]] — the boundary between project, organization and
  upstream, and the rule that it stays private. Read first.
- [[the-repository-index]] — where the index lives, why one file each, and the
  rule that keeps it from rotting.

**Workflows**

- [[create-internal-hq]] — derive the name, find out whether it exists, create
  it with agreement.
- [[index-repositories]] — sweep the hosting accounts, record one entry each,
  refresh what changed.
- [[verify-headquarters]] — still there, still private, still readable by more
  than one person.

**Concepts** — retrieved when relevant, never preloaded.

- [[why-a-headquarters]] — read when deciding whether to have one.
- [[knowing-without-access]] — the stance on indexing repositories nobody here
  can read. Read when it is challenged.

**Type** — [[repository]] · **Templates** —
[a repository entry](templates/repository-entry.md) ·
[the headquarters readme](templates/headquarters-readme.md)

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

## Where internal data may be written

**[[create-internal-hq]] is a prerequisite for [[index-repositories]].** Until a
headquarters has been established and recorded, indexing fails and writes
nothing. **No fallback, ever** — a workflow that picks a likely candidate when it
cannot find the declared one will eventually pick wrong, quietly.

Four checks, all required, **and any that cannot be performed is a failure rather
than a pass**: `~/.config/luma/luma-hq/config.toml` names the headquarters by
remote URL; the repository you are in *is* that one, compared normalised; its
`disclosure_level` accepts organization-internal data, where **absent refuses**;
and it is private now.

**The pointer is the organization tool's, not foreman's.** Foreman runs inside
other people's repositories and must not hold an organization's context — its own
boundary says so as a test: *if a check ever needs organization context in order
to run, the boundary has been broken.*

**Declared beats actual.** `disclosure_level` is a declaration; hosting
visibility is ambient state. A repository can be private today and planned for
publication — and its history goes with it. The declaration refuses now; a
visibility check would permit.

**And a mismatch is never resolved silently.** Actually public while declaring
narrower is a **showstopper** — content believed internal is readable right now,
so stop, say what is exposed, and change nothing. Declaring `public` while
actually private is the **safe direction and often correct**; report it once.

**The asymmetry behind every rule here:** being wrong toward restriction is an
inconvenience somebody notices and fixes in a minute; being wrong toward
permission is forked, cloned and cached before anybody looks. So absent refuses,
the declaration beats the observation, an unperformable check fails, and the
field can narrow but never widen — **one principle applied four times.**

**Nothing publishes on the strength of this field.** A tool reading `public` and
widening access has turned a safety limit into a command.

**Neither drives the other.** The value does not change the repository — a text
edit must never become an irreversible disclosure. And it is not derived from
the repository either, because a field derived from ambient state *is* ambient
state, and would record a soon-to-be-published repository as safe. **It is an
independent assertion checked against an independently observed reality**, and
the gap is reported rather than reconciled.

**Tightening the declaration is cheap and reversible; loosening it may not be
recoverable at all.** Widening disclosure only ever refuses more — it can break
a workflow, and everything it breaks is an interruption somebody notices in
minutes. Narrowing it permits content that was previously refused, which is the
one edit to this field that can cause a leak, and a leak is forked and cached
before anybody looks.

**And syncing the declaration to reality is not housekeeping.** A repository
declaring `public` because it is planned for publication, "corrected" to
`internal` because it is *currently* private, has just admitted internal data to
a repository about to be published — a change that reads in the diff as making a
file agree with the world. **Matching reality is an observation, and
observations do not grant permissions.**

**Why four and not one:** the single check this replaced *was passing.* It
confirmed the destination was private, which was true, and privacy was never the
question. **A check that confirms the wrong property is worse than no check**,
because its passing reads as assurance.

## The repository index, and how it avoids rotting

A headquarters reasons across repositories, so it has to know which exist and
what each is for. **That knowledge is a liability the moment it is copied**, so
one rule governs all of it:

**Store only what cannot be derived.** The repository owns its own facts —
description, language, visibility, whether it is archived — and those are
*cached with a source and a date*, never authored. The headquarters owns only the
judgements: whether a repository is in scope, who owns it, how it relates to
others. Those are what no scan will ever produce.

**A derived value with no source is indistinguishable from a hand-typed one**,
which is why `sources` is recorded. Without it a refresh either destroys
somebody's considered wording or refreshes nothing.

**One file per repository, in `repositories/`**, with a generated `index.md`
beside them. Not one manifest: additions stop conflicting, diffs stay legible,
and — decisively — **a manifest loads whole or not at all**, which is useless at
two hundred repositories, at exactly the level it exists to serve.

**Not `.luma/`.** That layout cuts directories by lifecycle and says *never by
topic*, so `.luma/hq/` is the one shape it rules out. The index also has a
lifecycle none of the four tiers covers: it is **derived and refreshed**, the
only content a tool overwrites wholesale.

**Nothing is ever deleted by a scan.** A repository that has vanished may be
deleted, renamed, transferred, made private, or simply invisible to the account
that ran the sweep — and an entry deleted wrongly takes the organization's
judgements with it.

## Repositories nobody here can read are still recorded

An organization running least privilege will have repositories the indexing
account cannot open. **That is the permission model working**, and the index
records their existence anyway: `access: restricted`, a location, and nothing
else. **An entry is a note that a door exists; it is not a key.**

**Because the alternative is worse than the objection.** Anything reasoning from
an index treats an absent entry as an answer — so an agent that cannot see the
billing service concludes there is none and proposes building one. **A second
system doing one job, written by whoever lacked access to the first**, is worse
on every axis including security.

**And completeness is asserted, never assumed.** Many organizations will make a
point of listing every repository, and theirs is more useful for it — but a
complete index and a partial one look identical from the inside, and **a scan
cannot establish this about itself**, since it only ever knows what it saw. So
the organization states it, naming the accounts, whether restricted repositories
are included, and as of when; the sweep carries that forward; and absent a
statement a reader treats the index as partial.

**This is a default, and it yields.** In some organizations a name alone is a
disclosure. A security owner may decide restricted repositories are never
indexed, per repository or wholesale — a legitimate configuration whose cost is
understood. [[knowing-without-access]] argues the trade-off once so that nobody
has to argue it again.

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

`0.4.0` — mismatch handling is new content; existing use is unaffected.

Actually public while declaring narrower now **stops the workflow**, because
content believed internal is readable right now and no correction retrieves it.
Declaring `public` while actually private is reported and is not a fault — it is
the safe direction, and this stack has a live example of it.

`0.3.0` — the destination gate is new content; existing use is unaffected,
except that `index-repositories` now **fails where it previously proceeded.**
That is the intended change.

**It was written after this bundle failed in exactly the way it was meant to
prevent.** An index was written into published software because the guard
confirmed the destination was private, which was true and irrelevant. The gate
that replaced it checks four things, none of which is *privacy alone*.

`0.2.0` — reading `.luma/project.md` was new content, and existing use was
unaffected.

**The naming rules have been run once and the workflows not at all.**
The suffix list is drawn from common legal forms rather than from anything
encountered, and it will be missing entries — treat it as a starting set, not a
specification.

**The location question is the least settled part.** A headquarters is recorded
as configuration rather than named in public repositories, but nothing reads
that configuration yet, so where it belongs has been reasoned rather than
demonstrated.

**The descriptor this depends on now exists and nothing has one.**
`.luma/project.md` is where a repository answers *when should somebody open
this?*, defined by `luma/project-documentation` — so the headquarters collects
rather than authors. No repository has written one yet, so in practice every
description here starts as a derived fallback, which is the one field most
likely to rot until that changes.
