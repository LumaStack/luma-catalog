---
type: workflow
title: Index repositories
description: Sweep an organization's hosting accounts, record one entry per repository, and refresh what has changed. Use on first setting up a headquarters, and periodically after.
---

# Index repositories

**The same workflow the first time and every time.** Discovering repositories
and refreshing them are one operation — a first run finds everything and a later
run finds the difference.

**It is idempotent or it is worthless.** A scan that re-asks the same questions
every run is a scan nobody runs twice, and an index nobody refreshes is worse
than none.

Read [[the-repository-index]] first: what is stored, what is not, and why the
answer is *as little as possible*.

## 0. The destination gate — refuse before doing anything

**This runs first, before the sweep.** An index is organization-private data,
and where it is written is not a judgement call.

**All four must pass. Any that cannot be performed is a failure, not a pass.**

**1. A headquarters has been established.** [[create-headquarters]] writes a
machine-local declaration naming it:

```sh
cat ~/.config/luma/luma-foreman/headquarters.toml   # url = "git@github.com:acme/acme-hq.git"
```

**No declaration means stop.** Do not search for a likely candidate, do not offer
to use the repository you are standing in. Say that no headquarters has been
established and that [[create-headquarters]] establishes one. **This workflow has
no fallback and must not acquire one.**

**2. You are standing in that repository.** Compare by remote URL, which is local
and needs no network:

```sh
git remote get-url origin
```

**It must equal the declared URL.** Not resemble it, not share a name — equal it.
A repository named `acme-hq` in the wrong account is a different repository.

**3. Its `disclosure_level` accepts organization-private data.** Read
`.luma/project.md` in the repository you are standing in.

**Absent refuses.** Undeclared is not permission, and a repository that has never
said what it is has not said it will hold this. **`public` refuses** — including
when the repository is private today, because a repository planned for
publication is one whose history goes with it.

**4. It is private now.** The weakest of the four and still worth running: a
declaration saying `internal` on a repository that is currently public is a
contradiction somebody needs to hear about immediately.

### Why four checks and not one

**Because the single check this replaced was passing.** It confirmed the
destination was private, which was true, and privacy was never the question —
*is this the headquarters* was. **A check that confirms the wrong property is
worse than no check**, because its passing is read as assurance.

Each of these can fail independently, and **no two of them fail for the same
reason.** Ambient state, identity, declared intent, current reality.

## 1. Ask which accounts to sweep

> *Which hosting accounts hold your repositories?*

**Expect more than one.** An organization is rarely one account — there is the
main one, an experiments or labs account, sometimes a personal account holding
a tool everybody depends on, occasionally a legacy account nobody has closed.

Record the list; the next run should not have to ask again.

## 2. List what is there

```sh
gh repo list <org> --limit 1000 \
  --json name,url,description,visibility,isArchived,isFork,updatedAt,primaryLanguage
```

**Check the count against the limit.** A result of exactly the limit means the
list was truncated, and a truncated sweep silently reports fewer repositories
than exist — which looks identical to a small organization.

Other hosts have equivalents. Where none is available, a hand-supplied list is
fine: the index does not care how a repository was found.

**What you cannot see will not be listed, and that is usually deliberate.** An
organization running least privilege has repositories this account cannot open,
so a sweep is a view rather than a census.

**Record the ones you know of anyway** — from a person, from a reference in
another repository, or from a sweep run with wider credentials:

```yaml
access: restricted
description:            # leave it out. Do not guess, do not infer from the name
```

**Do not retry, do not work around the permission, and above all do not conclude
the repository does not exist.** Something reasoning from this index treats an
absent entry as an answer, and the answer it reaches is *build a second one*.
See [[knowing-without-access]], including why a security owner may tell you to
stop recording these at all.

**Report what the sweep covered, not that it covered everything.** It saw what
this account can see. If the organization has stated its index is complete —
and many will — carry that statement rather than re-deriving it; a scan can only
ever know what it saw.

## 3. Compare against what is already recorded

Three sets, and each is handled differently:

**Known and still present** → refresh the derived values, step 5.

**Present but not recorded** → new. Decide scope, step 4.

**Recorded but not seen** → **do not delete it.** Deleted, renamed,
transferred, made private, or invisible to the account you are running as — the
difference matters enormously and a scan cannot tell you which.

Mark it as needing attention, say what was and was not established, and let a
person resolve it. **An entry deleted wrongly takes the organization's
judgements with it**, and those are the part no scan can rebuild.

## 4. Decide scope, once, for the new ones

**`in_scope` is the only judgement the index asks for**, and the only thing no
scan can produce.

Batch the question rather than asking per repository — a list of twenty with a
proposed answer each is one exchange; twenty questions is an interrogation
nobody finishes.

