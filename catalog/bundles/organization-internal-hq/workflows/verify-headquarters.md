---
type: workflow
title: Verify a headquarters
description: Check that an organization's headquarters still exists, is still private, and can still be read by more than one person. Use periodically, and whenever anything about the organization's repositories changes.
---

# Verify a headquarters

**Creating one correctly is not the same as it still being correct.** Visibility
can be changed by anybody with admin rights, access can be revoked when somebody
leaves, and a location recorded in configuration keeps pointing wherever it
pointed.

None of those announce themselves. This is the check that finds them.

**Run it periodically**, and always after a reorganization, an access review, a
repository transfer, or anybody leaving.

## 1. It exists, and it is where you think

```sh
gh repo view <org>/<slug>-hq --json name,url,visibility,isPrivate,isArchived,updatedAt
```

**Not found is ambiguous, and the difference matters.** It may be deleted,
renamed, transferred, or simply invisible to the account you are running as.
**Do not report it as missing** until you have checked whether you can see it at
all — reporting a deletion that did not happen is worse than reporting nothing.

## 2. It is still private

**The check that justifies the whole workflow.**

```sh
gh repo view <org>/<slug>-hq --json visibility,isPrivate --jq '.visibility'
```

**Anything but `PRIVATE` is a finding.** Report it as one — what it is, what is
in it, and that **flipping it back does not unpublish anything.** Forks stay
forked and clones stay cloned.

**Do not silently make it private.** The exposure already happened, whoever
changed it may have had a reason, and quietly reverting it destroys the evidence
of a decision somebody made. Say what happened; let a person choose.

**`INTERNAL` is a judgement call, not a pass.** Visible to everybody in the
enterprise may be exactly right, or may be far wider than intended. Report it and
ask rather than accepting it.

### Check it against what the repository declares

Compare the hosting visibility with `disclosure_level` in `.luma/project.md`.
**The two failures are nothing alike.**

**Actually wider than declared is a showstopper.** A headquarters declaring
`internal` that is publicly readable has already exposed everything in it. Stop,
say what is exposed, and change nothing — the exposure happened, and reverting
quietly destroys the record of whoever made the change.

**Actually narrower than declared is worth a line and no more.** Being wrong
toward restriction is an inconvenience; being wrong toward permission cannot be
undone.

**A missing `disclosure_level` on a headquarters is a finding.** Nothing writes
organization-internal data to a repository that has not said it accepts it, so an
undeclared headquarters is one that silently stopped working — see
[[create-internal-hq]] step 8.

## 3. More than one person can read it

```sh
gh api repos/<org>/<slug>-hq/collaborators --jq '.[].login'
gh repo view <org>/<slug>-hq --json url  # then check team access in settings
```

**One reader is a single point of failure**, and it is the finding this workflow
exists to catch early. An organization's reasoning behind one account is
recoverable right up until it is not.

**Departures are the usual cause.** Access lists are updated when somebody joins
and forgotten when somebody leaves, so the count drifts downward silently.

## 4. It is not stale or archived

`isArchived` is decisive — an archived headquarters is read-only, so the
organization has been recording decisions somewhere else, or not at all.

**Age is a signal, not a fault.** A quiet headquarters may mean a stable
organization or an abandoned practice, and the two look identical from the
outside. **Ask rather than concluding**: has anything been decided lately that
is not in here?

## 5. Everything pointing at it still resolves

Wherever the location is recorded — `.luma/config/` in private repositories,
`~/.config/luma/` elsewhere — check that it still points at what exists.

**A renamed or transferred repository leaves redirects that work until they do
not.** Hosting redirects are a courtesy, not a guarantee, and they break when
the old name is claimed by something else.

## 6. Nothing in it has leaked outward

The reverse direction, and the one nobody checks.

**Has anything from the headquarters been copied into a public repository?** A
standard quoted into a public readme, a decision pasted into a public issue, an
internal service named in a bundle promoted upstream.

**Promotion is the likely path.** A bundle moving from the headquarters to the
universal catalog is exactly the moment an internal name travels with it — see
[[what-a-headquarters-holds]] for the boundary, and check the promoted copy
rather than the original.

## 7. Report, and do not fix in passing

**Say what is true and let somebody decide.** Every finding here — public
visibility, a single reader, a broken pointer, a leaked name — is a change to
somebody's organization, and several of them are records of a decision that was
made.

The one exception is a stale pointer in configuration you own: correcting it
breaks nothing and hides nothing.
