---
type: policy
type_version: "0.0.1"
title: Output patterns
description: What a command prints when it runs — a decision tree for which kind of message this is, the three slots every message fills, and a catalog of the patterns commands reach for.
matches: topic:writing or changing what a command prints — a refusal, a report, an empty result, or a listing
---

# Output patterns

**[[command-line-style-guide]] owns what `--help` prints. This owns what a
command prints when it runs.** The two were one document and should not have
been: help is a template filled in once per command, and output is a decision
made freshly every time something goes wrong.

**Nothing here is one size.** The point of a catalog is that a refusal and an
empty result are different shapes, and reaching for the same block for both is
what produces messages that technically say the right thing and help nobody.

## 1. Which kind of message is this?

**Is this data, or a message about what happened?**

Data is the answer somebody asked for — a listing, a record, JSON. It goes to
**standard output** and takes the shapes in [[command-line-style-guide]]:
*many things, one line each*, or *one thing, in depth*.

Everything else is a message about the run. It goes to **standard error**, so a
caller redirecting output gets the answer with nothing to strip, and continues
down this tree.

**Did the command do what was asked?**

| | | |
| --- | --- | --- |
| **yes** | a **report** | heading is the *end state* |
| **no, and the reader can fix it** | a **refusal** | heading is *what is wrong* |
| **no, and nothing is wrong** | still a **report**, still exit `0` | heading is *what is true* |

That third row is the one decided wrongly. An empty result, an idempotent
re-run, a query matching nothing — none is a failure, and reporting one as a
failure makes every wrapper treat a settled state as a problem.

**For a refusal: can they fix it by changing the invocation, or must they change
the world first?**

Changing the invocation is a usage failure and the remedy is a corrected
command. Changing the world first — verify the outcome, repair the file, close
the tasks — takes a **condition** instead, because the same command run again
fails identically.

## 2. The three slots

```
<heading — what is wrong, or what is now true>
  <detail — the specifics that vary>

<lead-in, ending in a colon>:
  <the command>
```

**A slot with nothing in it is left out, not left empty.** That is where the
flexibility lives: `No record matches X` has no detail block because the heading
already carries the specific.

### The heading

**States the outcome, not the mechanism.** `Initialized backlog`, not
`Wrote configuration file`.

**An end state stays true on a re-run**, which is what lets one shape cover the
first run and the fifth. The detail block carries what happened this time.

**No tool-name prefix.** `tool: message` is right for a one-line diagnostic —
but on a laid-out block it sits on the heading and fights it. A tool prints
one-line diagnostics prefixed and laid-out messages whole.

**Never enumerate what did not happen.** *Creates no directories* reads as
padding; say what it does.

### The detail block

**Indented two spaces. The specifics that vary** — a path, a filter, a list of
candidates, a state per file.

**Where several things each have a state, put the state in a column**, so the
shared part stays in the heading and each row says only what is its own:

```
  created  .luma/config/luma-backlog.yaml
```

**It may nest one level**, where items belong to a summary line above them:

```
  2 of 2 outcomes are not proven
    retries-are-bounded
    the-queue-drains-under-load
```

**It may hold prose instead**, and should when the reason is worth more than the
specifics — see *a required input is missing* below.

### The command

**Introduced by a colon, on the line beneath, indented.**

```
Add one with:
  luma-backlog work-item new "<title>"
```

**Never in backticks.** They are shell syntax: a copied one becomes command
substitution rather than the command. The colon opens it and the line break
closes it, which delimits it without spending a character that can misfire —
and it means a command containing quotes needs no escaping.

**Double quotes cannot delimit it either**, for the same reason: commands
contain them.

**The lead-in says what the command is for.** *Add one*, *Close it with*, *Get
started with*. `Run …` says only that it is a command, which the indentation
already said.

**Placeholders in `<angle|brackets>`; everything else literal.** A reader copies
the line, replaces what is bracketed, and it runs.

**A command may end a line of prose instead** — `Add one with: luma-backlog
list` — where the message is short and the command is the last thing on the
line. Nothing may follow it, because then neither end is marked.

**Omit the whole slot when there is no command to give.** A refusal whose remedy
is a condition closes on prose and offers nothing to run.

## 3. The pattern catalog

Each entry is *when*, the real output, and the one rule people get wrong.

**Every example here is output a real command produced.** An invented example is
worse than none — it stops running the moment a flag is renamed, and nobody
finds out.

---

### Refusal — a required input is missing

**When** — the command is well-formed but cannot proceed until the caller
supplies something.

