---
type: policy
title: The repository index
description: Where a headquarters records the repositories it reasons about, why it is one file each, and the rule that keeps it from rotting — store only what cannot be derived.
compliance: mandatory
applies_to:
  - topic: recording or updating a repository in a headquarters
---

# The repository index

## Where it may be written, and nowhere else

**An index is organization-internal data.** It names repositories, including ones
most people cannot see, and where it is written is not a judgement call.

**[[create-internal-hq]] is a prerequisite.** Not a recommendation — until a
headquarters has been established and recorded, [[index-repositories]] fails and
writes nothing. **There is no fallback and there must never be one**: a workflow
that picks a likely candidate when it cannot find the declared one is a workflow
that will eventually pick wrong, quietly.

Four checks, all of which must pass, **and any that cannot be performed is a
failure rather than a pass**:

| | |
| --- | --- |
| **established** | `~/.config/luma/luma-leader/config.toml` names the headquarters by remote URL |
| **identity** | the repository you are in *is* that one — `git remote get-url origin` equal, not similar |
| **declared** | its `disclosure_level` accepts organization-internal data. **Absent refuses** |
| **actual** | it is private right now |

### Why not one check

**Because the single check this replaced was passing.** It confirmed the
destination repository was private. It was private. **Privacy was never the
question** — *is this the headquarters* was, and a check that confirms the wrong
property is worse than no check, because its passing is read as assurance.

The four fail for four different reasons — ambient state, identity, declared
intent, current reality — so no single mistake defeats them all.

### Declared beats actual, always

`disclosure_level` is a **declaration**; hosting visibility is **ambient state**.
A repository can be private today and planned for publication, and its history
goes with it when that happens. **The declaration refuses now; the visibility
check would permit.**

That is the whole failure mode: *the tool inferring its destination from ambient
state.* Every control worth having is one that does not depend on getting the
ambient state right.

### The pointer belongs to the organization tool

`~/.config/luma/luma-leader/config.toml`, **not** foreman's configuration.

**Foreman runs inside other people's project repositories**, on machines with no
connection to any headquarters, and its boundary is stated as a test: *if a
check ever needs organization context in order to run, the boundary has been
broken.* A key naming an organization's internal repository, held by the tool
that runs everywhere, is that boundary crossed — and it would travel to every
machine the tool is installed on.

Indexing repositories is organization-level work. **The tool that does
organization-level work holds the organization-level pointer.**

A headquarters reasons across repositories, so it needs to know which ones exist
and roughly what each is for. **That knowledge is a liability the moment it is
copied**, because the repositories keep changing and the copy does not.

Everything here follows from one rule.

## Store only what cannot be derived

**The repository owns its own facts. The headquarters owns only the judgements
about it.**

| | owned by | example |
| --- | --- | --- |
| **derived** | the repository or its host | description, language, visibility, default branch, whether it is archived |
| **adjudicated** | the headquarters | whether it is in scope, which team owns it, how it relates to other repositories |

**Derived values are cached, never authored.** They are copied in with a source
and a date so that re-deriving is mechanical, and so a stale one is visible as
stale rather than looking like a decision somebody made.

**Adjudicated values are the reason the index exists.** Nothing outside the
organization knows whether a repository is in scope, and no scan will ever
work it out.

### Record where a derived value came from

**A derived value with no source is indistinguishable from a hand-typed one.**
Six months later nobody can tell whether `description` was fetched or written,
so nobody dares refresh it and nobody trusts it.

`sources` records where it came from; `modified` records when, with
`by: process:<tool>` where a machine did it. Both are core fields, and between
them *is this current?* becomes a question with an answer.

**`stale_after` is the recheck date**, and it is what stops the index quietly
aging into fiction.

## When in doubt, store less and link

**A pointer that resolves beats a copy that decays.** If a fact can be looked up
in ten seconds by following the URL, the entry does not need it.

The test: **would a wrong value here cause a wrong decision at the organization
level?** If not, leave it out. An index that carries everything is an index
nobody refreshes, because refreshing it is a project.

## One file per repository, under its account

```
repositories/
  index.md              generated — never hand-edited
  acme/
    web.md
    api.md
  acme-internal/
    billing.md
```

**The account is a directory, not a filename prefix.** `acme-web.md` looks
simpler and is ambiguous: hyphens appear in account names and repository names
both, so `acme-widgets/web` and `acme/widgets-web` flatten to the same file. A
directory separator is the one character that cannot appear in either half, so
nesting cannot collide.

It also groups the way people think — an organization with several accounts reads
them as several accounts — and stays browsable at two hundred repositories where
a flat directory does not.

**Casing is the account's own, taken from the host.** `owner.login` from the API,
never from user input and never from a directory that already exists. Hosts treat
these names case-insensitively, so two accounts cannot differ only by case — but
a tool that writes `Acme/` sometimes and `acme/` others produces two entries for
one account on a case-insensitive filesystem, and git will track both. **The rule
is not which case to use; it is to take it from one source every time.**

