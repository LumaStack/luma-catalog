---
type: workflow
title: Create a headquarters
description: Derive a name for an organization's private headquarters repository, find out whether it already exists, and create it if not. Use when an organization has nowhere to record decisions that outlive a single project.
---

# Create a headquarters

Six steps, and **four of them are questions.** Naming a repository an
organization will refer to for years is worth four questions; guessing at it is
not.

**Nothing is created until step 6**, and nothing is created without agreement.

## 1. Ask for the organization's name

> *What is the organization called?*

**Ask for what people call it, not what is on the incorporation papers.**
*Alphabet Inc.* is a legal entity; everybody says *Google*. The repository is
named for the thing people say out loud, because that is what somebody will
guess when looking for it.

If the two genuinely differ, say so and let them choose — that is a real fork,
not a formality.

## 2. Offer to drop a legal suffix

Common suffixes, stripped by default:

```
LLC  L.L.C.  Inc  Inc.  Incorporated  Corp  Corp.  Corporation
Ltd  Ltd.  Limited  Co  Co.  Company  PLC  LLP  LP
GmbH  AG  B.V.  N.V.  S.A.  S.L.  SARL  Pty Ltd  Pte Ltd  AB  AS  Oy  K.K.
```

**Propose the stripped form and ask.** Do not strip silently:

> *`Acme Widgets LLC` → I would use `Acme Widgets`. Keep the `LLC`?*

**It is sometimes load-bearing.** It disambiguates where two organizations share
a name, and some organizations are known by the full legal form. Their answer
decides it; the default is only a default.

## 3. Slug it

Lowercase, words joined by hyphens.

| | |
| --- | --- |
| spaces and underscores | become `-` |
| `&` | becomes `and` — *Ben & Jerry's* → `ben-and-jerrys` |
| apostrophes | **removed, not replaced** — `jerrys`, never `jerry-s` |
| other punctuation | removed |
| accented characters | transliterated — `Zoë` → `zoe` |
| digits | kept as they are |
| repeated or edge hyphens | collapsed and trimmed |

**If a hosting organization already exists, its login wins.** Where the account
is `github.com/acme`, the slug is `acme` — even if the name slugs to
`acme-widgets`. A derived slug that disagrees with the account gives you
`github.com/acme/acme-widgets-hq`, which is confusing in every future reference
and cannot be fixed later without breaking links.

**Ask before deriving one that differs from an account you can see.**

## 4. Recommend the repository name

```
<organization-slug>-hq
```

So `acme` gives `acme-hq`, and the full location is
`https://github.com/acme/acme-hq`.

**The organization name is repeated on purpose.** A repository is cloned into a
directory that has lost all context — `~/code/acme-hq` says what it is, and
`~/code/hq` says nothing. The same applies to a tab, a search result, and a
pull request notification. The repetition is what makes the name work away from
the account that explains it.

**Recommend; do not impose.** If they want something else, take it — the naming
convention exists so that somebody guessing lands in the right place, and an
organization with its own established convention already has that.

## 5. Ask where it lives, and find out whether it exists

> *What is the hosting organization — `https://github.com/<org>`?*

```sh
gh repo view <org>/<slug>-hq --json name,visibility,isPrivate,url 2>&1
```

Three outcomes:

**It exists and is private.** Nothing to create — **and this workflow is not
finished.** Steps 8 and 9 still apply: a headquarters that exists but has
declared nothing and been recorded nowhere is one no tool can safely write to.
Skip to them, then run [[verify-headquarters]] for the rest.

**It exists and is public.** Stop. **This is a finding, not a step to fix in
passing** — say plainly that it is public, that anything already in it has been
published, and that flipping visibility does not unpublish. Whoever owns the
organization decides what happens next.

**It does not exist.** Continue.

## 6. Offer to create it

**Show the exact command and get explicit agreement.** Creating a repository
under somebody's organization is visible to their whole team and is not yours to
do unprompted.

```sh
gh repo create <org>/<slug>-hq --private --description "<Organization>'s headquarters — standards, decisions and boundaries"
```

**`--private` is not optional and not a default to rely on.** State it, and
verify it afterwards rather than trusting the flag:

```sh
gh repo view <org>/<slug>-hq --json visibility,isPrivate
```

If creation fails, it is almost always permissions — creating under an
organization needs rights a personal account does not have. **Say which
permission is missing** rather than retrying, and offer the alternative: somebody
with rights creates the empty repository, and the rest of this runs against it.

## 7. Give it a shape

An empty repository is a decision nobody can act on. Enough to be useful:

- **`README.md`** — what this repository is for and what belongs in it. Start
  from [the headquarters readme](../templates/headquarters-readme.md).
- **A place for decisions**, if the organization records them. `luma/decision-records`
  carries the shape; without it, a `DECISIONS.md` is enough to begin.
- **`catalog/`**, if the organization will have its own bundles. It names the
  universal catalog upstream rather than forking it.
- **`.luma/project.md`**, declaring what this repository is and **how widely it
  is disclosed.** This is not optional here — see step 8.
- **`.luma/`** more broadly, because a headquarters is a repository and keeps the
  same tiers. `luma/luma-layout` carries the layout and the workflow that
  initializes it.

**Create only what will have contents.** An empty `catalog/` is a question a
reader has to answer.

**Then commit it.** A repository whose shape exists only on your machine is not
yet a repository anybody can use.

## 8. Declare its disclosure level

In `.luma/project.md`, using the `project` type from
`luma/project-documentation`:

```yaml
disclosure_level: internal      # or confidential, or restricted
```

**Nothing writes organization-private data here until this exists.** Absent
refuses — undeclared is not permission, and a repository that has never said what
it is has not said it will hold this.

**Never `public`.** A headquarters that declares itself public is a
contradiction, and the declaration is what a guard reads rather than the hosting
visibility — which is ambient, true today, and answers a different question.

## 9. Record where it is, so a tool can find it without guessing

Write the machine-local declaration. **This is the step that makes a headquarters
a fact rather than an assumption**, and without it [[index-repositories]] fails
by design rather than picking a likely candidate.

```toml
# ~/.config/luma/luma-foreman/headquarters.toml
url = "git@github.com:acme/acme-hq.git"
```

**Machine-local, never committed.** Two reasons. A committed pointer is one file
that can be wrong for everybody at once. And to read a pointer inside the
headquarters you would have to already know which repository that is, which is
the question being answered.

**By remote URL, not by name.** A repository called `acme-hq` in the wrong
account is a different repository, and the URL is the only form that cannot be
confused. It is also local — `git remote get-url origin` reads `.git/config` and
needs no network.

**Write whatever `git remote get-url origin` returns**, and let the comparison
normalise. The same repository has several valid spellings and operators clone
differently — one over SSH, one over HTTPS — so a pointer that has to match
character for character is one that fails for a colleague and not for you.

**Each operator writes their own.** That is not duplication to be eliminated; it
is what stops one mistaken commit redirecting everybody's tooling at once.

## 10. Grant read access to more than one person

A headquarters only its creator can open is the organization's reasoning held
hostage to one account, and it is the failure nobody notices until the moment it
matters.
