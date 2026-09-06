---
type: policy
title: Command line style guide
description: The template every command's help follows, explained a piece at a time, plus the output conventions that go with it. Follow it and a new command looks like the rest.
matches: eager
---

# Command line style guide

**Follow this and a new command looks like every other one.** The shape is
`gh`'s, because it is the one most people have already read.

## The template

```
<one line: what this is>

USAGE
  <tool> <command> <subcommand> [args]

<GROUP NAME>
  verb              What it does
  verb <arg>        What it does

FLAGS
  --flag            What it changes

EXAMPLES
  $ <tool> <command> <arg>

NOTES
  <what a reader must know and cannot guess>

EXIT CODES
  0 fine   1 <what refused means here>   2 could not run

LEARN MORE
  <where to go next>
```

**A section with nothing in it is left out, not left empty.** `LEARN MORE`
belongs at the top level and almost nowhere else; a command with no caveats has
no `NOTES`.

The rest of this document is that template, a piece at a time.

## The first line

```
<one line: what this is>
```

**Say what the thing is, not what it does.** No `usage:` prefix and no
repeating the command name — the reader just typed it.

One line. A full stop is optional; a second sentence is not.

For a noun, lead with the verb the noun is about and follow it with the thing
it manages: *Manage bundles — what this project has taken, and what shape it is
in.*

## `USAGE`

```
USAGE
  <tool> <command> <subcommand> [args]
```

**This is the grammar, not an example.** Angle brackets for what the reader
supplies, square brackets for what is optional. Exactly one line — if a command
needs two forms, that is two commands or one flag.

Examples go in `EXAMPLES`, where they can be real.

## The command groups

```
<GROUP NAME>
  verb              What it does
  verb <arg>        What it does
```

**Group them, and order the groups by how often they are reached.** Not
alphabetically: alphabetical order serves looking up a name you already know,
which is the case a menu is least needed for.

**Name a group for what the reader wants**, not for what the code does —
`READING`, `AUTHORING`, `THE GATE`. All caps, no punctuation. Two or three
groups is usually right. A group holding one command is fine when that command
is genuinely a different kind of thing.

**Verbs are bare.** A row under `bundle` says `list`, not `bundle list`; the
heading already said it.

**Arguments go on the verb**, not into the description: `show <name>`, not
`show` described as *show a named thing*.

**Descriptions start with a capital and a verb, and take no full stop** —
*Every bundle this project carries*. Align them all to one column, so the page
has a single left edge for prose.

## `FLAGS`

```
FLAGS
  --flag            What it changes
```

**Only flags this command takes**, including `--help`. Leave out inherited
flags every command has, unless there is nothing else to list.

**Describe what the flag changes, not what it is.** *Work on a repository other
than this one*, not *the project directory*.

Short forms go first where they exist: `-g, --global`.

## `EXAMPLES`

```
EXAMPLES
  $ <tool> <command> <arg>
```

**Real commands, prefixed `$`.** Three to five. Never invent a flag or an
argument to make an example look richer — an example that does not run is worse
than no example.

**Order them the way somebody meets them**, first thing first. For a tool's top
level that is usually the whole first session, in sequence.

## `NOTES`

```
NOTES
  <what a reader must know and cannot guess>
```

This is where the things a reader cannot guess go, and it is also where padding
accumulates. So it takes one test:

**A line stays if a reader can act on it.**

| | |
| --- | --- |
| *This command refuses a vendored copy* | changes what somebody types — keep |
| *`register nothing` marks a bundle landed and not wired* | changes what a value means — keep |
| *This command needs a network* | changes when it can be run — keep |
| *Checks your project against the baseline* | changes nothing — delete |

**Delete a failing line rather than rewording it.** The last row above also
names a concept that does not exist anywhere, which is the worse half: a phrase
that sounds specific and points at nothing costs a reader more than a vague one,
because they go looking.

## `EXIT CODES`

```
EXIT CODES
  0 fine   1 <what refused means here>   2 could not run
```

**Every command states its own**, on one line, because what `1` means is local:
refused, behind, findings present.

**`0` includes doing nothing.** *Nothing to do* is a successful outcome, and
reporting it as a failure makes every wrapper treat a settled state as a
problem.

**Keep `2` for could-not-run.** A tool that refused is working; a tool that
could not try is not, and a caller conflating them cannot tell a healthy tool
from a broken one.

## `LEARN MORE`

```
LEARN MORE
  <where to go next>
```

**Top level only.** Point at `<command> --help` and at the project.

**Never promise a route that does not exist.** If no subcommand answers
`--help`, do not offer `<command> <subcommand> --help`. Help that spends a
reader's trust before they find out is worse than help that says less.

## Beyond the help

The same eye applies to what a command prints when it runs.

**Print only what differs from the default.** A column showing the same value
on every row is wallpaper, and it hides the row where the value matters.

**Where a mark classifies state, make the fallback mean *something is wrong*.**
Name the specific states and let everything else fall to the *not working*
mark. The other way round means the next unanticipated failure prints as
healthy.

**Explain only the marks on the screen.** A legend covering states nothing is
in is one people stop reading.

**Name the fix for the cause, not for the mark.** Where one mark covers several
conditions, give the remedy for *this* one — a remedy that does nothing is
worse than none.

**A refusal names the literal command that resolves it** — the line, ready to
copy, not a description of what to type.

**Refuse rather than warn.** A warning after the act is useless, and one before
it needs a prompt, which breaks the moment anybody scripts the tool.

**Numbers beat markers where the number is the point**, right-aligned so `3`
and `12` line up under each other.

## Naming a command

**The verb names the goal, never the procedure.** `get`, not
`fetch-and-copy-and-write-a-receipt`. The user has a goal; the tool has the
procedure.

**One word means one thing across the whole tool.** Before reusing a word,
check what it already means somewhere else.

**A borrowed word carries its old promise.** `push` means *sent, no review*
everywhere else; `publish` in a self-service registry means *live now*. Borrow
the word only if the promise still holds.

**Required values are operands; optional ones are flags** — a flag reads as
optional however the help describes it. Do not infer an operand because there
happens to be one candidate: refuse, and print the candidates as literal
commands.

## Decoration

**Decoration is for a person.** Box drawing and marks are worth having in front
of a reader and are noise in a pipe, a log, or a screen reader — which
announces every glyph before every row.

**Use characters every monospace font has.** Box drawing and geometric shapes
qualify; anything needing a patched font does not.

**Check the width class before mixing glyph families.** Characters from
different Unicode blocks can render at different widths, and a column that
aligns on one terminal and not another is worse than one that never aligned.
Where the mark that means the right thing has the wrong width class, prefer
meaning.
