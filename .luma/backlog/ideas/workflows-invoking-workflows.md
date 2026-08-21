---
type: idea
title: A shared language for workflows invoking other workflows
created: { by: human:benlinton, at: 2026-08-21T00:00:00Z }
contributors: [human:benlinton, agent:claude-opus-5]
horizon: later
scope: project
lifecycle_status: draft
---

# A shared language for workflows invoking other workflows

A workflow should be able to say that another workflow or command runs before it,
during it, or after it — and every workflow and tool should read that the same
way. The motivating case: `migrate-ideas` running `index-repositories` when the
index is stale, rather than reading a stale one and mentioning it.

## The problem it addresses

**Workflows already do this in prose, informally.** `index-repositories` says
*"read [[the-repository-index]] first"* and *"[[create-internal-hq]] is a
prerequisite"*. Nothing can act on either. An agent reads it, or does not.

**And the cross-cutting cases have no expression at all** — logging, journalling,
record keeping, rot checking, auditing. Every workflow needs them; none can say
so.

## The shape, as far as it got

**Declared in frontmatter with a slug, referenced by that slug in the body.**

```yaml
---
type: workflow
runs:
  refresh-index:  { run: luma/organization-internal-hq#index-repositories, level: best-attempt }
  record-the-run: { run: ..., level: require }
  fetch-upstream: { run: ..., level: recommend, absent: pause }   # override, rarely written
before: [record-the-run]
---
```

A marker naming `refresh-index` sits in whatever step it belongs to.

**Why not attach to a step number.** Numbers are positions. `migrate-ideas` was
renumbered on 2026-08-21 — a step inserted, 8→9 and 9→10 — and anything declaring
*run before step 8* would have moved silently, with nothing failing and no diff to
notice. A prose reference to "step 9" did break, and was caught by hand.

**Why a slug rather than inline.** Inline is renumber-safe but cannot be
pre-flighted: *does this workflow need anything I do not have* becomes
prose-parsing. Frontmatter is the manifest, the marker is the timing, and neither
duplicates the other.

**Slugs rather than identifiers.** These sit in a document people read.
`refresh-index` says what is about to happen; `a3f9c2` says go and look it up.

**Four levels, and they are not one ladder.**

| | when present | when absent |
| --- | --- | --- |
| `require` | must run; fail loudly | block, and help them install it. **If they decline, the workflow exits with an error** |
| `recommend` | pause, say why, let them decline | inform — or `pause`, if the maintainer overrides |
| `optional` | pause, ask whether they want it run | pause, ask whether to install it and then run it |
| `best attempt` | run it | do not run it, silently |

**`optional` and `best attempt` are opposites, not neighbours on a scale.**
`best attempt` is the quiet one — *do it if you can, do not bother me*. `optional`
is the loud one — *this is available, do you want it?* One defaults to yes and
says nothing; the other defaults to no and interrupts.

**`recommend` and `optional` differ by default, not by volume.** Recommend is *I
am about to, unless you stop me*. Optional is *shall I?*

The structure underneath:

| | initiates automatically | asks first |
| --- | --- | --- |
| **blocking** | `require` | — |
| **non-blocking** | `best attempt` | `recommend` leans yes · `optional` leans no |

**One field, four words, and a key most workflows never write.** There are two
real dimensions and neither derives from the other — what happens when the thing
is present, and how loud its absence is. Twelve combinations, of which these four
are the useful ones; *ask before running, then say nothing when it is missing* is
not a policy anybody wants. **A second field would expose all twelve to get four**,
and make every author set two things correctly instead of picking one word.

**`absent:` exists because exactly one cell is genuinely ambiguous.** For
`recommend`, whether a missing tool is worth stopping for depends on whether the
maintainer thinks somebody might go and install it mid-flow. Every other cell is
determined by what the level means — blocking *is* require, asking *is* optional,
quiet *is* best attempt.

**It defaults to `inform`, because a pause with no decision attached is only an
interruption.** The tool is not there; the user cannot run it either way.

**Five values and no key was the alternative** — split `recommend` in two. Not
taken: the two names would be near-synonyms, a reader would have to memorise
which meant which absence behaviour, and `absent: pause` says it on its face. If
a second cell ever proves ambiguous the key already covers it, with no fifth name
invented to find out.

**`best attempt` earns its place because some skips are noise.** A workflow that
reports every optional thing it did not do trains people to skim past the one
that mattered.

**Nothing installs without asking — but more than `require` may ask.** An earlier
version of this said only a required invocation could suggest an install. That
was really a rule against installing *silently*: `optional` is already
interrupting, so offering an install is the same interruption. What survives is
*never install unasked*, not *only require may ask*.

**A trigger is conditional on presence, never a dependency.** Bundles are
self-contained and depend on nothing — that is what makes promotion a directory
copy. A workflow naming another bundle's workflow must still work standalone with
every invocation absent.

**The caller may demand a pause, and the callee owns destructive consent.** A
caller knows things the callee cannot — *this is about to spend a minute on
network calls the user did not ask for*. But creating a repository or publishing
requires agreement no matter who called it.

## Why not now

Three things are unresolved, and the first is the motivating example.

**Conditions.** *Run it if the index is stale* is a predicate, and the four levels
have no room for one — they say how hard to push, never whether to bother.
Without conditions a `before` entry always runs or never does, which does not
express the case this started from.

**Organization-imposed versus workflow-declared.** Everything above is a workflow
declaring its own invocations. *Every workflow writes a record* is imposed on all
of them and nobody opts in — closer to a bundle with `obligation: mandatory` than
to a field in a workflow. It may be a second mechanism rather than a value.

**The name.** `trigger` is taken: *re-open trigger* runs through `DECISIONS.md`
and is the tightest term in the vocabulary. `cues`, `runs` and `checkpoints` were
considered without landing. `runs` is honest and boring; `cues` names the moment
rather than the action, which matters if one moment carries a log write, a rot
check and an invocation at once.

## Notes

Designed in conversation on 2026-08-21 across several exchanges. **Everything
above is unbuilt and unvalidated** — no workflow declares an invocation, nothing
reads one, and the four levels have met no real case except the one that produced
them.

**`horizon: later` is an assumption, not a judgement anybody made.**
