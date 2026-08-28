---
type: policy
title: Presenting a file
description: How a file is put in front of the reader — the shape, the order it arrives in, and the difference between a deep presentation and a shallow one.
matches:
  - topic: showing a file to somebody during a review
---

# Presenting a file

**One file at a time.** Presenting a cluster at once buys nothing: the reader
can only read one, and the other three scroll away while they do.

*The slice still covers the cluster — the file is the unit of presentation, not
of coverage.*

## The shape

[The presentation template](../templates/file-presentation.md) carries it, for
both modes. In outline: a heading naming the file and its place in the slice, a
data block, a summary of what the file *is*, what you make of it — **then open
it**, and not before. The reader wants to know what they are looking for before
they change windows.

## The data block

**Every row has to earn its place by changing how much attention the file
deserves.** Drop one that does not.

| row | what it tells the reader |
| --- | --- |
| **lines** | how long this will take |
| **commits** | whether it has a history to have drifted from |
| **linked from** | how much rides on it. Nothing inbound may mean nothing depends on it |
| **links out** | whether approving it implies more reading |
| **churn** | recent movement, which is what most sweeps are aimed at |
| **cross-check** | any claim in the file checked against the thing it describes |

**`cross-check` is the row that repays the most.** A documented list against
the code it lists, a count against what it counts, a flag against `--help`. It
is where a stale document announces itself, and it costs one command.

**The block is not fixed.** These six are a starting set, not a contract — a
sweep aimed at something else will want other rows, and finding them out is
part of running one.

## Deep and shallow are different presentations

| | deep | shallow |
| --- | --- | --- |
| the file | **given in full**, or opened for the reader | **summarised** |
| the reader | reads it themselves | reads the summary |
| the agent | says what to attend to | says what is wrong |
| ends with | the file open | a way to open it if they choose |

**Which one applies is declared per area**, alongside the pairing — see
[[who-does-the-reading]]. A sweep may be deep on its prose and shallow on its
code, and the index says which.

## Open it for them

**Run the command; do not print a path and hope.** A path is only clickable in
some terminals, and a reader who has to select and paste has been given a chore
rather than a file.

Ask once what opens files on this machine, then use it every time — and open at
the line under discussion rather than at the top, whenever there is one.

*This is the first thing to check at the start of a sweep and the easiest to
get wrong, because the agent cannot see whether the window opened.*
