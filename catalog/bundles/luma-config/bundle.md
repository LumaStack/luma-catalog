---
type: bundle
version: 0.1.0
published: 2026-08-19
consumers: [project, organization]
entry_point: policy/where-configuration-lives
description: Where luma configuration lives, what is committed and what belongs to the machine, and the order in which layers win.
---

# Luma config

Two homes and one rule of thumb:

```
.luma/config/          committed. What this project declares
~/.config/luma-*/      yours. Not committed, near enough always
```

**The reverse is the failure that matters.** Committed-but-personal is somebody's
private business. Uncommitted-but-inside-`.luma/` means two agents on two
machines read different rules for the same code, which is a correctness problem
in the one place whose job is saying what the rules are.

## What is here

- [[where-configuration-lives]] — the two homes, the XDG reasoning behind the
  machine-local side, and the test that tells configuration from cache. Read
  first.
- [[configuration-precedence]] — six layers, and why the committed file appears
  twice.
- [[add-a-setting]] — the four questions that decide where a new value goes.

## The two ideas worth carrying

**If deleting it loses a decision somebody made, it is not cache.** One question
that resolves nearly every placement, and the failure it prevents is nasty:
putting a decision under a cache path means clearing caches silently reverts
behaviour, and nobody suspects the cache because caches are meant to be safe to
clear.

**A project may suggest and may mandate, and those are different tables.**
`[defaults]` is a starting value somebody may change; `[require]` is a rule a
local preference cannot lift. Splitting them puts the precedence in the file
rather than in something a reader has to remember — and it corrects an earlier
formulation, *the committed declaration always wins*, which was too broad and
would have forbidden a project offering newcomers a sensible default.

## Naming, on both sides

Inside `.luma/config/`, files are named for the tool that reads them —
`foreman.toml` rather than `config.toml` — so several tools coexist without
negotiating a schema.

Outside, XDG decides: `~/.config/luma-foreman/`, application-named, **never**
`~/.config/luma/foreman/`. Nothing nests under a vendor, and shared
configuration across tools would be its own application sitting beside them.

The two sides differ in shape because they answer to different authorities. A
project has one set of rules, so `.luma/` is one directory. The machine-local
side is one directory per application because XDG says so and every other tool
on that machine agrees.

## Consumers

Both levels. An organization's headquarters is a repository and configures its
own tooling the same way.

## Version

`0.1.0`, and the precedence chain is **designed rather than built** — only one
layer is read today. The rules here are what the chain will be when it exists,
which makes them worth writing down now and worth re-checking against the first
tool that implements more than one.
