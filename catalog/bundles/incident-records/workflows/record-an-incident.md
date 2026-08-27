---
type: workflow
title: Record an incident
description: Open an incident record while it is happening, pick the kind that decides what it must capture, and close it honestly. Use when something has gone wrong — an outage, a breach, a leaked credential, an agent that violated a policy.
---

# Record an incident

**Open the record first and fill it in as you go.** A record written afterwards
is a reconstruction, and the details that matter — what you believed at the time,
what you tried, when you knew — are the ones memory loses first.

## 1. Open it now, with three fields

`INC-NNNN`, `detected_at`, and one line of what appears to be happening. **That
is enough to start.** Everything else can be wrong and corrected; the number and
the detection time cannot be recovered later.

**`detected_at` is now, not when it started.** You will estimate `began_at` later
from logs, and it will be an estimate — say so when you write it.

## 2. Pick the kind, because it decides what you must capture

| | when |
| --- | --- |
| **`outage`** | something was unavailable or degraded |
| **`security`** | unauthorized access, a leaked credential, a compromised account — **and nothing left** |
| **`data-breach`** | data reached somebody who should not have it. **A clock starts** |
| **`ai-policy-breach`** | a model or agent violated a policy |
| **`other`** | none of these fit. Say so in the body rather than forcing one |

**If you are choosing between `security` and `data-breach`, choose
`data-breach`.** The difference is whether anything was exfiltrated, that is
usually unknown early, and the breach form carries a notification clock the
security form does not. **Downgrading later is cheap; discovering a missed
deadline is not.**

**Copy that kind's template whole**, from `templates/`. One file, complete.

## 3. Record what you believed, not only what was true

**The timeline is the record.** What you saw, what you thought it was, what you
tried, what that ruled out. A timeline showing a wrong hypothesis held for forty
minutes is more useful than one that jumps to the answer — the wrong hypothesis
is the thing worth fixing.

**Correct by appending, never by rewriting.** People read this to reconstruct a
bad day and a silently amended timeline cannot be trusted.

## 4. Set severity by harm that reached the world

Not urgency, not effort. See [[recording-an-incident]] — and put *it could have
been worse* in the body, which is where it is useful, rather than in the field,
where it is a lie.

## 5. Close it, and be exact about what closing means

**`resolved_at` is when it stopped, not when the fix shipped and not when the
write-up finished.** Mitigated and resolved are different; if you mitigated at
14:00 and fixed the cause at 03:00 the next day, say both in the timeline and put
the one that ended the harm in the field.

**Status is derived from `resolved_at` being present.** There is nothing else to
set.

## 6. Anything the incident obliges you to do is not part of this record

**A notification deadline, a rotation, a postmortem, a fix** — those are
obligations the incident created, and they outlive it. Track them where the
project tracks work, and cite `INC-NNNN` from each.

**An incident record that also tries to be a task list stops being a record**:
somebody edits it to tick things off, and the account of what happened drifts.
The exception is the notification clock on a `data-breach`, which is in the
template because missing it is the failure the record exists to prevent.

## 7. Stamp `created_using` and commit

`created_using` is the version **that ran** — the adopted copy you just read
from, not whatever the catalog has published since:

```bash
luma-foreman bundle show incident-records
```

**Only you can answer it**, which is why the template leaves a placeholder — the
catalog cannot know what you adopted, so any value it shipped would be wrong for
somebody. **Nothing rewrites it afterwards** — not even a migration, which
would record itself separately. It is the answer to *why does this record look
like this*, and that answer does not change.

Commit it while the incident is open, and again as it changes. **The commit
history is a second, tamper-evident timeline** — which is worth more than any
field when somebody asks what was known and when.
