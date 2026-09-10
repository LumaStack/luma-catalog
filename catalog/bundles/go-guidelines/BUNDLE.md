---
type: bundle
title: lumastack/luma-catalog/go-guidelines
version: 0.1.0
stage: draft
survival: probationary
consumers: [project, organization]
description: The Go guidelines this project writes against, which one wins when they disagree, and the linting floor that keeps half of them out of an agent's context entirely.
published: 2026-09-10
---

# lumastack/luma-catalog/go-guidelines

**Adopting this bundle is the declaration.** It says that this project writes
Go against the four published guidelines named below, in the order given, and
that the only thing permitted to overrule them is a decision this project
recorded and put in force. Precedent is not a decision.

**Nobody disputes what good Go looks like; they dispute which document says
so.** Effective Go, Go Code Review Comments, Google's Go Style Guide and Uber's
guide are all authoritative, all still published, and they contradict each
other on naked returns, receiver naming, error wrapping and when to define an
error type. Four guides with no ranking is not guidance — it is four answers
and a shrug. **The ranking is the substance of this bundle**, because it is the
one thing none of the sources can provide.

## What is here

**[[writing-go]]** — the four sources, what each is for, which wins when they
disagree, and how to read 130,000 tokens of guidance without spending a context
window on it. Open it before writing Go.

**[[mechanical-floor]]** — the linters, the configuration, and the check
script, so the rules a tool can enforce are enforced by a tool.

The two answer different questions, and the second is what makes the first
affordable. **Roughly half of what these guides say is mechanically
checkable** — seventeen of Code Review Comments' thirty-one rules, and about a
third of Uber's guide. Those belong in `scripts/check`, not in an agent's
attention. What is left is the half that needs judgment, and that is what
[[writing-go]] ranks.

## Why it points rather than carries

**This bundle carries only what we wrote, and points at everything anyone else
wrote.** One licence in the repository, no `NOTICE` file, no per-directory
attribution, and nothing an adopter inherits without knowing.

The licences would mostly have permitted carrying. Effective Go, Code Review
Comments and Google's guide are Creative Commons Attribution — no ShareAlike,
so a copy or even a summary is allowed with attribution. Uber's guide is
Apache-2.0, the same licence as this catalog.

**What decides it is not permission but propagation.** `foreman get` copies a
bundle into the adopter's repository, so carrying Uber's guide would make every
adopter a redistributor of Apache-2.0 material — owing a copy of the licence
and a notice of modification, in a repository that may not be Apache-2.0 at
all. Carrying the Creative Commons documents would do the same with attribution
obligations. **Carrying does not put a disclaimer in this catalog; it puts one
in everybody else's**, and they would inherit it without being asked.

**And carrying buys less than it looks like.** Reading a file from disk costs
exactly what reading it from the web costs — the tokens are the content, not
the transport. Vendoring would buy offline access and a pinned snapshot, at
the price of a snapshot that goes stale with nothing to say so. These
documents are maintained, and three of the four have changed materially since
the last time anybody wrote a summary of them.

**The cost, and what pays it down.** This bundle's referenced substance does
not arrive with the repository. Step zero of [[writing-go]] closes most of that
gap with a machine-local cache under `~/.cache/`, refreshed at most daily and
read by seeking rather than whole. That copy is never committed: on one machine
it is nobody's business, in a published repository it is distribution and
carries the licence with it.

What the cache cannot give back is reproducibility. A fresh clone on a machine
that has never fetched them has seven URLs and nothing else.

**Go Proverbs are the one exception, and a deliberate one.** [[writing-go]]
quotes ten of Rob Pike's aphorisms directly rather than linking them. Short
phrases attract thin copyright at best, quoting them attributed to their author
is universal practice, and a tiebreaker that requires a network fetch is not a
tiebreaker. The site collecting them is MIT-licensed; the aphorisms are Pike's.

## Consumers

Both levels. A project declares how it writes Go; an organization can require
the same of every project that writes any.

## Version

`0.1.0` — first published, and `probationary` on purpose.

**The ranking has not been tested against a disagreement that mattered.** It is
derived from reading the four sources and from what each says about the others
— Code Review Comments now describes itself as "a laundry list of common style
issues, not a comprehensive style guide" and points at Google's, which is why
Google's ranks first here. That is the sources' own view of themselves rather
than a judgment earned by using them, and the first real conflict may reorder
them.

**No distilled judgment layer, deliberately.** The obvious next document is our
own statement of the rules that survive the linters — roughly 14,000 tokens of
Uber's guide plus fourteen Code Review Comments rules. Writing it now would
mean inventing rules from reading rather than from cases, so it waits for real
ones. `luma-backlog` is the first adopter and the place they will come from.

**Two claims here are measurements, and both were taken rather than
estimated.** The token counts come from the sources fetched on 2026-09-10;
the split of Code Review Comments into mechanical and judgment is a
classification against golangci-lint v2.13.2's linter set, and it is the
number most likely to be wrong at the edges — several rules are partly
checkable, and which side they fall on is a judgment call.
