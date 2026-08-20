---
type: policy
title: What a headquarters holds
description: What belongs in an organization's private repository, what stays in a project, what goes upstream — and the rule that it stays private.
preload: mandatory
---

# What a headquarters holds

An organization's headquarters is **one private repository holding what is
specific to you**: your standards, your boundaries, what you have already
learned, and what to build next.

It is a repository like any other, so the same `.luma/` tiers apply to it. **The
fractal is deliberate** — an organization has a headquarters, and so does each
project.

## The boundary

| | goes to | because |
| --- | --- | --- |
| a rule for **this repository** | the project's own `.luma/` | nobody else is bound by it |
| a rule for **your projects** | the headquarters | it is yours, and it names your things |
| a rule for **anyone's projects** | the universal catalog | it survives contact with a company sharing none of your history |

**The test for going upstream: would this help an organization that shares
nothing with yours?** Not *is it general* — almost anything can be phrased
generally. Anything naming your customers, your systems, your services or your
people stays here permanently, and generalizing it usually means deleting the
part that made it useful.

## It stays private

**This is the rule the bundle exists to protect**, and it is not a default to be
weighed against convenience. It is in the bundle's name because a name is the
only warning that survives being skimmed.

**Publishing a headquarters is the worst outcome available at this level.** Not
an embarrassment — a handover of trade secrets and institutional knowledge to
anybody who wants them. What an organization worked out over years, why it beat
a competitor, what it learned the expensive way: all of it in one repository,
organized, indexed, and far easier to read than the systems it describes.

**An agent must never publish this repository, or copy from it into anything
public, without a person deciding.** Not to share one useful standard, not
because a link would be convenient, not to make a nice public readme. If
publishing seems right, say so and stop.

A headquarters accumulates exactly what should not be public: which vendors you
depend on, what your internal services are called, which projects are struggling,
what you decided about a competitor, who argued for what. **None of it is a
secret in the sense a scanner would catch** — no credential, no key, nothing a
tool will flag — and that is what makes it dangerous. There is no automated
guard, only this rule.

**Public is not reversible.** Flipping visibility back does not unpublish
anything: forks stay forked, clones stay cloned, caches and mirrors keep what
they took. The same reasoning as a leaked credential, with no rotation available.

**So the check recurs.** Visibility can be changed by anybody with admin rights,
at any time, and nothing announces it — see [[verify-headquarters]]. A rule
checked once at creation is a rule that was true once.

**A public headquarters is a finding, not a preference.** If one exists, say so
plainly, say what is already published, and let somebody decide — do not quietly
make it private and report success, because the exposure already happened and
the record of it matters.

**Some organizations will publish theirs, and a few are right to.** That changes
nothing above. It is a decision made deliberately, once, with the contents
reviewed, by people who own the consequences — not a default anybody drifts
into, and never a call an agent makes on its own.

## Recommended, and genuinely optional

**An organization can work without one.** Small teams, single-project
organizations, and anyone whose standards fit in one repository's `.luma/` are
not missing anything.

What a headquarters buys is **somewhere for a decision that outlives the project
that prompted it.** Without one, cross-project reasoning lives in the project
that happened to raise it — invisible to the other four it governs, and lost
when that project is archived.

**The signal you need one:** the same argument being had twice in two
repositories, or a decision in one project that quietly binds another.

## The location is configuration, not content

**A headquarters does not name itself in public repositories.** A private repo's
URL is not a credential, but it reveals your organization's shape, and a public
project pointing at `github.com/acme/acme-hq` has announced that the repository
exists and what it is for.

So where it lives is recorded as configuration:

- **In a private repository** — `.luma/config/` is fine, since the reader is
  already inside.
- **In a public one** — machine-local, in `~/.config/luma/`, never committed.

**Nothing at runtime should need it.** A check that requires reading the
headquarters has broken the boundary: standards are argued and settled here, and
travel outward as executable checks that run without it.

## One reader is a single point of failure

A headquarters only one person can open holds the organization's reasoning
hostage to that person's access.

**Grant read access deliberately, to more than one human**, and record who has
it. This is the one thing about a headquarters that nobody notices is wrong
until the moment it matters.
