---
type: type_definition
defines: sweep
fields:
  scope:
    field_presence: required
    field_type: text
    desc: "what is being read — and, in the body, what deliberately is not"
  ordering:
    field_presence: required
    field_type: text
    desc: "the order units are taken in: narrative, risk-weighted, dependency, directory"
  indexed_at:
    field_presence: required
    field_type: text
    desc: "the 12-character commit the index was last reconciled against"
  contributors:
    field_presence: recommended
    field_type: list of actor
    desc: "everyone reading in this sweep, human and agent alike (§7.4)"
  archived:
    field_presence: optional
    field_type: date
    desc: "when the sweep was closed and moved to archived/"
---

# Sweep

One long read of a codebase, by a person, with an agent beside them. The
Document carries the scope, the order, and the index of what has been covered.

**It is not a record**, and the fields say so: `indexed_at` moves, the index is
edited at every sitting, and there is no commit pinning what the sweep is true
of — because a sweep is true of a moving target by construction. What it does
carry is enough to resume it and enough to check its coverage.

*Only what the format does not already have is declared here.* `created`,
`lifecycle_status` and `title` are core fields and are used as they come.

## `scope` must say what was left out

The half people skip, and the one that decides whether finished coverage means
anything. *"Everything under src/ and docs/; not the vendored tree, not the
generated clients"* is a scope. *"The repository"* is not — a reader cannot then
tell an empty row from an excluded one.

**Say which exclusions were given to you and which you chose.** An area the
owner ruled out reads differently from one you ran out of appetite for.

## `ordering` is not decorative

It is what makes the sequence checkable afterwards, and what a sitting consults
when the convenient next unit is not the correct one. Record the reason in the
body — the field carries the name, the prose carries why.

**Changing it mid-sweep is legitimate and gets a dated line in the body.**
Silently drifting from it is what the field exists to make visible.

## `indexed_at` is what keeps the index honest

The tree moves under a sweep — by the sweep's own fixes, if nothing else — so
every sitting reconciles the index from this commit to `HEAD` and then advances
it. Without it, reconciliation is a guess about what has already been accounted
for.

## No coverage field

**Coverage is derived from the sittings, never stored.** Each sitting says what
it covered; the index in the body is a cache of that, and the number in a
closing summary is computed at closing time.

The table in the body is edited constantly and will eventually be wrong. That is
tolerable precisely because it can be rebuilt — **when the index and the
sittings disagree, the sittings win.**
