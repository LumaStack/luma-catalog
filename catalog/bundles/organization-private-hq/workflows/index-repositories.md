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

**The host's description is a fallback, not the target.** What is wanted is a
sentence that answers *when should somebody open this?* — the same job a
workflow's `description` does. Most repository descriptions on a hosting account
do not answer it, because they were written for a different audience.

**Where the repository says it better, take that.** Its readme's opening line,
or its own project descriptor if it has one. **The repository owns this fact**;
the headquarters is only collecting it.

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

## 8. Commit it into the headquarters

**Check where you are.** These entries name the organization's repositories,
including private ones, and that is not a list to commit anywhere else.

**Confirm the repository is private before committing**, every time — see
[[verify-headquarters]]. Cheap, and the one check that matters most here: an
index of private repositories in a public headquarters publishes the shape of
the organization in a single commit.
