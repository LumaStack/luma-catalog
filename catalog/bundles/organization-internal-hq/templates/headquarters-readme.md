# Headquarters readme template

Copy the block to `README.md` in the new repository. **Copy the block, not this
file.**

The readme's job is to stop the two failures a fresh headquarters has: nobody
knows what belongs in it, and somebody eventually makes it public.

## The block

```markdown
# <organization>-hq

<Organization>'s headquarters — where we decide what good looks like, and why.

**This repository is private and stays private.** It names our vendors, our
internal services, our projects and our people. None of that is a secret a
scanner would catch, which is exactly why the rule has to be kept by hand.
Making it public is not reversible: forks stay forked and clones stay cloned.

## What belongs here

- **Boundaries** — what each repository owns, what it must not own, and where
  two are about to collide.
- **Standards** — what a well-formed project looks like here, and why each one
  exists.
- **Learnings** — what has been worked out once and should never be worked out
  again, with the reasoning that settled it.
- **What to build next** — which repository we need, why, and in what order.

## What does not belong here

- **Anything true of only one project.** That goes in that project's `.luma/`.
- **Anything that would help an organization sharing nothing with us.** That
  goes upstream to the universal catalog — and check that our names did not
  travel with it.
- **Credentials.** This being private is not a reason to keep secrets in it.

## Conventions

- **A standard without its reasoning is unfinished.** The answer is perishable;
  the argument is what survives, and it is what lets somebody disagree on the
  merits later instead of guessing at intent.
- **Record a path not taken as deferred, with a re-open trigger** — not as
  rejected. Circumstances change and *rejected* hides why.
- **More than one person can read this.** If that stops being true, fix it
  before it matters.
```

## Fill in

**`<organization>`** — the slug, so the heading matches the repository name.

**The two lists** are the ones worth editing. Ceremony nobody follows is worse
than nothing, so cut what is not true of this organization rather than keeping
it because it reads well.

**Leave the privacy paragraph.** It is the one part a new reader most needs and
the one most likely to be trimmed for brevity.
