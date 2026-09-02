# Bundles

One directory per bundle, flat. Each carries a `BUNDLE.md` at its root with a
`version` and a `consumers` list.

```yaml
---
type: bundle
version: 1.0.0
consumers: [project, organization]
description: Decisions with their reasoning, deferred alternatives, and re-open triggers.
---
```

`consumers` says who may adopt it — `project` means foreman installs it into a
repository, `organization` means hq installs it into a headquarters, and both
means the adopter chooses. Most bundles name one. The ones that name both are
the point: a decision record or an incident process is genuinely wanted at
either level by different adopters, and that is not the publisher's call to
make.

Directory names are namespaced only when vendored, since only then do they sit
alongside bundles from elsewhere.

## Why this is flat

**A bundle's path is its identity for adoption.** Anything encoded in the path
becomes unchangeable without breaking every pin, manifest entry and adopt
command that refers to it. So the test for whether a fact belongs in a directory
or a field is whether it is **single-valued and permanent**.

Which catalog a bundle sits in passes — a bundle is in exactly one, and moving it
between catalogs *is* promotion, so the path changing is correct.

Sorting bundles by level fails: a bundle can apply to both, and a directory can
only say one. Sorting them by kind fails twice over — an incident-response
bundle is a procedure *and* ships a Type Definition *and* carries templates, and
reclassifying one later would move something whose content never changed.
Nothing reads the kind anyway; a bundle declares where its own contents go, so
category is browsing metadata rather than routing.

If browsing ever gets hard, that is a multi-valued field on the bundle. Never a
directory.
