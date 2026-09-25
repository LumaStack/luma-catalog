---
type: work-item
type_version: "0.0.2"
key: CATA-0001
title: Pinned tool updates need Renovate or Dependabot, not a hand-rolled job
description: CI clones luma-catalog-curator and luma-foreman at fixed commits, so the checks cannot change under the repository — but nothing notices when either tool moves on, because the hand-rolled pins job was removed rather than repaired. Keeping those pins current is dependency management and there are tools for it. Renovate with a custom manager matching CURATOR_SHA and FOREMAN_SHA is the most direct answer; Dependabot probably cannot see a hex string in an arbitrary YAML file, and that claim was asserted from memory rather than checked.
workflow_status: captured
rank: 010.0010.000
kind: idea
stage: draft
created: { by: human:luma-founder, at: 2026-08-24T23:40:00Z }
---

# Pinned tool updates need Renovate or Dependabot, not a hand-rolled job

CI clones `luma-catalog-curator` and `luma-foreman` at fixed commits, so the
checks cannot change under the repository. The cost is that an upstream fix never
arrives until somebody edits two lines in `.github/workflows/ci.yml`. **Keeping
those pins current is dependency management, and there are tools for it.**

## The problem it addresses

The hand-rolled `pins` job was removed rather than repaired, so **nothing
currently notices when either tool moves on.** That is the gap this idea closes.

What that job got wrong is worth keeping, because a replacement can repeat it:

- **It ran on every push to `main`, not only weekly.** `main` went red on twenty
  consecutive merges, red became the normal state, and the signal stopped meaning
  anything. It went unnoticed for over a day.
- **It compared the pinned SHA against upstream `HEAD`**, so it fired for any
  commit at all. The one time it was acted on, both tools had changed only
  README and vendored docs — no behaviour had moved.
- **It gated nothing.** It failed after the merge, when the decision was already
  made.

A real tool fixes all three: it opens a pull request with the diff attached,
which is reviewable, ignorable, and does not turn the default branch red.

## Renovate probably works and Dependabot probably does not

**Check this first — it decides the whole approach.**

These tools are not declared in any manifest. They are cloned by shell in
`ci.yml` and checked out at a SHA held in an `env:` block. Dependabot updates
declared ecosystems, and as far as is known it has no generic mechanism for
*a hex string in an arbitrary YAML file*. Renovate has custom managers built for
exactly that shape.

So the likely answers are, in order:

1. **Renovate with a custom manager** matching `CURATOR_SHA:` and `FOREMAN_SHA:`.
   Most direct — nothing about the repository has to change.
2. **Repackage each tool as a composite action** and consume it with
   `uses: LumaStack/luma-foreman@<sha>`. Dependabot's `github-actions` ecosystem
   then handles pinning natively. More invasive, and it changes both upstream
   repositories, but it puts the pins in a format everything already understands.
3. **Neither**, and accept that pins are bumped when somebody notices.

**Verify the Dependabot claim before choosing.** It is the load-bearing fact
here and it was asserted from memory rather than checked.

## Notes

Whatever replaces this should be judged against the failure above: **a signal
that fires on noise, or that lands somewhere nobody looks, is not a signal.** A
pull request that sits until reviewed is better than a red run that has to be
noticed on a Monday.

The pins were bumped to current on 24 August 2026 and both tools were verified to
produce identical results, so the repository starts from a known-good state
rather than an unknown one.

## Related work

- Born from the idea it replaces: [`dependency-updates-need-a-real-tool`](../../ideas/dependency-updates-need-a-real-tool.md)
