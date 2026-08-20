---
type: policy
title: The repository index
description: Where a headquarters records the repositories it reasons about, why it is one file each, and the rule that keeps it from rotting — store only what cannot be derived.
preload: mandatory
---

# The repository index

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

## One file per repository

```
repositories/
  index.md          generated — never hand-edited
  acme-web.md
  acme-api.md
```

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
