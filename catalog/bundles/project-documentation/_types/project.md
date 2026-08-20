---
type: type_definition
defines: project
extends: document
fields:
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

## Two fields, because boundaries are the other thing outsiders need

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
