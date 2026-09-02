---
type: procedure
title: Create an internal headquarters
description: Derive a name for an organization's internal headquarters repository, decide which hosting account it belongs in, find out whether it already exists, and create it if not. Use when an organization has nowhere to record decisions that outlive a single project.
---

# Create an internal headquarters

Seven steps, and **five of them are questions.** Naming a repository an
organization will refer to for years is worth five questions; guessing at it is
not.

**Nothing is created until step 7**, and nothing is created without agreement.

## Internal, not private

**`internal` describes who it is for. `private` describes a hosting setting.**
The two are not the same, and the procedure depends on the difference:

- **Internal** is the audience — this organization, and not the public. That is
  a property of the content and it does not change when a setting does.
- **Private** is the hosting visibility. It is ambient, true today, and
  changeable by anybody with admin rights without announcement.

A headquarters is **created private and should stay private**, and the
[[verify-headquarters]] check exists because that can quietly stop being true.
But *internal* is what it **is**, and a few organizations will publish theirs
deliberately and be right to. Calling the thing *private* names the setting
rather than the audience, and leaves no way to say *this is ours, and we have
chosen to show it to people*.

**Publishing takes more than one round of signoff, and an agent never initiates
it.** Not a confirmation prompt, and never inferred from a `disclosure_level`
edit, a visibility setting, or somebody saying yes once. A person asks for it
explicitly; the contents are reviewed in full by somebody who would recognise
what should not leave; and they confirm again afterwards, knowing what the
review found.

The bar is that high because of what is handed over — what an organization
worked out over years, what it learned expensively, why it beat a competitor,
which projects are struggling — in one place and more readable than the systems
it describes. And **it does not reverse**: every fork, clone and cache keeps what
it took, which is the leaked-credential problem with no rotation available.

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

## 4. Recommend the repository name

```
<organization-slug>-hq
```

So `acme` gives `acme-hq`.

**The organization name is repeated on purpose.** A repository is cloned into a
directory that has lost all context — `~/code/acme-hq` says what it is, and
`~/code/hq` says nothing. The same applies to a tab, a search result, and a
pull request notification. The repetition is what makes the name work away from
the account that explains it.

**Recommend; do not impose.** If they want something else, take it — the naming
convention exists so that somebody guessing lands in the right place, and an
organization with its own established convention already has that.

## 5. Ask which account it belongs in

> *Which hosting account should this live in?*

**Ask. Do not infer it from where you are standing.** This is the step most
likely to be quietly wrong, because every available signal is a decent guess and
none of them is the answer:

- **A separate account for internal work is common and often deliberate.**
  Public repositories in `github.com/acme`, internal ones in
  `github.com/acme-internal`, with different membership and different defaults.
  Creating the headquarters alongside the public repositories defeats a
  separation somebody chose on purpose.
- **The operator may not be inside the target organization at all.** A
  contractor, a consultant, or somebody setting this up from a personal account
  for an organization they are not a member of.
- **The current repository is not evidence.** Whatever directory this is being
  run from says where somebody happened to be, not where an organization keeps
  what it does not publish.

**Offer what you can see, and mark it as a guess.** List the accounts the
authenticated user can create repositories in, say which one you would pick and
why, and let them correct it:

```sh
gh api user/orgs --jq '.[].login'
```

**If the account they name is one you cannot see, that is not an error.**
Permissions to create may be held by somebody else entirely — take the answer
and let step 7 fail informatively rather than arguing with it here.

**Only once the account is known does the slug rule bend to it.** Where the
account is `github.com/acme`, the slug is `acme` — even if the organization's
name slugs to `acme-widgets`. A derived slug that disagrees with the account
gives `github.com/acme/acme-widgets-hq`, which is confusing in every future
reference and cannot be fixed later without breaking links. **Ask before
deriving one that differs from an account you can see.**

## 6. Find out whether it already exists

```sh
gh repo view <account>/<slug>-hq --json name,visibility,isPrivate,url 2>&1
```

Three outcomes:

**It exists and is private.** Nothing to create — **and this procedure is not
finished.** Steps 9 and 10 still apply: a headquarters that exists but has
declared nothing and been recorded nowhere is one no tool can safely write to.
Skip to them, then run [[verify-headquarters]] for the rest.

**It exists and is public.** Stop. **This is a finding, not a step to fix in
passing** — say plainly that it is public, that anything already in it has been
published, and that flipping visibility does not unpublish. Whoever owns the
organization decides what happens next.

**It does not exist.** Continue.

## 7. Offer to create it

**Show the exact command and get explicit agreement.** Creating a repository
under somebody's organization is visible to their whole team and is not yours to
do unprompted.

```sh
gh repo create <account>/<slug>-hq --private --description "<Organization>'s headquarters — policies, decisions and boundaries"
```

**`--private` is not optional and not a default to rely on.** State it, and
verify it afterwards rather than trusting the flag:

```sh
gh repo view <account>/<slug>-hq --json visibility,isPrivate
```

If creation fails, it is almost always permissions — creating under an
organization needs rights a personal account does not have, and an operator
outside the organization will not have them at all. **Say which permission is
missing** rather than retrying, and offer the alternative: somebody with rights
creates the empty repository, and the rest of this runs against it.

## 8. Give it a shape, and no more than that

An empty repository is a decision nobody can act on. Enough to be useful:

- **`README.md`** — what this repository is for and what belongs in it. Start
  from [the headquarters readme](../templates/headquarters-readme.md).
- **`.luma/PROJECT.md`**, declaring what this repository is and **how widely it
  is disclosed.** This is not optional here — see step 9.

**And nothing else. Create no empty tiers.** `backlog/`, `policy/` and
`records/` are created **the first time something is written into one**, not
ahead of it:

- **An empty directory is a question a reader has to answer.** Somebody opening
  `records/` and finding nothing cannot tell whether nothing has happened,
  whether it is used, or whether something was lost.
- **Scaffolding invents obligations.** Three empty directories read as three
  things somebody is behind on, and a new headquarters looks like a chore before
  it has held a single decision.
- **The first write is where the tier gets its meaning.** A `records/` created
  by the first audit is self-evidently for audit output; one created empty at
  bootstrap is for whatever the first person to open it assumes.

The same applies to `catalog/`, which exists only when an organization actually
has bundles of its own, and names the universal catalog upstream rather than
forking it.

**Then commit it.** A repository whose shape exists only on your machine is not
yet a repository anybody can use.

## 9. Declare its disclosure level

In `.luma/PROJECT.md`, using the `project` type from
`lumastack/luma-catalog/project-documentation`:

```yaml
disclosure_level: internal      # or confidential, or restricted
```

**Nothing writes organization-internal data here until this exists.** Absent
refuses — undeclared is not permission, and a repository that has never said what
it is has not said it will hold this.

**Never `public`, and never as a step in this procedure.** A headquarters
declaring itself public is a contradiction with the reason it was created, and
the declaration is what a guard reads rather than the hosting visibility — which
is ambient, true today, and answers a different question. If an organization
genuinely decides to publish theirs, that is a deliberate act taken separately by
people who own the consequences, with the contents reviewed first. It is never
reached by editing this field in passing.

## 10. Record where it is, so a tool can find it without guessing

Write the machine-local declaration. **This is the step that makes a headquarters
a fact rather than an assumption**, and without it [[index-repositories]] fails
by design rather than picking a likely candidate.

```toml
# ~/.config/luma/luma-leader/config.toml
[headquarters]
url = "https://github.com/acme/acme-hq.git"
```

**It belongs to the organization tool.** Foreman runs inside other people's
project repositories, on machines with no connection to any headquarters, and
its own boundary is explicit: *if a check ever needs organization context in
order to run, the boundary has been broken.* A key naming an organization's
internal repository, in the tool that runs everywhere, is that boundary crossed.

Organization-level work is `luma-leader`'s, so the pointer is its configuration —
under `~/.config/luma/<repository-name>/`, the same shape every luma tool uses.

**A section rather than a file of its own**, because a headquarters pointer will
not be the only thing this tool needs to know.

**Machine-local, never committed.** Two reasons. A committed pointer is one file
that can be wrong for everybody at once. And to read a pointer inside the
headquarters you would have to already know which repository that is, which is
the question being answered.

**By remote URL, not by name.** A repository called `acme-hq` in the wrong
account is a different repository — and with internal work commonly kept in a
separate account, that is a live confusion rather than a theoretical one. The
URL is the only form that cannot be mistaken. It is also local:
`git remote get-url origin` reads `.git/config` and needs no network.

**Write whatever `git remote get-url origin` returns**, and let the comparison
normalise. The same repository has several valid spellings and operators clone
differently — one over SSH, one over HTTPS — so a pointer that has to match
character for character is one that fails for a colleague and not for you.

**Each operator writes their own.** That is not duplication to be eliminated; it
is what stops one mistaken commit redirecting everybody's tooling at once.

## 11. Grant read access to more than one person

A headquarters only its creator can open is the organization's reasoning held
hostage to one account, and it is the failure nobody notices until the moment it
matters.

**Check rather than assume, and check inherited access rather than the
collaborator list** — an organization repository is readable by owners and by
teams that never appear as direct collaborators:

```sh
gh api "repos/<account>/<slug>-hq/collaborators?affiliation=all" --jq '.[] | "\(.login) \(.role_name)"'
gh api orgs/<account>/members --jq '.[].login'
```

**One reader is a finding, not a failure to fix silently.** Where an
organization genuinely has one person, say so plainly and let them decide:
a second account with independent recovery, or a knowing acceptance that is
recorded. **A recorded acceptance is worth more than an unmet step**, because it
carries a reason and a date and can be revisited.
