---
type: type_definition
defines: project
extends: document
fields:
  disclosure_level:
    obligation: recommended
    field_type: enum
    values: [public, internal, confidential, restricted]
    desc: "how widely this repository is disclosed. Absent refuses organization-internal data — undeclared is not permission"
  owns:
    obligation: recommended
    field_type: list of text
    desc: "what this project is responsible for. A claim, which an organization may adjudicate"
  must_not_own:
    obligation: optional
    field_type: list of text
    desc: "what belongs to somebody else. The half that prevents scope creep"
---

# project

**A repository describing itself, to be read by something outside it.**

It lives at `.luma/project.md` — above the four tiers rather than inside one,
because it names the thing the tiers belong to. The filename and the type agree,
as `bundle.md` and `catalog.md` do.

## It answers one question

**When should somebody open this repository?**

That is `description`, and it is the field the whole document exists to carry.
Everything else is optional; a project descriptor that is one good sentence has
done its job.

**It is not a summary of the code.** *"Next.js application"* describes an
implementation and helps nobody decide anything. *"The customer-facing storefront
— anything a buyer sees, checkout, or the payment integration"* is what somebody
needs in order to know this is the repository they want.

**`description` carries unusual weight**, for the same reason it does on a
workflow: a consumer reads it to decide whether to load this at all, before
anything else about the project is fetched. The root declares it `optional` and
inheritance is add-only, so this type cannot strengthen it — **treat it as
required in practice.** A project descriptor without one has no reason to exist.

## `disclosure_level` — how widely this repository is disclosed

**The scale is people, not sensitivity.** `public` is the widest and `restricted`
the narrowest:

| | who sees it |
| --- | --- |
| `public` | anyone |
| `internal` | the whole organization |
| `confidential` | a named group within it |
| `restricted` | a named few |

**Content may only go where disclosure is no wider than its own
classification.** A `public` repository accepts only public content; a
`restricted` one accepts anything. That is the entire rule, and it is one
comparison.

### It is a declaration, not a state

**This is the property the field exists for.** A repository's hosting visibility
is ambient — it is true today and can change tomorrow, and reading it answers a
different question than the one being asked.

`LumaStack/luma-hq` is the worked example. It was private for months while
*planned to be published*, and its `disclosure_level` was `public` throughout —
so it refused organization-internal data the entire time it was still private.
**Checking `isPrivate` would have returned true and permitted the write**, which
is exactly how a repository ends up holding something that becomes public later.

**The declaration was right for months before the world caught up with it**,
which is the whole argument for declaring rather than observing.

**Never derive this from the host.** If it can be inferred from ambient state, it
is not doing the job.

### Absent refuses

**Undeclared is not permission.** A repository with no `disclosure_level` does
not accept organization-internal data, and nothing can be written there on the
strength of it looking safe.

**The tempting mistake is to treat absent as the most restrictive value.** That
reads as *safest*, and the safest value is the one that permits the most — so
the default would grant maximum access to every repository that never said
anything. **Absent means undeclared, and undeclared refuses.** You declare to
gain a capability, never to lose one.

**Scoped, so it does not break ordinary work.** What is refused is a write of
organization-internal data. A repository that has never heard of any of this is
unaffected in every other respect.

### It never causes anything to be published

**This field constrains writes. It is not an instruction about visibility.**

A tool that reads `disclosure_level: public` and makes the repository public has
turned a safety limit into a command — the exact inversion of what it is for.
**Nothing may publish a repository, widen its access, or treat its contents as
publishable on the strength of this field.** Publishing is a decision a person
makes, every time.

The asymmetry is the point: **it may only ever narrow what happens, never widen
it.** A control that can widen access is not a safety control.

### Neither drives the other

The obvious question is which way the coupling runs, and **both obvious answers
are wrong.**

**The value must never drive reality.** A tool that publishes a repository
because a line in a file changed has made a text edit into an irreversible
disclosure. Desired-state reconciliation is fine for resources you can put back;
publication is not one of them. **Nothing changes visibility, access, or
membership on the strength of this field.**

**The value must not be derived from reality either.** That sounds safe and
destroys the property the field exists for. A repository that is private today
and planned for publication would be recorded as `internal` — and would then
accept organization-internal data right up until the day it is published, which
is the failure this was built to prevent. **A field derived from ambient state
is ambient state.**

**So it is an independent assertion, checked against an independently observed
reality, with the gap between them reported.** This is a policy bound, not a
desired state. It says what must be true of the content, and something else
entirely decides what is true of the repository.

### Which edits are cheap and which are consequential

The coupling is asymmetric, in the same direction as everything else here.

**Tightening is cheap and reversible — not free.** Widening the declared
disclosure — `internal` to `public` — narrows what may be written and takes
effect immediately. It can genuinely break something: a workflow that was
writing there now refuses, and somebody is blocked until it is sorted out.

**But everything it breaks is recoverable.** The cost is an interruption
somebody notices within minutes, and loosening it back is available if the
tightening was wrong.

**Loosening is consequential and may not be recoverable at all.** Narrowing the
declared disclosure — `public` to `internal` — **permits content that was
previously refused.** It is the only edit to this field that can cause a leak,
and a leak is not an interruption: it is forked, cloned and cached before
anybody looks.

So it deserves the scrutiny of the change it enables rather than the scrutiny of
a one-line diff. A person decides it, and reality should already support it.

**Reality becoming more permissive invalidates a narrower declaration.** When a
repository is made public, every declaration narrower than `public` is now
false, and the content it admitted is already exposed. That is the error case
above — reported, never auto-corrected in either direction.

### Syncing to reality is not housekeeping

**The most dangerous edit to this field is the one that looks like tidying up.**

