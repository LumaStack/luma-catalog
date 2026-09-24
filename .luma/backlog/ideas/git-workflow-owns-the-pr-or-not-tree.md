---
type: luma/idea
type_version: "0.1.0"
title: git-workflow owns the PR-or-not tree
created: { by: human:luma-founder, at: 2026-09-24T18:50:52Z }
contributors: [human:luma-founder, agent:claude-opus-5]
horizon: next
scope: organization
stage: draft
---

# `git-workflow` owns the PR-or-not tree

**This has now been worked out twice from scratch, in separate sessions, and
that is the reason it is written down.** The reasoning is short and it is
reached the same way each time, which means the cost is not the thinking — it is
that neither bundle says what it owns at the boundary, so anyone reading either
one alone has to invent the line again.

## The split

- **`git-secrets`** — prevention, detection, and breach cleanup: rotate, revoke,
  rewrite, request a purge, re-audit, notify.
- **`git-workflow`** — the PR-or-not tree, for every reason a change might not
  take the normal path.

## Why the tree is not a secrets carve-out

**It is "when does a change go through a pull request, and when doesn't it."**
Secrets are one input. A history rewrite for any reason, an emergency revert, a
branch-protection bypass all land on the same tree. That gives it more than one
reason to exist, which is what makes it a real decision tree rather than an
exception clause bolted onto merge mechanics.

## The seam, stated once

**`git-workflow` has to know a secret is present without owning what one is.**
Its branch condition reads *the diff contains material `git-secrets` names*, and
points there for the definition. `git-secrets` answers what counts and how to
clean up; it never answers how the cleanup lands.

That is a one-directional dependency, which is the shape `luma-maintainers`
already covers.

## Why it goes in `git-workflow` rather than `git-secrets`

**Ask who is standing where when the rule needs to fire.**

A deliberate scrub has somebody in `git-secrets`, paying attention. An ordinary
change that happens to contain a secret nobody noticed has somebody about to
open a pull request, with `git-workflow` in play and `git-secrets` unopened.
**The second is the unattended failure**, and it is the one that actually
happens — so the rule belongs where the ordinary path runs.

## The substance the tree has to carry

**A pull request cannot perform a history scrub.** Removing something from
history is a force-push rewrite; a pull request adds a commit on top and leaves
every original object reachable by hash, with `refs/pull/N/head` surviving
branch deletion. So it does not trade safety for convenience — it publishes the
value in a second durable place *and* fails to remove it from the first.

**Framing that as risk invites a judgement call; framing it as futility does
not.** There is no tradeoff to weigh, which is why this branch of the tree is
absolute rather than advisory.

**Name the class, not pull requests.** `refs/pull/N/head` is one mechanism.
The others are notification emails already delivered, forks sharing the object
store, continuous integration logs, commit messages quoting the value, and
review comments. A rule that says "no pull requests" gets obeyed literally, and
then somebody pastes the diff into an issue.

**Scope it to the diff, not the session.** Work during a scrub that does not
contain the secret — adding an ignore pattern, setting commit identity — takes
the normal path. "Never open a pull request while scrubbing" overreaches and
gets worked around, which costs the rule.

**What stays the user's call.** Whether to scrub at all, how far back, what
residual exposure is acceptable, whether to ask the forge to purge. The
mechanism is absolute; the scope never is, and an agent must not decide it.

## What would make it unrepeatable

**Both bundles' scope statements, not a policy file alone.** A bundle's index
line is what decides whether it gets opened, so a correct policy behind a stale
description is a policy nobody reads.

- `git-workflow`'s description becomes the PR-or-not tree for every reason a
  change might not take the normal path — not merge mechanics alone.
- `git-secrets`' says prevention, detection and breach cleanup, and states
  plainly that it does not answer how cleanup lands.

Then the boundary is visible from both ends and the dependency direction is
explicit rather than inferred from absence.

**`git-secrets` also has no remediation procedure today** — it carries
prevention (`configure-identity`, `ignore-secret-files`) and detection
(`audit-sensitive-data`) and nothing for after a breach. A
`scrub-committed-secrets` procedure would live there and delegate the landing
step wholesale to `git-workflow` rather than re-deciding any of it. One handoff
at a clean seam is not a split tree; the same decision answered half in each
place is.

## The branch protection makes unreachable

**Tested on this repository the same day, and it failed.** The no-pull-request
branch was blocked by the forge, not by anybody's judgement:

```
GH006: Protected branch update failed for refs/heads/main.
- Required status check "check" is expected.
```

**Pull requests were never required here — the status check was the only thing
in the way**, and with `enforce_admins: true` the administrator could not push
past it either. So a repository can be configured such that the correct branch
of this tree cannot be taken, and the misconfiguration is invisible until
somebody needs it.

**Which makes `enforce_admins: false` part of what the tree assumes**, alongside
the merge settings `configure-merge-settings` already sets. A repository that
enforces protections against its own administrators has no escape hatch, and the
escape hatch is exactly what a breach needs. Disabling it leaves
`allow_force_pushes: false` and `allow_deletions: false` doing the work they were
actually there for.

**Check it at setup, not at incident time.** Discovering this mid-scrub costs a
settings change on a public repository under pressure, decided by whoever is
awake. That belongs in the procedure that configures a repository, not in the
one that cleans up after it.

## Notes

**Prose will not hold the absolute branch**, and the policy should say so. The
durable form is a check that refuses to open a pull request whose diff matches
the audit patterns. Naming it here is how it gets built rather than
rediscovered.

Related: `catalog-and-project-become-ruleset-bundles` puts `git-workflow` in the
policy/procedure bundle kind, which is the taxonomy this boundary is an instance
of — two adopted-judgment bundles dividing one domain.

Reached the first time in an unrecorded session; reached again on 2026-09-24
while scrubbing private identity out of luma-backlog, where an agent following
standing practice was one step from opening a pull request containing the
removed name.
