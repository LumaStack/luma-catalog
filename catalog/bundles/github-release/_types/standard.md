---
type: type_definition
defines: standard
---

# Standard

A rule a project holds itself to, and the reasoning that makes it worth holding.

**It declares no fields of its own.** A standard needs a name, a one-line
summary of what it governs, and a body — `title`, `description` and the content,
all inherited from the root. There is nothing left for the type to add.

The type earns its place on the name. `type: standard` tells a reader that this
document states an obligation rather than describing something, which is the
difference between *what conventional commits are* and *we use conventional
commits*. It also lets a tool collect a project's standards without guessing
from filenames.

## What separates a standard from a Type Definition

Both state rules, and the line is worth drawing because most bundles will carry
one or the other and putting content in the wrong place makes it unfindable.

A **Type Definition** governs the *shape of a Document* — which fields it
carries and what they hold. Its rules are checkable against a file.

A **standard** governs *conduct* — what a project does, when, and to what
degree. There is often no file to check it against, and where there is, the
check is about the project rather than about any single document.

"A decision record carries a `decided` date" is a Type Definition. "Record a
decision before an irreversible change" is a standard.

## A standard without its reasoning is not finished

The answer is perishable — the constraint that forced it disappears, or the
tooling changes underneath it. The argument is what survives, and it is the only
thing that lets someone disagree on the merits rather than guessing at intent.
