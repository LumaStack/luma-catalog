---
type: bundle
version: 0.6.1
published: 2026-08-23
consumers: [project]
entry_point: policy/readme
description: The prose a repository publishes — where it lives, what a README is for, and which documents are worth having at all.
---

# Project documentation

The documentation a repository publishes about itself: the front door, the guide
for a newcomer, the explanation of why it is shaped this way. Not `.luma/`, not
the records, not the changelog — those belong to other bundles and this one says
so out loud.

**Every document is a liability until somebody reads it.** It has to be kept
true, and a stale document is worse than a missing one — missing is honest,
stale is confidently wrong. So the governing question here is never *what should
we have*, it is **what condition have we hit**.

## What is here

- [[readme]] — what a README is for, the four-section default, and what belongs
  somewhere else. Read first.
- [[which-document]] — the documents most projects can have, and the condition
  that earns each one.
- [[documentation-layout]] — prose goes in `docs/`; what stays at the root and
  why.
- [[where-history-belongs]] — history stays in loaded context only where it earns
  its place; where it goes otherwise, and what earning it looks like.
- [[the-project-descriptor]] — the one file written for something *outside* the
  repository to read.
- [[add-document]] — the workflow: is it needed, is it ours, which kind, where.
- [[describe-project]] — write or refresh the descriptor.
- **Type** — [[project]]
- [the README template](templates/readme.md) ·
  [the project descriptor](templates/project.md)

## Two audiences, and one of them never arrives

Everything else here is written for a person who has already opened the
repository. **`.luma/project.md` is written for something that has not**, and is
deciding whether to.

That is the whole reason it is separate from the README rather than derived from
it. A front door assumes somebody is at the door; a descriptor is read *before*,
by something that will stop if the answer is no — so it is one sentence
answering **when should somebody open this?** rather than four sections that
hook a reader.

**The repository owns it, and that is the point.** Anything collecting
descriptions — an organization's index, a search tool, an agent choosing where to
work — could write them instead, and a written-elsewhere description is wrong
from the first commit that changes the project, with nothing announcing the
drift. Written here, it changes **in the same commit as the change that
invalidated it**, reviewed by the people who caused it. That is the only
mechanism where keeping it true is cheaper than not.

## The README default

A strong suggestion, not a rule: **a hook and what it is · why it exists · an
optional example · links to everything else.** Four sections, in that order.

A README is a front door, not a manual. Most people who open one are deciding
whether to keep reading at all — so the limit is the feature, and everything
past those four earns its place individually.

## What this bundle does not own

| | owned by |
| --- | --- |
| `CHANGELOG.md` | the release bundle |
| decision, audit and log records | the record bundles, under `.luma/records/` |
| everything in `.luma/` | the luma-layout bundle |
| `AGENTS.md`, `CLAUDE.md` | nothing — generated projections |

**Named, not depended on.** Nothing here breaks if those bundles are absent; you
simply have no policy about a changelog. A bundle may point at another to mark a
boundary — it may never require one to be present, because bundles have no
dependencies and an unresolved link is legal.

That is the working answer to a problem this catalog is starting to feel: two
bundles caring about the same file, the same directory, or the same convention.
**Acknowledge, do not depend.** See the bundle-manager bundle for the general
stance.

## Consumers

`project` only. An organization's headquarters is a repository too and has a
README, but what an organization publishes about itself is a different question
from what a project publishes about its code.

## Version

`0.6.1` — a wikilink in `where-history-belongs` pointed into the
`luma/git-workflow` bundle and therefore at nothing. Named in prose instead —
the sentence already said which bundle it meant, so nothing was lost.

`0.6.0` — `project` becomes `luma/project`, vendored from the `luma/luma-types`
bundle rather than defined here. Breaking for anything matching on the bare type
name.

**This bundle stopped being the type's owner because more than one tool needs to
agree on it.** foreman reads a project descriptor, so would a curator, so does
the backlog tool — and a contract three tools depend on cannot belong to whichever
bundle happened to need it first. It is vendored here like anywhere else, with
`vendored_from` recording the version taken.

**Namespaced rather than reserved in the format.** `project` is claimed across the
industry; `luma/project` cannot collide with anybody else's. Making it a knowledge-
format built-in was considered and declined — a consumer ignoring it reads the file
correctly as a plain `document`, and the type changes at this organization's rate
rather than the format's.

*Migration:* replace `type: project` with `type: luma/project` in `.luma/project.md`.
Nothing else changes; the fields are identical.

`0.5.0` — [[where-history-belongs]] is new content; existing use is unaffected.

**A preference with examples, deliberately not a rule or a test.** Documentation
keeps producing cases nobody anticipated, and both earlier drafts of this tried to
close the question — first by asking whether something was history, then by asking
whether keeping it prevented re-derivation. Each was a real consideration promoted
into the only one.

**History is concentrated rather than discarded.** Git history has its own job —
detective work when something breaks, and learning what a process gets wrong — and
that job is served better when the material is in one place than when it is
sprinkled through documents, where it also costs every reader on every read.

**The bundle was written entirely for human readers** — the front door, the
newcomer, the stranger with nowhere to report a vulnerability — and never said
that these documents are also loaded into agents, in full, repeatedly, against a
finite budget. That turns noise from a matter of taste into a recurring cost, and
gives *every document is a liability until somebody reads it* a second and sharper
reason.

**It also relocates something rather than forbidding it.** Reasoning that changed
course is worth keeping — it is how a team learns what its process gets wrong. It
belongs in git history, where it costs a reader nothing until they go looking. The
policy sends it somewhere that already claims the job: `luma/git-workflow` rests
its case against squashing on the commit message being where rationale lives.

**The exception is named as a type rather than a circumstance.** Decision records
and audit records exist precisely to show their work. *Show your work where it
matters* is a judgement every author makes generously about their own writing; *a
decision record shows its work, a README does not* is a fact about which file is
open.

`0.4.0` — the declared-versus-actual rules are new content; existing use is
unaffected.

**The governing asymmetry, now stated outright:** being wrong toward restriction
is an inconvenience somebody notices and fixes; being wrong toward permission is
forked, cloned and cached before anybody looks. Absent refusing, the declaration
beating the observation, an unperformable check failing — those are not separate
decisions but one principle applied repeatedly.

**And the field never publishes anything.** A tool reading `public` and widening
access has inverted a safety limit into a command.

`0.3.0` — `disclosure_level` is new content; existing use is unaffected.

**It was added after a real failure rather than in anticipation of one.** An
organization's private index was written into a repository that is published
software, and the guard that should have stopped it checked whether the
destination was *private*. It was. **Privacy was the wrong property**, and the
check passing read as assurance.

`disclosure_level` is the declared answer to the question actually being asked,
and it refuses on a repository that is private today and planned for publication
— the case that defeats every check derived from ambient state.

The README shape and the document matrix are drawn from practice; the conditions
in the matrix have not been tested against a project that had none of these
documents and needed to be talked through acquiring them.

**The descriptor has been written zero times.** Its bet is that a repository
will keep its own one-sentence description true because updating it lands in the
same pull request as the change — which is reasoning, not evidence. **If
descriptors go stale anyway, the argument for the repository owning this
collapses**, and collecting them centrally was right all along.

**The type name is also unsettled.** `project` is a loaded word for what is, in
practice, one repository describing itself. See the type for why it stayed.
