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

**Then the test that catches the commonest mistake: would this help a model that
does not have the problem?** If it would, you are holding a practice rather than
a correction, and it belongs in a model-neutral bundle. *Offer to script a check
you keep re-running* helps a flawless model exactly as much as a flawed one,
which is what marks it as a capability rather than a fix.

**Not** *does another model share it* — earlier versions of the same model
frequently do, and a shared fault is still a fault.

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

**Make *Never* specific enough to catch the contrastive case.** The failure returns
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
done

# 1b. how many carry a contrastive example — reported, never required
printf 'contrastive example in %s of %s guardrails\n' \
  "$(grep -lE '\*\*Contrastive example\.\*\*' "$B"/policy/*.md | wc -l | tr -d ' ')" \
  "$(ls "$B"/policy/*.md | grep -cv entrypoint)"

# 1c. and each one actually contrasts — two quoted fragments, not one plus prose
for f in "$B"/policy/*.md; do
  [ "$(basename "$f")" = entrypoint.md ] && continue
  q=$(sed -n '/\*\*Contrastive example\.\*\*/,$p' "$f" | grep -o '\*"' | wc -l)
  [ "$q" -eq 1 ] && echo "$f: one quoted side only — negative example, not contrastive"
done

# 2. exactly one document declares matches — the entrypoint
grep -l '^matches:' "$B"/policy/*.md

# 3. the ceiling is declared
grep -i 'Ceiling:' "$B"/BUNDLE.md || echo 'no ceiling declared'

# 4. and met
wc -w "$B"/policy/*.md | tail -1

# 5. ALWAYS carries more than NEVER — an inverted guardrail underperforms
for f in "$B"/policy/*.md; do
  [ "$(basename "$f")" = entrypoint.md ] && continue
  awk '/\*\*ALWAYS\*\*/{s=1;next} /\*\*NEVER\*\*/{s=2;next}
       /\*\*Contrastive example\.\*\*/{s=0} s==1{a+=NF} s==2{n+=NF}
       END{if(n>a) printf "%s: NEVER %d > ALWAYS %d — inverted\n", FILENAME, n, a}' "$f"
done
```

**Check 1** because the four parts became the shape after guardrails were
already written, and nothing reported which ones lacked them.

**Check 1c fails**, unlike 1b. Whether to have an example is a judgement;
whether a thing labelled *contrastive* actually contrasts is not. Two of the
four guardrails quoted the wrong version and described the right one in prose —
a negative example wearing the contrastive label, and nothing caught it until a
person read them side by side.

**Check 1b reports and does not fail**, deliberately. A contrastive example is attempted
every time and included only where a real one exists — enforcing its presence
produces fabricated examples, which teach a wrong edge and are worse than the
gap. The count is worth seeing; a failure here would be the mandate surviving
in the tooling after being removed from the policy.

**Check 2** because a guardrail that quietly declares its own `matches` breaks
[[the-entrypoint-compels-the-read]] without any symptom — it simply starts
costing more than it should.

**Check 3** because a restructure removed the ceiling from `BUNDLE.md` entirely
and it went unnoticed until somebody looked for it by hand. **A budget nobody
states is a budget nobody exceeds.**

**Check 5** because the rule that ALWAYS outweighs NEVER was stated and
unenforced, which is the shape this bundle exists to name. **It is written in
`awk` deliberately** — the obvious `sed` range uses `\|` alternation, which
basic regular expressions do not support, so the range never terminates and
every file reports as inverted. That version was written, run, and found wrong
before it was written down.

**Check 4 last**, because over the ceiling something comes out — and what comes
out is a decision to record, not an oversight. Where the thing that would come
out is a contrastive example, raise the ceiling instead: an example outweighs more
instruction, and a number that forces out the highest-leverage part is
optimising itself.

## 5b. Have the model read it back

**Ask the model the guardrail is for to explain it in its own words** — what the
behaviour is, and what it would do differently. It is the only check that tests
comprehension rather than shape, and it costs one exchange.

**It has to be that model, and both ways of getting it wrong are real.** A
different model that explains it correctly gives a **false pass** — you conclude
the guardrail is clear and the model it governs still misreads it, and nothing
downstream will report that. One that explains it badly gives a false failure,
and you rewrite something that was already fine.

**The false pass is the one to fear**, because it is silent. The false failure
costs a rewrite and announces itself.

**A wrong read-back is a finding about the guardrail, not about the model.**
Rewrite it. The model that misexplains it in a clean session is the same one
that will misapply it in a real one.

**This is authoring-time only.** Having a model restate constraints during
ordinary work is per-turn padding and is rejected in
[[what-makes-a-guardrail-stick]] — the objection does not apply to a check run
once, by a person, while writing.

## 6. Land it, and say what came out

Version per `lumastack/luma-catalog/versioning`: a new policy is a minor bump, a
reworded one is a patch, and **removing one is a minor bump too** — an adopter
loses a rule they may have been relying on.

**The changelog entry names the case.** *"Added after an agent produced three
unverified objections to a proposal in one exchange"* is what lets somebody
later decide the policy has stopped earning its place. *"Improved guardrails"*
does not.
