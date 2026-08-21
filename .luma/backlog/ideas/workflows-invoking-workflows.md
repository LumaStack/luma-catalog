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
  record-the-run: { run: ..., level: require }
  refresh-index:  { run: luma/organization-internal-hq#index-repositories, level: recommend, absent: silent }
  fetch-extras:   { run: ..., level: optional }
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

**A preset over two fields.** `level` is mandatory and sets both defaults;
`present` and `absent` are written only to disagree with it.

```yaml
level:   require | recommend | optional | best-attempt    # mandatory
present: run | ask                                        # default: from the level
absent:  block | inform | pause | silent                  # default: from the level
```

| level | sets `present` | sets `absent` |
| --- | --- | --- |
| `require` | run | block, and help them install it — **if they decline, the workflow exits with an error** |
| `recommend` | run | inform |
| `best-attempt` | run | silent |
| `optional` | **ask** | pause, and ask whether to install it and then run it |

**`present` and `absent` as a pair is what makes it readable** — same shape,
opposite condition, and a reader who meets one knows the other exists. That
symmetry is worth more than the field count.

**`run` is the default for `present`, because the common case is a workflow doing
what it declared.** Asking is the exception, so the unusual entries are the ones
that look unusual — which is what matters when skimming forty of them.

**Nothing pauses when the tool is present, except `optional`.** Consent to the
workflow is consent to what it declares. Stopping to say *I recommend the thing I
told you I would do* is noise, and noise teaches people to skim past the pause
that mattered.

**`optional` is opt-in where the others are opt-out**, and it does not lean either
way. Declaring something optional is the author saying *I do not know whether you
want this* — so an agent that manufactures a recommendation is inventing an
opinion the author declined to have. It is also why its absence behaviour is to
ask about installing: it was already interrupting.

**`best-attempt` stays a preset rather than folding into `recommend` +
`absent: silent`.** Presets cost one word, `run` with a silent absence is common,
and writing the override every time is worse than naming it. Some skips are
noise, and a workflow reporting every optional thing it did not do trains people
to skim past the one that mattered.

**`level` is mandatory rather than defaulted.** It is the one field carrying the
semantics, entries are few per workflow, and every candidate default fails in a
different way: `require` blocks over tools nobody needed and is the only level
that may demand an install; `optional` pauses on every unlabelled entry until
people click yes reflexively; `best-attempt` means a forgotten annotation
silently never happens. `recommend` was the least bad — it never surprises — but
*absent refuses* is the instinct applied everywhere else here, and one word per
entry buys zero accidental semantics.

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
