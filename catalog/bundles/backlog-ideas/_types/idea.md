---
type: type_definition
defines: idea
extends: document
fields:
  horizon:
    obligation: recommended
    field_type: enum
    values: [next, later, someday]
    desc: "how soon this needs deciding. Absent means someday"
  scope:
    obligation: recommended
    field_type: enum
    values: [project, department, organization]
    desc: "whose idea it is, and therefore where it lives"
  archived:
    obligation: optional
    field_type: date
    desc: "when it was pruned — the clock retention is measured from"
---

# idea

Something worth doing that nobody is doing yet, written down so it is not lost
while the current task continues.

**It is not a task, a plan, or a specification.** An idea that is fully worked
out has stopped being one; see the growth stages below.

## Three fields, because the root already has the rest

An earlier draft of this type declared `captured` and `originated`. Both were
core fields wearing new names:

| declared | is really |
| --- | --- |
| `captured` | `created.at` |
| `originated` | `created.by` — and **immutable**, which is what an origin should be |

`created` is an `actor_event` (§7.1) carrying **both** the author and the time.
Declaring either half again would have produced two fields holding one fact,
free to disagree.

`created` is `optional` at the root and inheritance is add-only (§10.3), so this
type cannot strengthen it. **Treat it as required in practice** — an idea with no
date and no author cannot be tended, because tending reads exactly those two
things.

## `created.by` answers *was a person involved*

Not *who typed it*. The specification is explicit that `created.by` is the
original-author record and that a git author is often merely whoever was running
an agent.

**An agent that transcribes an idea without shaping it is not its author**, any
more than a keyboard is. The person who had it is.

`created.by: agent:<model>` therefore means something precise and worth being
able to find: **no human had this idea.**

## The one rule: a person appears only if they saw it

**The question this type exists to answer is whether an idea passed a human by
without notice.** Everything about authorship and contribution serves that and
nothing else.

So the rule is uniform across every field that names a person:

> **Record a human only when they saw the idea and responded to it.**

Not *a session was open*. Not *they were nominally present*. An agent running in
auto mode while nobody is reading, or working in a subprocess whose output never
surfaced, has **not** had a human present — whatever the session claims.

From an agent's side this is testable rather than a judgement: **did I show this
to them and get a reply?** If not, do not name them. That is what makes the
propose-before-filing step load-bearing rather than courteous — it is what
produces the evidence.

## Which field depends on what they did

| what happened | where it goes |
| --- | --- |
| they had the idea | `created.by` |
| they led the agent to it, or shaped it in the exchange | `contributors` |
| they read it afterwards and approved it | `verified` |

**Leading counts as having it.** If a person steered an agent toward an idea and
the agent produced the words, it is as much theirs — `created.by: human:` with
the agent as a contributor, not the reverse.

**The check spans all three.** An idea that passed everybody by is one with no
human in `created.by`, `contributors`, or `verified`:

```yaml
created: { by: agent:opus-5, at: 2026-08-20T09:00:00Z }
# no contributors, no verified — nobody has seen this
```

Once a person reads it, a `verified` entry clears that. They have not authored
or shaped it, and recording them as though they had would be a different lie
than the one this avoids.

## Being named is not endorsement

`contributors` records involvement; `verified` records vouching. A bad idea's
contributor list says who was in the exchange, not who stood behind it, so
nobody inherits blame for an idea they were merely party to.

**And nobody is named for an idea they never saw.** Telling a person *you did
this* about something unfamiliar is worse than an incomplete list — it reads as
a verification that never happened, and it can attach somebody to a mistake they
had no part in.

## `horizon` — three values, and deliberately no fourth

| | |
| --- | --- |
| `next` | wants deciding within the current stretch of work |
| `later` | real, and not now. The bulk of a healthy list |
| `someday` | worth remembering, may never happen, and that is fine |

Borrowed from *Now / Next / Later* roadmapping and GTD's *someday*, because both
are widely understood and neither needed inventing.

**There is no `now`.** Something being done now is not an idea, it is work.
Adding that value would invite this to become a task list, which is the failure
this type most needs to avoid.

**Absent means `someday`** — honest, and it costs nothing to leave off at
capture.

## Growth stages use `lifecycle_status`

The gardening ladder is already the root type's:

| garden | `lifecycle_status` | means |
| --- | --- | --- |
| **seedling** | `draft` | captured, not yet thought about |
| **budding** | `provisional` | revisited at least once, taking shape |
| **evergreen** | `stable` | worked out, waiting only on capacity |
| **pruned** | `archived` | set aside, with `archived` dated |

Absent means `draft`, which is correct: everything starts as a seedling.

`archived` is the one date the root cannot supply. `modified` advances on every
edit, so it cannot say *when this was set aside* — and retention, once it is a
setting, has to measure from something that does not move.

## Size is a symptom, not a limit

There is no length rule, because length is not the thing that has gone wrong. An
idea that has grown long has usually become **a backlog item wearing an idea's
clothes** — decided, scoped, and waiting only on someone to start.

*What actually triggers that transition is unresolved*, and it needs the backlog
tool to answer properly. Until then, an idea that reads like a plan is a signal
to ask whether it still belongs here — not a rule to enforce.
