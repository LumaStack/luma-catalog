---
type: tutorial_step
title: How the cost actually compounds
step: 2
pause: practice
---

# How the cost actually compounds

The model has no memory. Not a short one — none at all. Every time you press
enter, the entire conversation is packed up and sent again from the top.

So your first message costs what you typed. The second costs what you typed,
plus the reply, plus the first message. By message twenty, the thing you just
wrote is a sliver at the top of the request, and everything underneath it is
material you have already paid for, being paid for again.

**The number that matters is never the size of a thing on its own. It is the
size multiplied by the turns left.** A 3,000-token file your agent reads on turn
four of a forty-turn session does not cost 3,000 tokens. It costs 3,000 tokens
thirty-seven more times.

That is the entire mechanism. Every step after this one is a consequence of
it — which is why this is the step worth actually holding on to.

It also explains the most surprising thing in this tutorial. **What you
personally type is a rounding error.** In a real session's logs, everything the
human actually wrote came to about a hundredth of a percent of the bill. The
rest was the agent re-reading things it had already been sent.
