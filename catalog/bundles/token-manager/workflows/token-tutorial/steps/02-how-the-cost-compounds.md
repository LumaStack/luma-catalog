---
type: luma/tutorial_step
title: How the cost actually compounds
step: 2
pause: practice
---

# How the cost actually compounds

The model has no memory. Every time you press enter, the entire conversation
is packed up and sent again from the very beginning.

**So the price of a message is never the message being sent. It is the whole conversation,
paid over and over again.**

Message #1 costs only one message. Message #2 includes the cost of the first + the second.
And message #3 costs one, two and three combined. By message #20 you are paying for all twenty — every
single time you press enter.

A 3,000-token file your agent reads at the beginning of a forty-turn session does not cost 3,000 tokens.
It costs 3,000 tokens 40 times — on top of the compounding every other turn is
adding at the same time.

To keep it simple, always remember that your next message is more expensive than everything that came before it;
no matter how small or simple it is. Turns compound on each other.

Another surprising fact is **What you personally type is a rounding error.** In token optimization studies, everything the
human actually wrote came to about 0.01% of the bill. The rest was the agent re-reading things it had already been sent before.

## Takeaways

- Every turn resends the whole conversation from the beginning of this session.
- **Every new message costs everything that came before it.** Message #20 costs twenty messages, not one.
- Continuing a session costs you exponentially, not linearly.
- What *you* type is a rounding error — around a hundredth of a percent. The spend is re-reading.
