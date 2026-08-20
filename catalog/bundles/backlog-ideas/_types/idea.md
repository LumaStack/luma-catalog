---
type: type_definition
defines: idea
extends: document
fields:
  captured:
    obligation: mandatory
    field_type: date
    desc: "when it was written down — not when it was had, which nobody remembers"
  originated:
    obligation: mandatory
    field_type: actor
    desc: "who had the idea (§7.4). human: means a person did, whoever wrote it up"
  contributors:
    obligation: optional
    field_type: list
    desc: "anyone who shaped it afterwards — actors, same grammar as originated"
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

## The fields are few on purpose

Capture is the moment ideas are cheapest to lose and most expensive to
interrupt. Everything here is either free to write or optional at capture time.

`captured` is the date it was **written down**. Nobody remembers when they had
an idea, and a date invented after the fact is worse than the honest one.

`horizon` is the only judgement asked for, and **absent means `someday`** —
which is honest, since an idea nobody has classified is one nobody has decided
to do soon.

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

## `originated` is the human-or-not signal, not a credit line

The question it answers is **was a person involved in having this**, not who
deserves attribution.

- **`human:<id>`** — a person had it. Still true if an agent asked the question
  that prompted it, wrote every word of the file, and improved it afterwards.
  That agent is a `contributor`.
- **`agent:<model>`** — **no person was involved in having it.** This is the
  case worth being able to find: an idea nobody has looked at yet.

That distinction has to survive being written up, because agents write up
almost everything. Attribution by *who typed it* would mark every idea as the
agent's and lose the only signal that matters.

## Growth stages use `lifecycle_status`, not a field of their own

The gardening ladder is already the root type's:

| garden | `lifecycle_status` | means |
| --- | --- | --- |
| **seedling** | `draft` | captured, not yet thought about |
| **budding** | `provisional` | revisited at least once, taking shape |
| **evergreen** | `stable` | worked out, waiting only on capacity |
| **pruned** | `archived` | set aside, with `archived` dated |

Absent means `draft`, which is correct: everything starts as a seedling.

## Size is a symptom, not a limit

There is no length rule, because length is not the thing that has gone wrong. An
idea that has grown long has usually become **a backlog item wearing an idea's
clothes** — decided, scoped, and waiting only on someone to start.

*What actually triggers that transition is unresolved*, and it needs the backlog
tool to answer properly. Until then, an idea that reads like a plan is a signal
to ask whether it still belongs here — not a rule to enforce.
