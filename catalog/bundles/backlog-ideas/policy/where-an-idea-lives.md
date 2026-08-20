---
type: policy
title: Where an idea lives
description: Choosing the scope — project, department or organization — and the default that applies when it is unclear.
---

# Where an idea lives

```
.luma/backlog/ideas/<slug>.md        preferred
docs/ideas/<slug>.md                 where luma is not installed
```

**Preferred, not required.** `.luma/backlog/ideas/` is the right home because
the backlog tier is exactly what the practice needs — *what we intend and have
not done* — but **not every repository has luma installed, and an idea still
has to go somewhere.**

What actually matters is **one file per idea, in one consistent place**, with
frontmatter a reader and a tool can both use. None of that depends on the path.

**Never create `.luma/` in a repository that has not adopted it.** Bringing a
directory structure into somebody's project because you wanted to file an idea
is a change they did not ask for. Ask — and if the answer is no, use whatever
the repository already keeps such material in.

**Where luma is absent**, follow what is there rather than inventing: `docs/`
if that is where prose lives, or a sibling of whatever `IDEAS.md` you are
replacing. Consistency within a repository beats consistency across them.

## Choosing the scope

Ask **who would act on this**, not what it is about.

| `scope` | when |
| --- | --- |
| `project` | this repository would do it, and the idea dies if the repository does |
| `department` | several projects under one team would, and no other team cares |
| `organization` | it is about how the organization works, not how anything is built |

**When unclear, ask for guidance or lean towards `project`.** A project-scoped
idea is cheap to promote later; an organization-scoped one nobody owns is the
kind that goes stale in silence. Narrow and promotable beats broad and
orphaned.

## The list of scopes will grow

`project`, `department` and `organization` are a **first guess**, made before
any real backlog met them. Some ideas will fit none of them, and some will fit
badly — belonging to a customer, a product line, a community, a piece of shared
infrastructure that no single project owns.

**When that happens, record it rather than forcing the nearest fit.** An idea
with no good home is evidence about this list, and it is the only evidence there
will be.

**The default is what puts that evidence at risk.** An awkward idea quietly
filed as `project` is indistinguishable from a well-placed one, so leaning on
the default without noting the discomfort is how a missing scope stays missing.
Lean on it, and say when you did.

## The file follows the scope

An idea scoped to the organization belongs in the organization's own repository,
not in whichever repository somebody happened to be working in. An idea captured
in the wrong place is one the people who would act on it never see.

**Do not let the location be decided by where you were standing.** That is the
most common way an idea ends up invisible, and it happens silently. Ideas belong
in the repository that would most naturally act upon them.

If an organization's headquarters is present, ask it — it has the breadth to
see where an idea belongs, which a single repository does not. *Not implemented
yet.*

**Asking is a person or an agent consulting it, never a tool depending on it.**
Foreman must work in a repository belonging to no organization at all, so
nothing in the toolchain may require a headquarters to be reachable. Absent one,
this step is skipped and the guidance above stands on its own.

## One idea or theme per file

Both are fine, and the test is whether they **rise and fall together**. Three
variations on the same underlying change are one file. Three unrelated
improvements that happen to touch the same subsystem are three separate files.

A themed file that starts collecting unrelated entries has become a second
`IDEAS.md` junk drawer, which is what this system exists to replace.

## Naming

`<slug>.md` — kebab-case, from the idea rather than from the area.

`cache-the-dependency-layer.md`, not `build-improvements.md`. The second is a
bucket, and buckets attract everything.