```
Disposition required
  cancelled work and completed work look identical without one

Close it with:
  luma-backlog work-item close payments-v2 <completed|rejected|canceled|superseded>
```

**The rule that gets missed** — the detail block is worth more as the **reason**
than as the list of valid values. The values belong beside the command somebody
is about to retype. A refusal that only lists what is allowed reads as
bureaucracy; one that says what is lost reads as a reason.

---

### Refusal — the reference names nothing

**When** — a lookup found no record.

```
No work item matches WORK-9999

See what exists with:
  luma-backlog list
```

**The rule that gets missed** — name the kind of thing looked for, and be honest
about it. Where the command accepts several kinds, *record* is correct and
naming one of them sends somebody to the wrong listing.

---

### Refusal — the reference names several

**When** — a lookup matched more than one candidate.

```
Ambiguous reference payments
  backlog/work-items/WORK-0001-payments-v2/index.md
  backlog/work-items/WORK-0002-payments-rollout/index.md

Name one of them, or pass the key.
```

**The rule that gets missed** — this is a **different failure from finding
none**, and collapsing them is how a well-formed query produces a duplicate:
*not found* invites creating the thing, and it already exists twice. Different
message, different exit code ([[exit-codes]]).

---

### Refusal — the verb does not exist

**When** — a mistyped or invented command, flag, or argument count.

```
Unknown command work-tiem
  did you mean work-item

See every command with:
  luma-backlog --help
```

**The rule that gets missed** — **these never reach the application layer.**
The argument parser rejects them first, so whatever it says is what a reader
gets, in its house style rather than yours. That is how a tool with careful
messages everywhere else answers a typo in a stranger's voice. Translate at the
boundary, and take the near-miss from the parser rather than writing a second
distance function that can disagree with the one in the help.

---

### Refusal — a precondition is not met

**When** — the invocation is correct and the world is not ready.

```
WORK-0001-payments-v2 cannot be completed
  2 of 2 outcomes are not proven
    retries-are-bounded
    the-queue-drains-under-load

Verify them, or close with a different disposition. Abandoning one records
why it is unmet and does not clear this — a completed close over an unmet
outcome needs --force, and the count will say so.
```

**The rule that gets missed** — close on a **condition**, never a command.
Offering a corrected invocation is a lie here: nothing about the invocation was
wrong, so the same line fails again. Where an escape hatch exists, name it and
name what it costs.

---

### Refusal — not set up, or the wrong place

**When** — the command needs something that must exist before any of it works.

```
No backlog found
  missing .luma/config/luma-backlog.yaml

Get started with:
  luma-backlog init
```

**The rule that gets missed** — **name the file that was looked for.** A bare
*not set up here* is arguable when a directory of that name is visibly present,
created by a different tool. The specific turns an error somebody disputes into
one they can act on.

---

### Report — something changed

**When** — the command did what was asked and wrote something.

```
Initialized backlog
  created  .luma/config/luma-backlog.yaml

Add a work item with:
  luma-backlog work-item new "<title>"
```

**The rule that gets missed** — the heading is the **end state**, not the verb
that ran. That is what makes the next pattern the same shape rather than a
second layout.

---

### Report — a record changed

**When** — the ordinary write, run many times a day.

```
moved  WORK-0001 · Payments v2
  backlog/work-items/WORK-0001-payments-v2/index.md
  captured → todo (050.0010.000)
```

**Two rules get missed here, and the second survives the first.**

**The verb comes first.** This led with the path, so the single word saying what
happened arrived in column two, after sixty characters the reader already knew.

**Then: name the record, do not print its location.** Even verb-first, the
subject was a path — which buries the identifier in a filename and the title in
a slug, and the identifier is the handle for the *next* command. So the handle
leads and the path drops to detail. A record with no identifier is titled and
nothing else, since the title is the only handle it has:

```
abandoned  The queue drains
  backlog/work-items/WORK-0001-payments-v2/outcomes/the-queue-drains.md
  still counted as unmet — this explains the gap, it does not close it
  1 verdict already recorded, and it stands

No reason recorded. A retrospective asks which of two things happened —
a requirement nobody could state, or one we dropped — and nothing here says.
```

**That second rule is why a shape check is not enough.** `created  <path>`
satisfies every mechanical rule in section 2 — verb column, detail beneath, no
slot half-filled — and still fails the reader, because shape cannot see whether
the right facts are present. See section 5.

---

### Report — nothing to do

**When** — the command ran, the end state holds, and nothing needed doing.

```
Initialized backlog
  exists   .luma/config/luma-backlog.yaml

Add a work item with:
  luma-backlog work-item new "<title>"
```

