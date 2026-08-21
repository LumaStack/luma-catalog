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
invokes:
  record-the-run: { workflow: acme/journal, level: require }
  refresh-index:  { workflow: luma/organization-internal-hq#index-repositories, level: recommend, absent: silent }
  need-gh:        { command: "gh", level: require }
  load-security:  { bundle: luma/git-secrets, level: recommend }
before: [record-the-run]
---
```

A marker sits at the point in the body where it should play:

```
luma-invoke: refresh-index
```

**`luma-invoke:` — namespaced, consistent with `.luma/` and the format's own
name.** Bare `invoke:` would probably survive prose, since *invoke* is rare in
ordinary writing where *run* is constant. It is not worth the residual risk: a
marker that can occur by accident is one that eventually will, and this one
changes what an agent does.

**The namespace is a settled position, not a new one.** The same reasoning chose
a vendor-named `.luma/` over a generic directory — the namespace is owned, so
nobody can claim it out from under you — and the format itself is
`luma-knowledge-format`. A prefix here is consistent rather than exceptional.

**The field and the marker share a root** — declare it in `invokes:`, place it
with `luma-invoke:`. Nothing to remember.

### `luma-invoke:` is reserved, and reserving prose is new

The format already reserves names — `document`, `concept`, `workflow`, `policy`,
`bundle`, `type_definition` belong to it and a bundle should not redefine them.
Those are **frontmatter type names**. This would be the **first token the format
reserves inside prose**, which needs two things a type name does not.

**Where it is active.** A line whose first non-whitespace content is
`luma-invoke:`. **Inert inside a fenced code block** — otherwise documentation
showing an example fires it, and every document explaining this feature becomes a
document that performs it.

**What a tool that has not implemented it must do.** The permissive-conformance
law says no consumer rejects a bundle over something it does not understand, so
rejecting is out. **But ignoring is worse**: a `require`-level invocation that
silently does not happen is the failure this whole design exists to prevent.

So the rule is neither: **a tool that meets `luma-invoke:` and cannot act on it
says so.** Unimplemented is not the same as absent, and the difference has to
reach the person. That is the same distinction the levels draw between `inform`
and `silent`, applied one layer down to the tool itself.

**And reserving it means nothing else may use the token** — not as a heading, not
as a field, not as prose. That is the cost of a keyword and the reason it is
namespaced: `luma-invoke:` is unlikely to be wanted for anything else, where
`invoke:` might be.

**It must render visibly.** An HTML comment would hide it, and invisible
behaviour is the tax this design exists to avoid.

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

**A target is a workflow, a command, or a bundle, and which one is declared
rather than inferred.** Exactly one of `workflow:`, `command:` or `bundle:`; more
than one, or none, is a publish-time error. Sniffing the type from the shape of the value would be
implicit typing, and this system chooses declaration over inference everywhere
else.

**`invokes:` is the format's own word.** SPEC partitions the three base types by
how a Document is engaged with, and a workflow is the one that is **invoked** —
so the field and the type it sits on agree rather than describing the same thing
two ways.

**It covers every target, once *invoke* is read properly.** The narrow reading is
*execute*, which is why `bundle:` looked like a misfit. The other sense — **call
upon, bring into force** — is ordinary English: invoke a clause, invoke a right,
invoke a precedent. *Invoke a policy at step twelve* means bring it to bear here,
which is exactly the operation.

`runs:` and `calls:` are true of two targets out of three. `uses:` is true of all
three and says almost nothing — it was a vaguer word chosen to make a merge read,
when the merge was fine. `needs:` is worse than weak: it names a *dependency*,
contradicting the rule below that an entry is conditional on presence and never
one.

**The one cost:** to a programmer *invoke* leans toward execution, so `bundle:`
may momentarily read as *run the bundle*. One sentence of documentation fixes it.

**Bundles are opaque in a way even workflows are not, which is why they belong
here.** A workflow runs and finishes; **a loaded bundle persists**, bringing
policy and guardrails that shape every decision afterwards, with nothing marking
where that began. *Go read it* means the whole bundle, not one document — and its
`preload: mandatory` documents pull in more, so the reachable set is not visible
from the manifest either.

**All four levels fit a bundle**, which is the confirming signal. Unlike a plain
document, where `optional` is nonsense — nobody pauses to ask permission before
reading — *shall I load the security policy bundle?* is a fair question, because
loading costs context and changes behaviour.

**`preload` supplies the payload, not the timing.** It is eager and
non-negotiable: adopted bundle, documents in context from the start, nobody
chooses — and that is exactly what makes it the right enforcement path for policy
and mandates. What it cannot do is load something at step twelve, conditionally.
So a `bundle:` entry says **when** and **whether**; the bundle's preload set
answers **what arrives**, because its author already decided what is needed in
order to work with it.

**This is where a prose `when` earns its place most clearly** — *load the
TypeScript policy when the project actually has TypeScript* is the case no level
can express.

**Commands and documents stay out, because the contract is for opacity.** A
fenced command shows its whole self before it runs. A `[[wikilink]]` is
transparent and changes nothing. Neither needs declaring, and agents already
handle both. **`command:` is a narrow escape hatch** for when the *absence*
behaviour is invisible — `gh` being missing is not in the fence — and a fenced
command remains the normal way to run one.

**A workflow can refuse; a command cannot — and that asymmetry is load-bearing.**
The rule elsewhere is that the callee owns destructive consent: creating a
repository or publishing requires agreement no matter who called it. A shell
command has no prose, no level of its own, and no way to stop and ask. **For a
command, the caller's `level` is the only protection there is** — so a
destructive one wants `optional`, or an explicit warning in the prose beside the
marker, because nothing downstream will do it.

**Conditions are prose in the body, introduced by *when*, beside the marker.**

> Refresh the index first when it is past its `stale_after`. `[[refresh-index]]`

**Because the consumer is an agent reading markdown, not a machine evaluating a
predicate.** A `when:` expression in frontmatter would be structured data, which
needs a vocabulary or an expression language — and that is the failure the tags
decision holds hardest against: *every policy system that collapsed did so by
growing one more operator at a time, each individually reasonable.* Prose has no
parser to grow.

**It also keeps the halves honest.** Frontmatter is machine-facing and answers
*could this run* — which is what pre-flight needs. The body is agent-facing and
answers *should it, here, now*. A condition refines **when**, not **what**, so it
belongs with the marker rather than the manifest.

**A condition must turn on something observable** — a date, a file's presence, a
declared value. *When the index is past its `stale_after`* is checkable and two
agents will agree. *When it seems out of date* is a vibe, and will be judged
differently every run.

### Writing a `when` two agents read the same way

**A loose, extendable contract — not a spec.** Nothing validates these and
nothing should. The point is enough shared shape that two readers reach the same
conclusion; breaking one should feel like writing badly rather than like an
error, and the consequence is a misread rather than a rejection.

**Extendable the way tags are.** These forms are a starting set, not a closed
list. An organization that keeps hitting a shape not covered here adds its own and
records it where its people will find it — the same move as extending a tag
vocabulary or a starter. **What must survive any extension** is the small part
that makes conditions readable at all: they turn on something observable, they
are testable when read, and an unevaluable one runs rather than skipping.

New forms are additive by construction. A reader who knows only the ones below
still reads those correctly, which is what makes extending safe.

```
When <artifact> <is | is not> <state observable right now>.
```

**Name the artifact, not the situation.** *When `repositories/index.md` is past
its `stale_after`* — not *when the index is out of date*. An agent can open a
file; it cannot open a situation.

**Prefer one condition to a compound.** *When A and B* is where prose starts
growing operators, and *and* invites *or*, which invites precedence. Where two
things genuinely gate it, that is often two invocations — or the same marker
placed in a step that only runs under the first.

**Testable at the moment it is read.** Present tense, checkable now. *When the
descriptor is absent* works; *when this will be needed later* is a prediction, and
two agents will predict differently.

**Do not restate the level.** *When it matters* is not a condition, it is the
difference between `require` and `recommend`. A condition says whether the
situation applies; the level says how much it costs to skip.

**If it cannot be evaluated, run it — this one is firm.** An agent that cannot tell whether the index
is stale should refresh it. This is safe precisely because of the standing
consequence below — anything invocable is cheap to invoke redundantly — and the
alternative fails silently: skipping when unsure means the thing quietly does not
happen and nothing says so.

**Most invocations need no condition at all.** Three things absorb the common
cases: a callee that is idempotent no-ops when nothing changed, so *skip if
fresh* never reaches the caller; placement answers *only in this branch*, since
the marker goes in the step where the condition already holds; and `optional`
answers *genuinely uncertain and expensive*, because if the callee cannot cheaply
decide, the caller — which has less information — certainly cannot.

**Standing consequence: a workflow that can be invoked must be cheap to invoke
redundantly.** That is the price of not having machine conditions, and
`index-repositories` already pays it — *it is idempotent or it is worthless*.

**Re-open trigger:** if anything ever *executes* workflows rather than reading
them, conditions have to become machine-evaluable. The bounded version is the
tags pattern — the invoked workflow publishes the conditions it understands,
callers pick from that list, and anything outside it is an error. A closed list
cannot grow an operator at a time.

**A trigger is conditional on presence, never a dependency.** Bundles are
self-contained and depend on nothing — that is what makes promotion a directory
copy. A workflow naming another bundle's workflow must still work standalone with
every invocation absent.

**The caller may demand a pause, and the callee owns destructive consent.** A
caller knows things the callee cannot — *this is about to spend a minute on
network calls the user did not ask for*. But creating a repository or publishing
requires agreement no matter who called it.

## Two questions, closed

**Organization-imposed invocations: not a mechanism.** The worry was that an
organization wants behaviour inside workflows it did not write and cannot edit.
It dissolves into two cases that already have answers. **One workflow needing an
organization-specific change** is a fork into your own catalog — supported,
cheap, and the promotion path back upstream is designed for it. **Every workflow
should journal** is a *runner* concern: whatever executes workflows writes the
record, no workflow declares anything, and nothing needs an attachment point. It
felt like injection only because journaling was being pictured as something a
workflow *does*, when it is something that happens *around* a workflow being done.

**Deferred: extension points, or plugins.** A workflow declaring named interior
places that others may attach to, filled by an organization's catalog. Rejected
for now as overkill — it charges every workflow author a maintenance obligation
in exchange for a case nobody can name concretely. **Re-open when somebody can
name a real instance** of wanting custom behaviour at interior points of several
workflows they did not write, which forking the few that matter does not serve.

**The name: `invokes:` for the field, `luma-invoke:` for the marker.** `trigger` was
unavailable — *re-open trigger* runs through `DECISIONS.md` and is the tightest
term in the vocabulary. `runs:` held it while the targets were workflows and
commands, and lost the moment bundles joined: you do not run a bundle. `uses:`
replaced it and was too vague to carry anything. `needs:` names a dependency
where the design insists on none. `cues` and `checkpoints` were considered
earlier and did not survive.

## Notes

Designed in conversation on 2026-08-21 across several exchanges. **Everything
above is unbuilt and unvalidated** — no workflow declares an invocation, nothing
reads one, and the four levels have met no real case except the one that produced
them.

**`horizon: later` is an assumption, not a judgement anybody made.**

**Nothing here is unresolved any more, but nothing is built either.** The design
settled over one long conversation; no workflow declares an `invokes:` block, nothing
reads one, and the four levels have met no real case except the one that produced
them. **The first workflow to declare an invocation is the test**, and it will
probably find something this could not.
