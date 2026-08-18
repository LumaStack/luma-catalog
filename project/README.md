# Project bundles

Bundles that install into a repository. `luma-foreman` vendors these into a
project's `.hq/standards/bundles/`.

One directory per bundle, named for the bundle without a namespace prefix — the
namespace is added when it is vendored, since only then does it sit alongside
bundles from elsewhere. Each carries a `bundle.md` at its root with a `version`.

A bundle belongs here if applying it changes something inside one repository:
commit conventions, a test layout, a release workflow, a set of type
definitions. If it changes how an organization decides things, it belongs in
[`organization/`](../organization/) instead.

Empty for now.
