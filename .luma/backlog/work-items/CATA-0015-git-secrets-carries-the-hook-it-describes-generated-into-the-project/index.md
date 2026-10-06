---
type: work-item
type_version: "0.0.2"
key: CATA-0015
title: git-secrets carries the hook it describes, generated into the project
workflow_status: captured
rank: 010.0150.000
kind: idea
stage: draft
created: {by: 'human:warden', at: '2026-09-25T16:12:31Z'}
description: 'add the hook to the bundle, using some kind of generator. git-secrets is prevention-first prose with no enforcement mechanism at all — it says to configure identity and ignore credential filenames, and ships nothing that stops a commit. A project wanting enforcement writes its own, as one adopter did five weeks before adopting the bundle. A static file cannot work, since a bundle is vendored read-only and the hook has to land in .githooks/, so delivery is by generator, of some kind not yet decided. The self-matching problem comes with it: prose teaching an address pattern trips an address scanner, which never-commit-private-identity admits happened to that document, and which an adopter currently solves by hardcoding an exclude pathspec — the fix that same policy calls wrong every time. Solved once upstream, it is solved for every adopter.'
modified: {by: 'human:warden', at: '2026-09-25T16:12:37Z'}
---

# git-secrets carries the hook it describes, generated into the project

## The problem

**The bundle is prevention-first prose with no enforcement mechanism.** Two
policies and three procedures: configure the commit identity, ignore the
filenames that are a credential by their name alone, audit what history already
published. Nothing stops a commit.

So a project that wants enforcement writes its own. One did — by hand, five
weeks before it adopted this bundle, on the same concern and in the same
vocabulary, independently. Nothing regenerates it, nothing tests it, and the
work stays in one repository.

## What is being delivered

The bundle carries the hook, and **some kind of generator** puts it in the
project. Which generator is open.

A static file in the bundle cannot do it: an adopted bundle is a vendored copy
that must not be edited, and the hook has to arrive at `.githooks/pre-commit`
with `core.hooksPath` pointing at it. Something has to write it out.

## Out of scope

- **Agent hooks.** FORE-0053 is `PreToolUse`, `UserPromptSubmit` and
  `SessionStart` delivering knowledge documents. This is git, and the shared
  word is the only thing they share.
- **Building the delivery mechanism**, if FORE-0004 reaches it first.

## Constraints

**The hook matches its own corpus.** Prose that teaches a reader what an email
address looks like trips a scanner for email addresses. `never-commit-private-identity`
records this happening to that document itself.

The workaround in the field is an exclude pathspec naming the bundle's
directory — and that policy calls exclusion the wrong fix every time, because
it *"changes nothing except your ability to see it"*. A generated hook could
read its exemptions from configuration rather than carrying them, which is the
switch CATA-0002 wants.

**It must not need context it may not read.** FORE-0004 is blocked on exactly
this, and any shared mechanism inherits the constraint.

## Notes

Relations found at capture, and where the seams are.

- **FORE-0004** — overlap, and the closest. Same mechanism: a git pre-commit
  hook for leak prevention, delivered by tooling rather than by memory. One of
  its three ways out is matching a project-local string, *"which writes the
  protected thing into the public repository"* — structurally the same defect as
  the pathspec above, reached from the other direction. The seam: FORE-0004
  covers the organization-name pattern and the boundary problem of a check
  needing configuration it may not read; this covers the address, home-path and
  digit-run patterns and a hook whose own corpus trips it. Whoever builds
  delivery builds it for both.
- **CATA-0002** — overlap. Wants a switch that turns one guardrail off without
  deleting it, most likely an override list in `.luma/config/`. That is the
  generated-hook form of a hardcoded pathspec, and it would remove the need for
  one.
- **CATA-0008** — overlap one level up. `outfit` is a working install mechanism
  with nothing to install; this is an adopted bundle with no mechanism to
  install from. Same gap, opposite half.
- **FORE-0053** — not a match, despite being the title anyone would reach for
  first.

Noticed in `luma-clarify`, where the hand-written hook refused a commit over
three placeholder addresses in this bundle's own vendored prose.
