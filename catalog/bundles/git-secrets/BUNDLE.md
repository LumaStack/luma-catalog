---
type: bundle
version: 0.2.0
published: 2026-08-25
consumers: [project, organization]
entry_point: policy/never-commit-private-identity
description: Keeping credentials and private identity out of a repository — names, personal addresses, home paths, machine names, tokens and key files. Prevention first, then audit.
---

# Git secrets

Two kinds of thing must never reach a repository:

- **Credentials** — tokens, keys, passwords, and the files that hold them.
- **Private identity** — a real name, a personal address, a `/Users/<name>`
  path, a machine hostname.

Credentials are the obvious half. Identity is the half that leaks in practice,
because it rides on every commit's author field, where nobody looks.

What unites them is that **neither can be unpublished**. A repository is
mirrored, forked and cloned, so a commit is permanent in a way deleting it does
not undo — rewriting history does not recall the copies other people already
hold.

## What is here

**Policy**

- [[never-commit-private-identity]] — what must never appear, what to use instead, and why
  deletion does not undo it. Read first.
- [[never-commit-credentials]] — what counts as a credential, and why rotation comes
  before cleanup.

**Workflows**

- [[configure-identity]] — set a repository's commit identity so it cannot leak.
  Before the first commit.
- [[ignore-secret-files]] — ignore the files that are a credential by their name
  alone, before the tool that writes one exists.
- [[audit-sensitive-data]] — check what is already there, and decide what each
  finding is worth.

## Credentials and identity need opposite reflexes

Averaging them produces the worst of both — panic about an email address, and
complacency about a token.

| | a leaked credential | leaked identity |
| --- | --- | --- |
| **first move** | **rotate it, now** | decide whether cleanup is worth it |
| **urgency** | seconds — public pushes are scanned | none; the damage is already done |
| **can it be undone** | yes, by rotating | no. There is nothing to rotate |
| **often the right answer** | rotate, remove, move on | accept it, fix the config, stop the next one |

That is why they are two policies rather than one, in one bundle rather than
two: the same projects want both, at the same moments, checked by the same
command — but the advice diverges the instant something is found.

## Prevention leads

Prevention and detection both matter, and they are not equal. **Configuration
governs every future commit; an audit only reports the past**, and the past is the part that is often
not worth fixing. A project that audits without configuring finds the same thing
again next month.

## Adopted at either level

An organization decides which addresses are publishable and what its example
names are. A project applies that to its own commits and content. The documents
are the same either way, which is why `consumers` names both levels rather than
forcing the choice on whoever publishes.

## Version

`0.2.0` — **the manifest is `BUNDLE.md`.** Reserved markdown files are now
ALL CAPS across the estate, because nobody types all caps by accident: a file
becomes load-bearing only when somebody deliberately made it so, and writing
`bundle.md` now fails in the safe direction — ignored rather than silently wired
into machinery. Minor rather than patch, and pre-1.0 that is the tier for a
breaking change: anything naming the old path by hand stops resolving.

`0.1.0`. The identity rules come from a real leak found in a real repository and
the checks are implemented and tested — but these workflows have been run
against one machine's configuration and no other.
