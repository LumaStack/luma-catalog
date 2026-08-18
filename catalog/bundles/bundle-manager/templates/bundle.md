# Bundle manifest template

Copy the block below into `<bundle>/bundle.md` and fill it in. **Copy the block,
not this file** — this file deliberately has no frontmatter of its own, because
a template carrying `type: bundle` would be a second manifest inside this
bundle, and every tool reading it would believe that.

```yaml
---
type: bundle
version: 0.1.0
published: YYYY-MM-DD
consumers: [project]
entry_point: workflows/CHANGE-ME
description: One line — what this holds and who it is for.
---
```

- **`version`** — `0.1.0` for anything used in one place or none. `1.0.0`
  claims the shape has stopped moving.
- **`consumers`** — `project`, `organization`, or both. Both when the same
  content is wanted at either level by different adopters.
- **`entry_point`** — the full Document ID, e.g. `workflows/create-bundle`.
- **`description`** — what a consumer reads when deciding whether to adopt.

## Body

```markdown
# Bundle Name

Why this exists, in a paragraph. What goes wrong without it.

## What is here

- [[the-entry-point]] — the workflow. Start here.
- [[a-policy]] — what this obliges.

## Loading

Which documents are `preload: mandatory`, and why the rest are not. Keep the
mandatory set small — a consumer that cannot load one must fail rather than
proceed.

## Version

Why this number.
```

The *What is here* section links each document with one line on why to open it.
It is not an inventory — the directory already lists the files.
