---
type: workflow
title: Initialize luma
description: Initialize .luma/ in a repository that does not have one. Use when setting up luma in a project for the first time.
---

# Initialize luma

## 1. Check whether one exists

```sh
ls -d .luma 2>/dev/null
```

If it is there, this is not the workflow you want — see [[migrate-into-luma]] for
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
adding one breaks the invariant `.luma/` depends on — see
[[luma-directory-layout]] for why two agents reading different rules is a
correctness failure rather than an inconvenience.

If something in here should not be committed, it is machine-local state and
belongs in `~/.config/luma/` instead.

## 4. Commit it before using it, except for empty directories

An empty committed `.luma/` is a claim that this project has one. A directory
that exists only on your machine is not part of the project — it is something
that will surprise the next person to clone.

**Git tracks files, not directories, so an empty one cannot be committed.**
`records/` therefore joins the repository with whatever is written into it
first, and until then it exists only where you made it. That is expected rather
than a step you missed, and it is not worth a placeholder file: `.luma/` holds
things that mean something, and `.gitkeep` would be the only entry that does
not.

What this step is really asking for is that **everything with contents is
committed before anybody relies on it** — `PROJECT.md` on day one, and each
directory as it earns a file.

## 5. Adopt what you need

```sh
luma-foreman get luma/<bundle>
```

That creates `bundles/` and `bundles/adopted.toml` on first use. You do not
create either by hand — `adopted.toml` is tool-written, and a hand-made one will
disagree with reality the moment anything is adopted.
