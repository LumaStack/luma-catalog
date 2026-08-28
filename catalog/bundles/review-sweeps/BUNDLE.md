---
type: bundle
version: 0.1.0
published: 2026-08-28
consumers: [project]
entrypoint: policy/how-a-sweep-is-stored
description: Reading a whole codebase with an agent beside you — ordered, resumable, file by file, with the person's own read as the thing being protected.
---

# Review sweeps

Reading your own project properly is a thing people intend and do not do. It has
no natural unit, no end, and no way to tell at any moment how much is left — so
it starts, covers whatever was interesting, and stops without anybody deciding
it had.

A **sweep** gives it the three things it lacks: an order chosen on purpose, an
index that makes coverage checkable, and a unit of work small enough to finish
in an evening. It runs for weeks and survives every session boundary in between,
because all of its state is on disk rather than in a conversation.

## What is here

**Policy**

- [[how-a-sweep-is-stored]] — where it lives, why it is backlog rather than a
  record, and the two units that get confused. Read first.
- [[the-pairing-turn]] — orientation before the person reads, judgement only
  after they have spoken. The rule the practice is built around.
- [[choosing-an-order]] — four orders, what each buys and costs, and why the
  choice is recorded.
- [[what-a-sitting-produces]] — where each reaction goes, and why nothing worth
  keeping stays inside the sweep.

**Workflows**

- [[start-a-sweep]] — scope, order, index, and an honest estimate of the size.
- [[review-next]] — one sitting. This is the loop, and it is also how a sweep
  is resumed.
- [[close-a-sweep]] — finish or abandon one without the index telling a lie
  afterwards.

**Templates** — [a sweep](templates/sweep.md) · [a sitting](templates/sitting.md)

## Worth knowing before reading further

**The person's own read is the product.** An agent that opens a file with a list
of findings has already done the review, and what is left for the person is to
agree — which they will. The sweep then produces the agent's judgement with
somebody's name on it, and it looks exactly like success.

Everything about the turn order follows from that. **Facts may be offered at any
time; verdicts wait until the person has spoken.** *This is called from three
places, one of them holding no lock* is orientation. *This is over-engineered* is
a verdict.

**It is not an audit, and the difference is not rigour.** An audit pins a commit
and separates the party that finds from the party that answers. A sweep has
neither: the code moves as you go, and the person finding is the person fixing.
Filing a sweep as an audit produces a commit pin that is false by the third file
and a response written by its own auditor.

**Coverage is derived, not stored.** Each sitting says which files it covered;
the index in `sweep.md` is a cache of that. When they disagree, the sittings win.

**Nothing worth keeping stays in the sweep.** It is backlog — it gets archived
and eventually deleted — so a fix, an idea, a decision or a finding leaves at
the sitting that produced it. A sitting that ends with six observations in a
note has produced nothing.

## What it does not own

**The destinations.** A fix becomes a pull request, an unresolved defect becomes
an idea or a finding, and a *why is it like this* becomes a decision record.
Those shapes belong to `backlog-ideas`, `audit-records` and `decision-records`
respectively, and this bundle names them without requiring them — where one is
not adopted, the destination is whatever the project already uses, and the
routing rule is unchanged.

**Ending a session.** A sweep spans many, and what to write when one stops
belongs to `session-manager`. What this bundle guarantees is that there is
little to hand over: the index and the sittings are on disk and committed, so a
sweep survives a crash without anybody having prepared for one.

## Consumers

`project` only, for now. The practice is written against a working tree and a
call graph, and while a headquarters could be read the same way, nobody has —
adding `organization` on that basis would be claiming a fit nothing has tested.

## Version

`0.1.0` — **nothing has run a sweep yet.**

It was written straight into this catalog rather than in the project that wanted
it, which is a legitimate route and has a known cost: the conventions here are
reasoned rather than observed, and the parts real use would have sanded down are
still sharp. Stating that is how the cost is managed, so it is stated here
rather than discovered by the first adopter.

**The parts most likely to be wrong**, named now so the first sweep can watch
for them:

- **Three to eight files per sitting** is a guess. It is the range where a
  cluster is coherent and an evening is enough, and both halves of that are
  untested.
- **One pull request per sitting** may be too coarse for a sweep that fixes
  little and too fine for one that fixes a lot.
- **The index as a table in one file** is chosen against this estate's usual
  one-file-per-item instinct, on the grounds that a coverage ledger's whole
  value is being readable at a glance and that a sweep has one writer. If sweeps
  turn out to run with several readers at once, that reasoning fails and the
  shape has to change.
- **Whether `close-a-sweep` earns being a workflow** rather than a paragraph.

**No retention period for archived sweeps**, deliberately. Nobody has run enough
of them to know what one should be, and a number invented now would be enforced
for years on no evidence.
