---
type: type_definition
defines: workflow
---

# Workflow

A procedure a person or an agent follows. The body is the instructions; the
frontmatter carries nothing the root type does not already provide.

**It declares no fields of its own**, and that is worth stating rather than
leaving as an absence. A workflow needs a name, a one-line summary of when it
applies, and a body — which is `title`, `description` and the content, all
inherited. There is nothing left for the type to add.

The type still earns its place, because the *name* is what a tool looks for. An
adapter projecting workflows into a harness — Claude Code skills, or whatever
replaces them — finds them by `type: workflow`, not by which directory they sit
in. A path-based scan silently misses a file someone moved, and a capability
that quietly fails to be generated is the worst failure available here:
everything looks fine and the skill simply is not there.

## `description` is load-bearing

For most Documents `description` is a nicety. For a workflow it is the text a
harness uses to decide **when to invoke this at all**, so a workflow without one
projects into a skill that never fires.

The root type declares it `optional` and inheritance is add-only (§10.3), so
this type cannot strengthen it to `recommended`. Treat it as required in
practice: **a workflow without a `description` is broken**, whatever the
contract is able to say.

## Projection is the consumer's job

A workflow says what to do. It does not say where it should be installed, in
what format, or for which harness — those are properties of the tool consuming
it, and baking them in would tie a vendor-neutral document to whichever
assistant happened to be current when it was written.
