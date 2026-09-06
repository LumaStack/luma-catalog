---
type: bundle
title: lumastack/luma-catalog/command-line-interface
version: 0.3.0
stage: draft
consumers: [project, organization]
description: How this project designs its command line — the guidelines it follows, and the style guide its own commands are written to.
published: 2026-09-03
---

# lumastack/luma-catalog/command-line-interface

**Adopting this bundle is the declaration.** It says that this project
designs anything a user types or reads back against
[clig.dev](https://clig.dev), and that the only thing permitted to overrule
it is a decision this project recorded and put in force. Precedent is not a
decision.

## What is here

**[[command-line-interface-guidelines]]** — the declaration, and how to
read the guide it points at. Open it before adding or changing a command, a
verb, a flag, or a message.

**[[command-line-style-guide]]** — the template every command's help
follows, explained a piece at a time, and the output conventions that go with
it. Follow it and a new command looks like the rest.

**[[ascii-styleguide]]** — the marks a command line shows state with, and the
rules that keep them readable without colour, without a font that has them, and
in a pipe. Six glyphs, fixed order, one meaning each.

The first two answer different questions. The first is *what should a command line
do*, which is somebody else's document and is pointed at rather than copied.
The second is *what should ours look like*, which is ours and is written out
in full.

## Why it points rather than restates

clig.dev is CC BY-SA 4.0. A summary of it is a derivative work, so a bundle
carrying one drags a second licence and a ShareAlike obligation into every
repository that adopts it — for prose that already exists, in one place,
maintained by the people who wrote it.

**The cost, and what pays it down:** this bundle's substance is not vendored,
so unlike everything else a project adopts it does not arrive with the
repository. Step zero of the policy closes most of that gap — a machine-local
cache under `~/.cache/`, refreshed at most daily, read by seeking rather than
whole. That copy is never committed: on one machine it is nobody's business,
in a published repository it is distribution and carries the licence with it.

What the cache cannot give back is reproducibility. A fresh clone on a
machine that has never fetched it has a URL and nothing else.

## Version

`0.3.0` — adds [[ascii-styleguide]]. The style guide settled what help looks
like and said nothing about how a command shows *state*, so every listing
invented its own — a word per row here, a checkbox there, and no two tools
agreeing on what a cancelled thing looks like against a failed one.

Six marks, and the argument is mostly about which distinctions are worth a
glyph. Unfinished work shares the circle and finished work changes shape, so
done separates from not-done before anything is read. Superseded and cancelled
get their own marks rather than borrowing the failure one, because neither is a
failure and marking them as one reports a loss where there was a decision.

It also fixes the things that make marks worse than words when they are done
carelessly: the heavy `✔` and `✘` rather than the light pair, since a finished
row should be the easiest to skip rather than the faintest; a fixed order, since
a view that reorders cannot be scanned; and colour that is redundant with the
glyph, so output survives a pipe and a reader who cannot see the hues.

`0.2.0` — adds [[command-line-style-guide]]. The guidelines policy says what a
command line should do and defers to a document this bundle does not carry; a
project still had nowhere to put the answers that document leaves open, so they
lived in commit messages and were re-derived differently each time. The style
guide is original writing about one project's own choices, so it adds no
licence obligation and is vendored in full — which also means it arrives with a
fresh clone, unlike the substance behind the first policy.

`0.1.0` — first published.