**Propose, do not decide.** Reasonable defaults to offer: forks of upstream
projects and the `.github` repository are usually out; anything archived is
usually out; everything else is usually in.

**Record `false` explicitly.** An excluded repository gets an entry saying so,
which is what stops it being rediscovered and re-asked forever. Leaving it out
entirely means the next run treats it as new.

**Undecided is a real state.** If somebody does not know, leave `in_scope`
absent rather than guessing — that is a question worth finding later, and
`false` would hide it.

## 5. Refresh the derived values

For each in-scope repository, cache only what the organization needs in order to
reason at its level — see [[the-repository-index]] for the test.

```yaml
description: <when somebody should open this repository>
sources: [{ from: "github:<org>/<name>", field: description }]
modified: { by: process:index-repositories, at: <timestamp> }
stale_after: <a date somebody will actually recheck by>
```

### Where `description` comes from, in order

**The repository owns this fact and the headquarters must never become its
author.** A description written here is a copy, and a copy of something that
changes is wrong from the first commit that changes it, with nothing announcing
the drift.

**1. `.luma/project.md`** — the repository's own descriptor, written to answer
exactly this question. Take it and cite it.

```sh
gh api repos/<org>/<name>/contents/.luma/project.md --jq .content | base64 -d
```

**2. Derived, with the source recorded.** No descriptor: fall back to the
readme's opening line or the hosting description, and **say where it came from.**
Both were written for a human who had already arrived, so they usually answer a
different question — which is why this is second, and visibly so.

**3. Absent.** Nothing usable: **leave `description` out.** *Nobody has said what
this is for* is honest, findable, and fixable.

### Never invent one

**An invented description is indistinguishable from an authored one**, and
something selecting repositories on a guess is worse off than something that
knows it does not know.

Deriving is not inventing — the difference is provenance. A fallback recorded
with its source stays visibly second-best. **A sentence composed from reading the
code and stored as though the project said it does not**, and it will be
believed, propagated, and never corrected, because nothing marks it as a guess.

### Offering to write one

Closing the gap properly means the repository gets its own descriptor, and that
is worth offering.

**Ask per repository, and never in bulk.** An organization owner may not own
every repository in it, and a sweep that opens forty pull requests is one
somebody has to apologize for.

**It goes as a pull request against that repository**, never a direct commit.
The descriptor is a claim the repository makes about itself, so its own people
decide the wording — and the direction of this bundle is *collect*, which
writing into a project repository inverts.

**Only where `.luma/` already exists.** A repository that has not adopted it has
nowhere to put a descriptor, and having something to file is not a reason to
introduce a directory structure into somebody's project. Report that as the gap
it is.

What belongs in one is `luma/project-documentation`'s business, not this
bundle's.

**Never overwrite an adjudicated value with a derived one.** If somebody wrote a
better description by hand, refreshing must not replace it. The presence of
`sources` for that field is what tells you which it was — which is exactly why
that field is recorded.

## 6. Notice what changed, and say so

A refresh that silently rewrites entries has hidden the interesting part.
**Report the deltas**, not the totals:

- Repositories that appeared or disappeared.
- **Visibility changes** — anything that became public deserves its own line.
- Anything newly archived.
- Descriptions that changed materially.

**Totals are noise; changes are the product.** *"48 repositories indexed"* tells
nobody anything they can act on.

## 7. Regenerate the index

`repositories/index.md` is generated from the entries. Rewrite it whole; never
hand-edit it.

Enough to scan: name, one line, in-scope or not, and a link. **A generated file
that disagrees with its source is a second answer nobody asked for**, so if the
index and an entry conflict, the entry wins and the index was stale.

**State the coverage on its face**, and mark restricted entries as such.

**If the organization has asserted the index is complete, reproduce that
assertion with its scope** — which accounts, whether restricted repositories are
included, as of when. **Otherwise say what the sweep covered** and leave it
there.

Both readings are load-bearing. A reader who takes a partial index for a census
concludes that what is not listed does not exist; a reader who treats a
genuinely complete one as partial hedges every conclusion and wastes the effort
that made it complete.

## 8. Commit it into the headquarters

**Run the step 0 gate again, immediately before writing.** All four checks, not a
recollection that they passed earlier. A sweep takes time, branches get switched,
and **the only check that counts is the one performed against the state you are
about to write into.**

An index of private repositories in the wrong repository publishes the shape of
the organization in a single commit, and no later correction removes it — a
merged pull request keeps its own refs, which the repository owner cannot alter
or delete.

**If any check fails, write nothing and say which one.** Not a partial commit,
not a local file kept for later, not a suggestion of somewhere else it could go.
**The absence of a destination is the finding.**
