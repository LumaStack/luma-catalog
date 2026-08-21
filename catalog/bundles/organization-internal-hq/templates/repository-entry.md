# Repository entry template

Copy the blocks to `repositories/<name>.md` in the headquarters. **Copy the
blocks, not this file.**

**The whole point is that this is small.** Everything the repository can answer
about itself is fetched, dated and sourced; everything else is a judgement the
organization made. If an entry is getting long, something belongs in the
repository instead.

## Frontmatter — the minimum

```yaml
---
type: repository
title: acme-web
url: https://github.com/acme/acme-web
in_scope: true
description: <when somebody should open this repository>
---
```

**`description` is the field that earns its keep.** It decides whether this
repository is relevant before anything else about it is loaded, so write it as
the answer to *when should somebody open this?* rather than as a summary of
what the code does.

> *"The customer-facing storefront. Open it for anything a buyer sees, checkout,
> or the payment integration."*

not

> *"Next.js application."*

## Frontmatter — with derived values cached

```yaml
---
type: repository
title: acme-web
url: https://github.com/acme/acme-web
in_scope: true
description: The customer-facing storefront — anything a buyer sees, checkout, payments.
sources:
  - { from: "github:acme/acme-web", field: description }
created:  { by: human:fsmith, at: 2026-08-20T09:00:00Z }
modified: { by: process:index-repositories, at: 2026-08-20T09:00:00Z }
stale_after: 2026-11-20
---
```

**`sources` is what makes a refresh safe.** It says which fields were fetched,
so a later run knows what it may overwrite and what somebody wrote by hand.
Without it, no refresh can tell a cached value from a considered one — so it
either destroys judgements or refreshes nothing.

**`stale_after` is a date somebody will actually recheck by.** A date nobody
honours is worse than none, because it makes the entry look supervised.

## Body — only what the organization knows

```markdown
## Why it exists

<One paragraph. The problem it solves, in the organization's terms rather
than the repository's own. This is the part no scan can produce.>

## Boundaries

<What it owns and must not own. Which other repositories it must not
reach into. Only where somebody has actually decided.>

## Relations

<Repositories it depends on, or that depend on it — where that is a
standing fact rather than something a package manifest already says.>
```

**Every heading is optional and an empty one is worse than absent.** A body full
of headings with nothing under them reads as a form somebody abandoned, and
teaches the next person that these entries are paperwork.

## For an out-of-scope repository

```yaml
---
type: repository
title: forked-upstream-thing
url: https://github.com/acme/forked-upstream-thing
in_scope: false
description: A fork of an upstream tool, carried for one patch. Not ours to reason about.
---
```

**Record the exclusion; do not omit the entry.** A repository left out entirely
is rediscovered as new on the next sweep and asked about again, forever. **One
line saying no is what makes the sweep idempotent.**

**Leave `in_scope` absent if nobody has decided.** Undecided and *decided
against* are different states, and only one of them is a question worth finding
later.

## For a repository you cannot read

```yaml
---
type: repository
title: acme-billing
url: https://github.com/acme/acme-billing
in_scope: true
access: restricted
---
```

**No `description`, and do not guess one** — not from the name, not from what it
probably does. `access: restricted` says the gap is a **boundary rather than an
omission**, which is what stops somebody helpfully offering to fill it.

**In scope and unreadable is a normal state**, not a contradiction. The
organization reasons about this repository; this account cannot open it.

**The entry buys one thing: nothing concludes the repository does not exist.** An
agent that cannot see a billing service and finds no entry proposes building
one. See [[knowing-without-access]] — including why a security owner may
legitimately tell you not to record these at all.
