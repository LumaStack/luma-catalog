# Tutorial quiz template

Copy the block below into `workflows/<tutorial>/steps/quiz.md`. **Copy the block,
not this file.**

Four or five questions is usually right. Enough to cover what the tutorial was
for, few enough that the reader is still answering rather than enduring.

````markdown
---
type: luma/tutorial_quiz
title: Quiz
after_step: 20
---

# Quiz

Ask these one at a time, in order. Present each question with its options through
the interactive picker if the harness has one; a numbered list is a fine fallback.

**Never show the answer, or hint at it, before they have chosen.**

**After every answer, say whether they got it right and why.** If they got it
wrong, give the right answer, say why it is right, and say what is wrong with the
one they picked — that last part is where the learning is. Everything you need is
below the question.

A wrong answer is not a failure state. Do not re-ask it, do not keep a running
score out loud, do not make it a big deal. Say what was wrong, why, and move on.

---

## 1. CHANGE-ME — a situation, not a definition

- **A.** A plausible wrong answer somebody would actually pick.
- **B.** The correct one.
- **C.** A wrong answer that is right about something else.
- **D.** The intuition the tutorial exists to break.

**Correct: B.**

Why it is right, in the tutorial's own terms. Two or three sentences, and name
the mechanism rather than restating the option.

- **A** — what would have to be true for this to work, and why it is not.
- **C** — the part that is correct, and the question it is actually answering.
- **D** — the model somebody is carrying if they picked this, said plainly.

---

## 2. CHANGE-ME

…

---

## LAST. The one that ends the tutorial

Make the final question the action the reader should take right now, so answering
it *is* the instruction rather than a hypothetical about it.
````

## Writing the questions

**Situations, not definitions.** *You are thirty turns in and X happens — what
does it cost?* beats *what is X?* A definition tests whether they read; a
situation tests whether they can use it.

**Every wrong option is explained on its own terms.** Not *that is incorrect* —
what that answer would mean if it were true, and where the reasoning goes wrong.
**The wrong answers are the material.** A reader who picked one has just shown
exactly which model they are carrying, and this is the only moment it is cheap to
correct.

**Make the distractors ones somebody would really pick.** An option nobody
chooses teaches nothing and pads the list. The best distractor is the thing the
reader believed before the tutorial started.

**`after_step`** is the last step's number. It is a loading instruction: the quiz
carries its own answers, so nothing may read it before that point.