**Not one manifest.** Four reasons, and the last is decisive.

**Diffs stay legible.** Adding a repository is a new file; changing one touches
one file. In a single manifest every change is a diff against the same blob.

**Additions stop conflicting.** Two people adding two repositories in one
manifest collide every time. As separate files they never do.

**It matches how the rest of this works.** A growing `IDEAS.md` was replaced by
one file per idea for the same reasons, and a document per thing is what the
format is for.

**And a manifest loads whole or not at all.** An agent reasoning about one
repository should read one file. At two hundred repositories a single manifest
is unusable at exactly the organization level it exists to serve — which is the
same progressive-disclosure argument that separates a concept from a preloaded
policy.

### `index.md` is generated

Regenerate it; never hand-edit it. It exists so a person can scan the whole set,
and it is disposable — **the entries are the source, and a generated file that
disagrees with its source is a second answer nobody asked for.**

## Where it lives: `repositories/`, not `.luma/`

At the root of the headquarters repository, named for what it holds.

**`.luma/` was the obvious guess and it is wrong.** That layout cuts directories
by lifecycle — intended, in force, happened — and says so explicitly: *never by
topic*. A `.luma/hq/` would be a topic, which is the one shape the layout rules
out.

**The index has a lifecycle none of the four tiers covers.** It is neither
intent, nor a rule in force, nor a record of what happened. It is **derived and
refreshed**, and it is the only content in the repository that a tool overwrites
wholesale.

**And `.luma/` is a contract every luma tool honours in every repository.** A
repository index belongs to headquarters alone. Putting it there would claim a
generality it does not have, for the benefit of one bundle.

`data/` was the other candidate. `repositories/` says what is in it, and a
reader browsing the repository learns something from the name.

## Record what you cannot read

**Repositories missing from a sweep are often missing by design.** An
organization running least privilege has repositories the indexing account
cannot open — the permission model working, not an obstacle to route around.

**Record that they exist.** Not the contents, not a guessed description:
`access: restricted`, the location, and nothing else. **An entry is a note that a
door exists; it is not a key**, and being listed grants nobody anything.

**The alternative is worse than the objection.** Anything reasoning from an index
treats an absent entry as an answer, so an agent that cannot see the billing
service concludes there is none and proposes building one. **A second system
doing one job, written by whoever lacked access to the first**, is a worse
outcome on every axis including security. [[knowing-without-access]] carries the
full argument.

**A sensible default, not a rule.** In some organizations a name alone is a
disclosure, and a security owner may decide restricted repositories are never
indexed — per repository or wholesale. **That is a legitimate configuration**
whose cost is understood, and this bundle does not argue with it twice.

### Completeness is asserted, never assumed

**A sweep cannot discover what it cannot see.** Restricted repositories reach the
index another way: somebody adds one, a reference in another repository points at
one, or a sweep runs with wider credentials.

**Many organizations will make a point of listing every repository**, and theirs
is more useful for it — an agent that can rely on the index can stop looking.
**What a reader cannot do is infer that.** A complete index and a partial one
look identical from the inside, and both mistakes cost: assuming complete when it
is not produces a duplicate of something that already exists, and treating a
complete one as partial wastes the effort that made it complete.

**So the organization states it, and the index carries the statement on its
face.** Absent one, a reader treats the index as partial.

**A useful claim names its scope** — which accounts, whether restricted
repositories are included, and as of when:

> *Complete for the `acme` and `acme-labs` accounts, restricted repositories
> included, as of 2026-08-20.*

**A bare *"complete"* is worse than none**, because it invites reliance without
saying what is being relied on.

**A scan cannot establish this about itself.** It only ever knows what it saw, so
completeness is a statement about how the organization manages its repositories
— made by the organization, carried forward by the sweep.

## Removal is never automatic

**A repository missing from a scan is ambiguous.** Deleted, renamed,
transferred, made private, or simply invisible to the account that ran the scan
— and the difference matters enormously.

**Never delete an entry because a scan did not see it.** Mark it as needing
attention and say what was and was not established. An entry deleted wrongly
takes the organization's judgements with it, and those were the part no scan can
rebuild.

Retiring one for real is `lifecycle_status: archived`, which keeps the reasoning
and stops it being treated as live.

## A scan must remember decisions

**Every organization has repositories that do not belong in the index**: forks
of upstream tools, the `.github` repository, a decade of abandoned experiments.

So `in_scope` is a field, and **a repository excluded once stays excluded.** A
scan that re-asks about the same forty repositories every time it runs is a
scan nobody runs twice.

That is what makes this idempotent, and idempotence is the whole difference
between a thing that stays current and a thing somebody did once.
