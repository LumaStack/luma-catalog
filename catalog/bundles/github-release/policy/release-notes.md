---
type: policy
title: Release titles and contents
description: What a release is called and what it must contain. Release notes are the only thing most people will ever read about a version.
---

# Release titles and contents

A pushed tag is not a release. **The tag is the mechanism; the release notes are
what people read**, and for most projects they are the only account of a version
that anyone ever sees. A changelog entry is a line in a file someone has to go
looking for; a release arrives in a feed.

Fill in [the template](../templates/release-notes.md) rather than starting from a
blank page — it carries the required sections in order.

## Titles

```
vX.Y.Z — what changed, in a few words
```

- **Lead with the version.** It is what people scan for and sort by.
- **Then say what changed**, in the fewest words that are actually specific.
- **Lowercase after the dash**, no trailing period. It is a label, not a
  sentence.

```
v0.0.8 — preload and entry_point
v2.1.0 — retries are configurable per endpoint
v3.0.0 — drops Node 18
```

**Name the change, not its size.** `v2.4.0 — big update`, `v1.1.0 — improvements
and fixes`, and `v0.4.0 — quality of life` all cost a reader the same thing:
they have to open the release to learn whether it affects them. A title that
says what moved lets most people stop reading, which is the point.

A release with no honest short title is usually a release doing too many
unrelated things.

## Required sections

**Changes, grouped** — Added, Changed, Deprecated, Removed. Only the groups that
apply.

Each entry says **what changed and why**, not only what changed. The outcome is
discoverable from a diff; the reasoning is not, and it is what someone needs
when deciding whether your change is a problem for them.

**Upgrading from vX.Y.Z** — what a user must actually *do*.

This is the most valuable section and the most often omitted. **Say plainly when
the answer is nothing**, which is usually the single most useful sentence in the
notes — it converts "I should read all of this carefully" into "I can upgrade
now."

It is not a copy of per-change migration notes. Those are written as each change
lands and are scattered; this is the whole upgrade in one place, written once
the release is known.

## Conditional sections

**Version category** — include it whenever the number is not what the rules
would obviously produce: a breaking change shipping as a patch under a pre-1.0
allowance, a large release that is only a minor, a skipped deprecation cycle.

Unexplained, these read as mistakes later — most often to the person who made
them. One sentence at the time is cheaper than the archaeology.

**Known issues** — anything shipping broken, and what to do instead. A release
that hides a known defect buys a day and spends a reputation.

## What to leave out

- **Commit-log dumps.** A list of commit subjects is not release notes. If the
  tooling offers to generate one, it is a starting point, not the artifact.
- **Internal churn** — refactors, test changes, dependency bumps nobody can
  observe. If a user cannot tell it happened, it does not belong.
- **Thanks and ceremony above the content.** Fine at the bottom; costly at the
  top, where the reader is still deciding whether this affects them.

## A pointer to the full history

End with a link to `CHANGELOG.md`. Release notes are per-version and a reader
often arrives needing the shape of several.
