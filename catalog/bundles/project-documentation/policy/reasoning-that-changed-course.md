---
type: policy
title: Reasoning that changed course belongs in history
description: Where history belongs — in git, in records, in backlog journals, in logs, and in whatever else a team already uses. Not a comprehensive list. With examples of what usually goes where, and reasons a document sometimes keeps its history anyway.
---

# Reasoning that changed course belongs in history

**A preference, not a rule.** What follows is where things usually belong and why.
It is not a list to apply exhaustively — documentation keeps producing cases
nobody anticipated, and a rule written today would be wrong in some of them.

**The short version: steer the mess somewhere holding it is the job, and let the
document say what is true now.** Lean that way by default. Depart from it when
there is a reason, and the reason does not have to appear below.

## Where history belongs

**History belongs in git, in records, in backlog journals, in logs, and in
whatever else a team already uses for it.**

**That is not a comprehensive list and should not be read as one.** What the places
on it have in common is that holding the reasoning is their job — so any
destination with that property qualifies, including ones nobody here has thought
of.

Some of them, with what each is good for:

- **git history** — the commit message. [[merge-commits]] in the
  `luma/git-workflow` bundle rests its case against squashing on the commit
  message being where rationale lives, so this is a home that already claims the
  job.
- **pull request bodies and review threads** — the same property, and often the
  more natural place for an argument that involved several people.
- **records** — a decision record keeps deferred alternatives and re-open
  triggers; an audit record keeps a finding and the answer to it.
- **backlog journals** — how an intention changed, kept beside the intention
  itself rather than in the document describing what is now planned.
- **logs** — `log.md` is reserved for this by the `luma/luma-layout` bundle:
  append-only, newest first, and never rewritten once written.
- **wherever a team already keeps this** — an issue tracker, a design archive, a
  wiki. A destination that exists and is used beats a better one that is not.

**They are not equivalent, and one distinction is worth keeping straight.** Git
history and pull requests sit outside the working tree, so they cost a reader
nothing until somebody goes looking. Records and journals are committed and
loadable, so they cost what a document costs. The difference is that in them the
reasoning is not noise: the same paragraph is clutter in a policy document and
content in a decision record, and nothing about the paragraph changed.

## History is not being discarded, it is being concentrated

**Git history has its own job**, and it is a real one: detective work when
something breaks, and learning what a process gets wrong so it can get better.
Both of those need the false starts, the reversals and the arguments that lost.

**That job is done better when the material is in one place.** Somebody
reconstructing how a decision went wrong reads history deliberately, with tools
built for it. The same material sprinkled through a dozen documents serves them
worse *and* costs everybody else on every read.

So this is about **where the mess is useful**, not about throwing it away.

## What usually goes where

Illustrative, not exhaustive.

| | usually |
| --- | --- |
| what was decided, and what is in force | the document |
| what was rejected, and why it stays rejected | the document |
| the back-and-forth before deciding | history — usually the commit or the pull request |
| scratchpad notes and working thoughts | history, or nowhere |
| what an earlier draft said | history |
| that somebody was wrong, and corrected it | history |
| how long it took, and how many attempts | history |

**The pattern underneath, loosely:** content describing *the shape of the answer*
tends to belong in the document; content describing *the shape of the work* tends
to belong in history.

That is a lean, not a boundary. Plenty of things sit on it.

## Reasons a document keeps its history anyway

Several, and there will be others nobody has hit yet:

- **Re-litigation is likely.** A compressed *this was considered and not taken,
  because* saves the next person a week — the version that fits in a paragraph,
  not the argument as it happened.
- **The rule is unreadable without the failure that produced it.** Some constraints
  only make sense once you know what went wrong, and stripping the story leaves
  something nobody can apply.
- **The reader is learning rather than looking something up.** Explanation and
  tutorial material often teaches through the wrong turn.
- **The history is the subject** — a postmortem, a migration guide, a document about
  how something came to be shaped this way.
- **A record type exists whose job is showing the work** — see below.

**When it is genuinely unclear, leaving it out is the cheaper mistake.** Adding a
paragraph back later costs a paragraph. Removing one that has been read for a year
costs everyone who read it.

## Why wasteful context costs more than it looks

**These documents are loaded into agents, in full, repeatedly, against a finite
budget.** A paragraph a person skims in a second is paid for on every read,
forever — and an agent cannot skim. It reads what it is given.

**The second effect is worse than the cost.** Content describing a position nobody
holds any more invites a reader to reason about it as though somebody did. A person
recognises *we used to think X* as background. An agent may take it as a live
constraint, and nothing in the text marks which sentences are still in force.

That gives *every document is a liability until somebody reads it* — from
[[which-document]] — a second and sharper reason.

## What this is not

**Not an argument for terse documents.** Length spent on what is true now earns its
place. A long explanation of a live constraint is fine; a short paragraph about a
dead one is not.

**Not an argument against recording what was rejected.** *We considered X and did
not take it, because Y* is live content — it says what would change the answer.

**A rejected alternative is design. "I previously thought X" is a diary.** That
distinction is worth more than any rule here.

## Some types show their work by design

**Where a record type exists whose job is showing the work, the question does not
arise.** There, reasoning that changed course is the content:

- **decision records** — deferred alternatives, re-open triggers, and the argument
  that was not taken, kept so a decision can be revisited rather than re-litigated
- **audit records** — a finding written by one party and answered by another, where
  the exchange is the point

**This is the easy case, and it is easy because the file decides rather than the
author.** Everywhere else somebody has to think about it, which is why the rest of
this is a preference.

## In practice

**When reasoning changes course mid-edit**, the usual move is that the correction
goes in the commit message and the document simply reads correctly afterwards. A
note explaining the change is usually worth deleting.

**When reviewing**, a sentence that only makes sense to somebody who knows what the
document used to say is the one worth a second look. Sometimes it earns its place.
Often it is a leftover.
