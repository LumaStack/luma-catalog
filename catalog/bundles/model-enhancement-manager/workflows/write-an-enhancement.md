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

[[what-an-enhancement-is]] has the shape. Two things it is easy to get wrong:

**State the behaviour without softening it.** *The model sometimes may not
always verify* describes nothing. The document is read by the thing doing it,
and a hedge gives it room.

**Make *Never* specific enough to catch the near-miss.** The failure returns
wearing a synonym, so name the synonyms.

## 5. Size it

```sh
wc -w catalog/bundles/<model-bundle>/policy/*.md
```

**Against the ceiling in that bundle's `BUNDLE.md`.** Over it, something comes
out — and what comes out is a decision to record, not an oversight.

## 6. Land it, and say what came out

Version per `lumastack/luma-catalog/versioning`: a new policy is a minor bump, a
reworded one is a patch, and **removing one is a minor bump too** — an adopter
loses a rule they may have been relying on.

**The changelog entry names the case.** *"Added after an agent produced three
unverified objections to a proposal in one exchange"* is what lets somebody
later decide the policy has stopped earning its place. *"Improved guardrails"*
does not.