**The rule that gets missed** — **same heading, same shape, exit `0`.** An
idempotent command that prints a different layout on its second run teaches a
reader that re-running is exceptional, and an idempotent command's whole promise
is that it is not. The status column carries the difference.

---

### Empty result — nothing exists yet

**When** — the query was unnarrowed and the collection is empty.

```
No work items yet

Add one with:
  luma-backlog work-item new "<title>"
```

**The rule that gets missed** — **print something.** Silence is the default a
listing falls into, and it is indistinguishable from a broken command. No detail
block: there are no specifics, and the command is the whole value.

---

### Empty result — the filter matched nothing

**When** — the query was narrowed, matched nothing, and the collection is not
empty.

```
No work items match
  --status closed

See them all with:
  luma-backlog list
```

**The rule that gets missed** — **show the filter, and never use the previous
pattern here.** *Nothing exists* and *your question excluded everything* call for
opposite next moves, and a reader told the first when the second is true goes
off to create something they already have.

---

### Report — succeeded, with something worth saying

**When** — the command did what was asked and noticed something the caller
should hear but is not stopped by.

```
luma-backlog: skipped backlog/work-items/WORK-0001-payments-v2/outcomes/broken.md: no frontmatter: a record starts with ---
KEY                          STATUS      TITLE
retries-are-bounded          unverified  Retries are bounded
the-queue-drains-under-load  unverified  The queue drains under load
```

**The rule that gets missed** — this is the one place the **prefixed one-liner**
is right, because it accompanies output rather than replacing it and may appear
several times. Two rules keep it honest: it goes to standard error so the answer
stays clean, and **it must never fire on a correct state**. A warning that
appears on ordinary runs is one people learn to scroll past, and these have to
survive being ignored for months before they matter once.

---

### Data — many things, one line each

See [[command-line-style-guide]], *`list` — many things, one line each*. Marks
come from [[ascii-styleguide]].

### Data — one thing, in depth

See [[command-line-style-guide]], *`show` — one thing, in depth*.

## 4. What this does not cover yet

Named so the gap is visible rather than quietly filled with a guess:

- **Progress, and long-running work** — including what changes when output is
  not a terminal.
- **Partial success across a batch** — some items succeeded, some failed, and
  the exit code has to mean something.
- **Destructive confirmation.** The style guide already half-answers it —
  *refuse rather than warn*, since a prompt breaks the moment anybody scripts
  the tool — so the pattern may turn out to be *refuse, and name the flag that
  proceeds* rather than a prompt at all. Worth settling from a real case.

**Add a pattern when a real command needs one**, with the output it actually
produced. A catalog is where invented examples breed, and a plausible one is
harder to spot than a wrong one.

## 5. Checking it, rather than remembering it

**Hunting for nonconforming messages by hand does not work.** They get fixed one
at a time as somebody trips over them, and the ones nobody trips over keep
whatever style they were written in — so a tool ends up speaking four dialects,
and no single reader ever sees enough of them at once to notice.

Three things are worth automating, and the first is worth more than the other
two together:

**A battery that exercises every message and checks its shape.** One row per
message a command can produce; the checks run over all of it. What a machine can
see is enough: no backticks, a lead-in has a command under it, the first line of
a block is not indented, a prefixed one-liner does not run on into a block.

**Feed every command a message offers back through the tool.** A worked example
decays silently when a verb is renamed, and this is the half a shape check
cannot reach.

**Check the facts, not only the frame.** A report can be perfectly shaped and
still name the wrong thing — a path where the reader needed the identifier they
are about to type. Anything a house rule requires a message to *contain* is
checkable in the same battery, and is the failure that survives a green shape
check.

**Remove the constructors that build a shapeless refusal.** Where the layer has
a typed way to refuse, deleting the bare `UsageError`-style helpers is worth
more than a rule about not using them: a one-line message is only one call away
for as long as the function exists.

**Two things to know before trusting such a battery**, both of which were true
of the one written alongside this document and neither of which announced
itself:

- **A case nobody exercises is a case nobody checks.** The first battery ran
  every case against a set-up project, so the two refusals a person meets
  *first* — no repository, and no backlog yet — were the two nothing tested.
- **Prove the checks fail.** Each one was mutation-tested by reintroducing the
  exact defect it exists to catch. Two of the three passed the mutation happily
  and had to be rewritten: the shape check because the message was outside its
  battery, and the command check because probing a verb with `--help` exits zero
  for an unknown subcommand — so it was asserting nothing at all.