A repository declares `public` because it is planned for publication. Somebody
notices it is *currently* private, treats the declaration as a stale value, and
"corrects" it to `internal`. **Organization-private data is now writable into a
repository that is about to be published** — and the change reads, in the diff,
as making a file agree with the world.

**Warn on any edit that loosens this field. Warn harder when the reason given is
that it had fallen out of sync**, because *it did not match reality* is the most
plausible-sounding justification for the most dangerous change available here.

**Matching reality is not a reason.** The declaration is allowed to be stricter
than reality and usually should be. **A divergence is more often a signal that
reality is behind than that the declaration is wrong** — the fix for a
`public` declaration on a private repository is usually to publish it, or to
leave both alone, never to loosen the declaration.

**Require the reason to be about the content, not the metadata.** *Nothing
sensitive will ever live here* is a reason. *It didn't match* is an observation,
and observations do not grant permissions.

### The asymmetry every rule here rests on

**Being wrong toward restriction is an inconvenience. Being wrong toward
permission is unrecoverable.**

Too restrictive means somebody cannot read something they should, notices, and
it is fixed in a minute. Too permissive means data is out — forked, cloned,
cached, indexed — and no correction retrieves it.

**So every rule here fails toward restriction, deliberately.** Absent refuses.
The declaration beats the observation. A check that cannot be performed is a
failure rather than a pass. The field can narrow and never widen. **None of
those are separate decisions; they are one principle applied four times**, and
the cost of each is a mild inconvenience against an outcome nobody can undo.

### When declared and actual disagree

**Never resolve a mismatch silently**, and the two cases are nothing alike.

| declared | actually | | |
| --- | --- | --- | --- |
| `public` | private | more restricted than declared | **report. Not an error** |
| `internal` or narrower | **public** | **more permissive than declared** | **error. Stop** |

**More restricted than declared is the safe direction and often correct.** A
repository planned for publication declares `public` while it is still private,
which is the whole reason this is a declaration — it refuses today, before the
publication that would make a mistake permanent. Say so where a person will see
it; do not treat it as a fault.

**More permissive than declared is a showstopper.** Content the organization
believes is internal is publicly readable *right now*. Somebody changed the
visibility and did not change the declaration, or the declaration was
aspirational.

**Error immediately, say what is exposed, and change nothing.** The exposure has
already happened, quietly flipping the repository private destroys the record of
a decision somebody made, and it does not un-publish anything anyway.

**Hosting visibility can only prove one direction.** `public` and `private` are
coarser than this ladder, so a private repository declaring `restricted` cannot
be checked against the host at all. What *is* checkable is the case that
matters — **actually public, declared anything else** — which is the
unrecoverable one.

A correct `disclosure_level` is necessary and never sufficient. **The destination
must also be established as the intended one**, by identity rather than by
inference — see the `luma/organization-internal-hq` bundle, where the headquarters
is named in machine-local configuration and matched by remote URL.

Two independent checks, both of which must pass. **The field can only ever
refuse.**

## Two more fields, because boundaries are the other thing outsiders need

`owns` and `must_not_own` are what let somebody detect that **two projects are
about to collide**, which is a question no single repository can answer and
every organization eventually asks.

```yaml
owns: [storefront, checkout, payment-integration]
must_not_own: [inventory levels, pricing rules]
```

**`must_not_own` is the more useful half.** Everything owns something; an
explicit *this is not ours* is a boundary somebody argued about, and it is what
stops a project quietly absorbing a neighbour's job over two years.

**They are claims, not rulings.** A project states what it believes it owns; an
organization may disagree, and that disagreement is exactly the finding worth
having. Nothing here is authoritative over an organization's own boundaries.

## Everything else is core, or belongs elsewhere

| | where |
| --- | --- |
| how mature it is | `lifecycle_status` |
| when it was last reviewed | `modified`, `stale_after` |
| what it is called | `title` |
| **where it is hosted** | **nowhere here** — see below |
| how to build or run it | the README, or `docs/` |
| decisions, records, backlog | the `.luma/` tiers |

**It does not record its own URL, visibility, or language.** A repository that
names its own location is wrong the moment it is forked, mirrored, or
transferred, and every one of those facts is already knowable by whoever is
holding it. **A document should not state what its reader already knows.**

## Why the repository owns this and not the organization

An organization can cache a description; it cannot keep one true. The project
changes, the cache does not, and nothing announces the drift.

**Written here, it changes in the same commit as the change that invalidated
it** — reviewed by the people who caused it, in the pull request where they
still remember why. That is the only mechanism that reliably keeps a description
honest, and it is the entire argument for this type.

Whoever collects these is then doing something safe: **combining, not
authoring.**

## The name is not settled

**`project` is a loaded word**, and this is one repository describing itself, so
`repo` is arguably the more honest name. Recorded rather than resolved.

**What keeps `project` for now** is that the catalog already uses it everywhere —
`consumers: [project, organization]`, the per-project `.luma/`, project bundles —
and that a `repo` type would sit beside the `repository` type an organization's
index already declares. **Two types called `repo` and `repository`, meaning
different things, is worse than one loaded word.**

The existing split is at least coherent: **a repository is where it lives; a
project is what it is.** If that stops holding, the rename is cheap while few
bundles declare the type and expensive afterwards.

## What it is not

**Not a README.** A README is a front door for a human deciding whether to keep
reading. This is a machine-read fact for something deciding whether this
repository is relevant at all, and the two are different jobs with different
audiences.

**Not a manifest.** Nothing is built, installed, or resolved from it.

**Not a mandate.** What a project *must* do is policy, and lives in `.luma/`
with the rest of what is in force.
