---
type: concept
title: Knowing without access
description: Why the index records repositories it cannot read, why that is not a security weakness, and why the stance is a default rather than a rule. Read when somebody challenges it.
---

# Knowing without access

**Read this when the index is challenged**, which it will be, and reasonably.

An organization running least privilege or zero trust will have repositories the
indexing account cannot read. **That is the permission model working**, not a
failure to route around. The question is what the index should say about them.

## The stance

**Record that a repository exists even when its contents cannot be read.**

Not the code, not the description, not the boundaries — none of that is
available and none of it should be guessed. Just: *this exists, here is where,
and we cannot see inside it.*

## Why the alternative is worse

**An agent that cannot see a repository will conclude it does not exist.**

That is not a hypothetical failure — it is the default behaviour of anything
reasoning from an index. And what follows from it is concrete:

*"There is no billing service. We should build one."*

So the organization gets **a second billing service**, built by people who could
not read the first, duplicating what already worked and diverging from it
immediately. **Two systems doing one job, one of them written without the
context that would have made it correct**, is a worse outcome than an agent
knowing there is something it may not open — including on security grounds,
because the duplicate was built by whoever happened to lack access.

**Not knowing is not neutral.** An absent entry is read as an answer, and it is
the wrong one.

## Why this is not a security weakness

**The index records existence, not contents.** A name and a location, which
whoever ran the sweep could already see. Nothing is fetched that permissions
denied, nothing is inferred about what is inside, and **no access is granted by
being listed.** An entry is a note that a door exists; it is not a key.

**It lives in the private headquarters**, which is subject to the same rules as
everything else there — see [[what-a-headquarters-holds]].

**And it makes the boundary visible rather than invisible.** A restricted
repository that nothing records is one nobody can ask about; a recorded one is
something a person can request access to, deliberately, through whatever process
exists. **Being able to see that a boundary is there is what lets somebody go
through it properly.**

## The honest caveat

**It does move names to a slightly wider audience.** If the headquarters is
readable by more people than a given repository, listing that repository tells
its readers a name they did not have.

**And in some organizations a name alone is sensitive.** `acme-acquisition-q3`
is a disclosure whatever is inside it. That is a real case, not a corner one.

So the stance above is stated as a default because it is right most of the time
— **not because the objection is wrong.**

## It is a default, and it yields

**A security owner who wants a different answer should get it**, and this bundle
should not argue.

**Per repository** — the entry is removed, and nothing records that it was.
**Wholesale** — an organization may decide restricted repositories are never
indexed, and the index then covers only what the sweeping account can read.

**That is a legitimate configuration, not a degraded one.** The cost is the
duplicate-service failure above, which somebody has now accepted with their eyes
open, and accepting a known cost deliberately is exactly what a security posture
is for.

**Argue the trade-off once, then follow the decision.** A bundle relitigating a
security owner's call every time it runs is a bundle that gets removed.

## The limit nobody should forget

**A sweep cannot discover what it cannot see.**

Restricted repositories do not appear in a listing that lacks permission for
them, so they reach the index another way: a person adds one, a reference in
another repository points at one, or a sweep runs with wider credentials.

Which means **the index is only ever as complete as the account that built it**,
and:

**Never claim completeness.** Not in the generated index, not in a report, not
in a summary to a person. It holds *the repositories we know about*, never *all
the repositories*.

The distinction sounds pedantic and is the whole thing. An index that implies it
is exhaustive re-creates the exact failure this stance exists to prevent — an
agent concluding that what is not listed does not exist.
