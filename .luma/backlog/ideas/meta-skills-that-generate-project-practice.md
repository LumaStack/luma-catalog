---
type: luma/idea
title: Meta-skills that generate a project's own practice rather than copying a template
created: { by: human:benlinton, at: 2026-08-09T00:00:00Z }
contributors: [human:benlinton, agent:claude-opus-5]
horizon: someday
scope: project
lifecycle: draft
---

# Meta-skills that generate a project's own practice rather than copying a template

Skills that generate a project's own best-practice skills, rather than copying a
template.

## Why not now

Abstract, and undesigned. The hard part — what "best practice for *this* project"
would be derived *from* — is not addressed at all.

## Notes

Migrated from `luma-foreman/docs/IDEAS.md`, where it was one line among five
loosely captured capabilities.

Checked at migration time:

- `bundle-manager` authors bundles from a known shape (`create-bundle`,
  `update-bundle`, `repair-bundle`). Nothing reads a project and derives practice
  from it.
- This is not foreman's projection. `luma-foreman/docs/scope.md` covers loading
  and unloading skills, and records that skill *distribution* is solved by the
  `SKILL.md` standard and not worth competing on. Distribution and generation are
  different jobs; only the first is scoped.

**The routing has a live counter-case.** Foreman is what runs inside a project
and can actually read it, which a generator needs. If this turns out to be
`foreman generate` rather than a workflow an agent follows, it belongs there
instead. It is filed here because the original entry says "skills", which is
bundle content — one word in a one-line entry, so not a strong signal.

Related: the verification counterpart is *return periodically to confirm the
latest learnings were applied*, migrated separately.
