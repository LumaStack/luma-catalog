---
type: workflow
title: Create the store
description: Initialize .luma/ in a repository that does not have one. Use when setting up luma in a project for the first time.
---

# Create the store

## 1. Check whether one exists

```sh
ls -d .luma 2>/dev/null
```

If it is there, this is not the workflow you want — see [[migrate-store]] for
moving an existing structure into it, or just add what is missing.

## 2. Create only what will have contents

```sh
mkdir -p .luma/records
```

**Do not create all four directories up front.** An empty `backlog/` is a
question a reader has to answer — *is this unused, or is something broken?* —
and directories cost nothing to add on first use.

`records/` is the usual exception: something will write an audit or a decision
almost immediately.

## 3. Ignore nothing

`.luma/` is committed in full. There is no `.gitignore` entry to add, and
adding one breaks the invariant the store depends on — see
[[the-luma-directory]] for why two agents reading different rules is a
correctness failure rather than an inconvenience.

If something in here should not be committed, it is machine-local state and
belongs in `~/.config/luma/` instead.

## 4. Commit it before using it

An empty committed store is a claim that this project has one. A store that
exists only on your machine is not a store — it is a directory that will
surprise the next person to clone.

## 5. Adopt what you need

```sh
luma-foreman adopt luma/<bundle>
```

That creates `bundles/` and `bundles/adopted.toml` on first use. You do not
create either by hand — `adopted.toml` is tool-written, and a hand-made one will
disagree with reality the moment anything is adopted.
