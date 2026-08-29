---
type: workflow
title: Write an enhancement
description: Turn a behaviour you just watched cost somebody time into a guardrail that fits the budget. Use when a model has just done something worth preventing.
---

# Write an enhancement

## 1. Establish it is the model

**Rule out the cheaper explanations first**, because a guardrail aimed at the
wrong cause loads forever and never fires:

- **the prompt** — was it actually asked for? Ambiguity is not misbehaviour.
- **the harness** — a missing tool, a denied permission, a truncated context.
- **the material** — wrong or absent information in the repository.

**Where it is the harness and the harness is one of several**, it is still an
enhancement with a scoping line. Where it is the prompt, it is not one at all.

## 2. Find the second instance

**One occurrence is an anecdote.** Look back through the session for the same
shape wearing different clothes — the same failure usually recurs within the
hour and is not recognised as the same thing.

**If there is only one, write it in the project's own notes and wait.** A
guardrail for something that happened once is charged to every session forever
on the strength of a single event.

## 3. Check it is not already covered

Read the existing policies in the model's bundle. **The common case is that this
is a sharper instance of one already there** — and sharpening it costs nothing
where adding costs the budget. Widen the existing *Behaviour* and add the new
case to *Never*.

## 4. Write the four parts

**Copy the blocks from [[enhancement]]** — the template carries the frontmatter,
the four parts and the three that get written wrongly. [[what-an-enhancement-is]]
is the reasoning behind it.

Two things it is easy to get wrong:

**State the behaviour without softening it.** *The model sometimes may not
always verify* describes nothing. The document is read by the thing doing it,
and a hedge gives it room.

**Make *Never* specific enough to catch the near-miss.** The failure returns
wearing a synonym, so name the synonyms.

## 5. Check it

**Four things, one paste, under a second.** Each is here because it has already
been got wrong.

```sh
B=catalog/bundles/<model-bundle>

# 1. every guardrail carries all five parts
for f in "$B"/policy/*.md; do
  [ "$(basename "$f")" = entrypoint.md ] && continue
  for part in 'Problem\.' 'Goal\.' 'ALWAYS' 'NEVER'; do
    grep -q "\*\*$part\*\*" "$f" || echo "$f: missing $part"
  done
  grep -qE '\*\*(The near-miss|No near-miss)\.\*\*' "$f" \
    || echo "$f: no near-miss, and no stated reason for its absence"
done

# 2. exactly one document declares matches — the entrypoint
grep -l '^matches:' "$B"/policy/*.md

# 3. the ceiling is declared
grep -i 'Ceiling:' "$B"/BUNDLE.md || echo 'no ceiling declared'

# 4. and met
wc -w "$B"/policy/*.md | tail -1
```

**Check 1** because the near-miss became required after three guardrails were
already written, and nothing reported that they lacked it. It accepts
`**No near-miss.**` too — the rule is that an absence is argued, not that an
example always exists.

**Check 2** because a guardrail that quietly declares its own `matches` breaks
[[the-entrypoint-compels-the-read]] without any symptom — it simply starts
costing more than it should.

**Check 3** because a restructure removed the ceiling from `BUNDLE.md` entirely
and it went unnoticed until somebody looked for it by hand. **A budget nobody
states is a budget nobody exceeds.**

**Check 4 last**, because over the ceiling something comes out — and what comes
out is a decision to record, not an oversight. Where the thing that would come
out is a near-miss, raise the ceiling instead: an example outweighs more
instruction, and a number that forces out the highest-leverage part is
optimising itself.

## 6. Land it, and say what came out

Version per `lumastack/luma-catalog/versioning`: a new policy is a minor bump, a
reworded one is a patch, and **removing one is a minor bump too** — an adopter
loses a rule they may have been relying on.

**The changelog entry names the case.** *"Added after an agent produced three
unverified objections to a proposal in one exchange"* is what lets somebody
later decide the policy has stopped earning its place. *"Improved guardrails"*
does not.
