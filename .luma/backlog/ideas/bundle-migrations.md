---
type: luma/idea
title: Bundle migrations — walking an adopter from version X to version Y
created: { by: human:benlinton, at: 2026-08-19T00:00:00Z }
contributors: [human:benlinton, agent:claude-opus-5]
horizon: later
scope: project
lifecycle: draft
---

# Bundle migrations — walking an adopter from version X to version Y

**Wanted, not designed.** A way to say *here is how to get from version X to
version Y*, so an adopter several versions behind can be walked forward rather
than left to work it out from a changelog.

```
<bundle>/migrations/0.2.0/migration.md      what to do to arrive at 0.2.0
<bundle>/migrations/0.3.0/migration.md
```

Mostly prose an agent follows, with scripts alongside where a step is
mechanical. A directory per migration rather than a file, for the same reason a
workflow carrying assets gets one.

## The reframe that makes it tractable

**A migration is about the adopter's content, not the bundle's.**

Re-vendoring already replaces the bundle wholesale — the new version arrives by
copying, and nothing needs migrating inside it. What breaks is **everything
outside the bundle that depended on the old shape**: the project's own documents
linking to a renamed one, its configuration naming a moved path, records written
against a Type Definition whose fields changed.

That is the whole job, and stating it that way keeps the scope from swallowing
the upgrade process entirely.

## Where it goes: `bundle-manager`, not the format

It earns a type by the §10.4 test — a consumer **consults** it, reading every
migration and computing which to run in what order, where a `workflow` is
*chosen* rather than derived.

It fails the further test for being built in. The format's machinery does not
depend on it, and ubiquity is unmeasurable because **zero migrations exist** —
predicting would be exactly what the ubiquity test now warns against. There is a
cleaner line too: `bundle` is in the format because a Bundle is the unit of
distribution it defines, while *upgrading between versions* is the adoption
lifecycle, which the format deliberately does not cover.

If most bundles turn out to carry migrations, that count is the argument for
promoting it later.

## Design, as far as it is settled

- **`extends: workflow`.** A migration *is* a procedure an agent runs. It adds
  version metadata and is selected by comparison rather than by choice, and
  inheriting says both at once.
- **Name the directory for the version it migrates *to*.** `0.2.0/` reads as
  *to get here, do this*, and chaining becomes a version sort. An arbitrary
  identifier needs a second field to establish order.
- **Reversibility is a field.** Some migrations are one-way in practice —
  splitting a `decision_log` into individual records is the known case, since
  each record then accumulates its own history that collapsing would discard. A
  migration that does not say so is one somebody tries to undo.
- **A migration that needs a person says so.** An agent that attempts an
  unautomatable step is worse than one that stops and explains.
- **Migrations never run on adoption.** A migration carrying a script is fine —
  that is code invoked deliberately. `foreman adopt` running one automatically
  is code executing as a side effect of fetching, which is the supply chain the
  bundle model refuses. Deliberate invocation only, always.

## What foreman would do

Read `adopted.toml` for the version in place, read the bundle's `migrations/`,
select every migration whose target is above the current version and at or below
the desired one, and run them in ascending order.

No solver, no constraints, no graph — a sort. Worth saying because it looks like
dependency resolution and is not.

## Open, and worth settling before building

**Distinguishing "no migration needed" from "migration missing."** A bundle
going `0.1.0` → `0.2.0` → `0.4.0` with nothing for `0.3.0` might have needed
nothing, or might have a hole. Nothing tells them apart, and an adopter crossing
the gap silently skips whatever was required. Possibly every version needs an
entry, with most saying *nothing to do*.

**Partial failure.** The same shape as a half-created worktree: leave nothing or
leave everything. A migration that stops halfway produces an adopter confidently
running against a state neither version describes.

**Accumulation.** Migrations pile up forever and nothing prunes them. Dropping
those below the last major is the obvious rule and would strand anybody further
behind than that.

**Local drift.** An adopter who edited their vendored copy — already a finding —
has content a migration's assumptions do not hold for. Refusing to migrate a
drifted bundle is probably right, and it makes drift block an upgrade, which
some adopter will resent at exactly the wrong moment.

## Notes

Migrated from `luma-foreman/docs/IDEAS.md` on 2026-08-21. `created.at` is a
day-level estimate from git history.

**`bundle-manager` already records this gap in writing.** Its `migrate-bundle`
workflow closes with *"What migration cannot do — it cannot carry adopters
across. A bundle that moves or changes shape has no way to update the copies
already vendored into projects… Adopters re-adopt, or they do not. That is a real
gap rather than an oversight."* This idea is the answer to that sentence, which
is also why it belongs in that bundle.

**A name collision is waiting.** `migrate-bundle` opens *"Two different moves
wear the same word"* — promoting between catalogs, and restructuring in place.
This would be a third thing called migration, and the one most easily confused
with the other two. Worth settling before it ships rather than after.

**`bundle-manager` has no `_types/` directory**, so the `type_definition` this
proposes would be its first.
