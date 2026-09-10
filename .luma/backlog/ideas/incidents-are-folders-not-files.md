---
type: luma/idea
title: An incident is a folder, because evidence does not fit in frontmatter
created: { by: human:benlinton, at: 2026-09-08T03:10:00Z }
contributors: [human:benlinton, agent:claude-opus-5]
horizon: next
scope: project
stage: draft
---

# An incident is a folder, because evidence does not fit in frontmatter

**An incident is a file today** — `.luma/records/incidents/INC-NNNN-<slug>.md` —
and incidents are exactly the records that arrive with attachments. Logs, a
screenshot, a transcript, an export, the report that went to somebody else.
There is nowhere to put any of it.

## Why a file is the wrong shape here specifically

**Supporting evidence is not prose and cannot be inlined.** A log excerpt pasted
into a record is an excerpt somebody chose; the file is the evidence. The
distinction matters most in the records where somebody will later ask *how do
you know*, and that is every incident.

**The type already leans on evidence it cannot hold.** `detected_by` names a
process, `began_at` is usually inferred from logs, and the type says outright
that *an estimate presented as a measurement is the most common lie in an
incident record*. The thing that would settle it is the log, which has no home.

**And the record is written under pressure, then revisited.** An incident is
drafted during and completed after — the type says as much when arguing for
`created_using`. Attachments accumulate across that gap.

## Shape

The same move `bundle-migrations` makes for the same reason — *a directory per
migration rather than a file, for the same reason a workflow carrying assets
gets one*.

```
.luma/records/incidents/
    INC-0007-retry-storm/
        index.md
        evidence/
            gateway-2026-09-08.log
            timeline.png
```

## Open

- **Whether `evidence/` is the name, and whether it is a tier.** The luma layout
  does not name a place for record attachments, so this may be a `luma-layout`
  question wearing an incident's clothes.
- **What listings do with a file that is not a record.** A directory of
  attachments will be walked by anything reading records, and a `.log` with no
  frontmatter is reported as a skipped record — a warning firing on a correct
  state, which is the kind people learn to ignore.
- **Whether every record type wants this**, or only the ones that carry
  evidence. Decisions and explorations are files with the same limitation and
  much less need.
