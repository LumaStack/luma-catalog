---
type: luma/tutorial_step
title: Delegate when the session still has a long way to run
step: 9
pause: practice
---

# Delegate when the session still has a long way to run

A subagent reads a pile of files in its own context and hands back a short
summary. In your main window that looks like an enormous win — thousands of
tokens of reading, a few hundred tokens back.

**The win is real, but it is a win about your context rather than about total
spend.** The subagent loaded its own system prompt, its own copy of your memory
file and its own tool definitions before it read anything. Measured end to end it
can easily spend more than it saved.

So the question is not whether it saved tokens in isolation. It is whether the
tokens it kept out of your context would have been resent often enough to pay for
it. Delegate when all of these hold:

- the output is high volume
- you will not need the detail again
- the session has many turns left to run

**The last one is the whole game.** Those avoided tokens would have been resent
on every remaining turn, so the return scales with how much session is left.
Delegate and then immediately end the session and you paid the setup cost for
nothing.
