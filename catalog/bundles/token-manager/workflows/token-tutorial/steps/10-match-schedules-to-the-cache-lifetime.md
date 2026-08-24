---
type: luma/tutorial_step
title: Check what your scheduled tasks do at three in the morning
step: 10
pause: apply_here
---

# Check what your scheduled tasks do at three in the morning

Everything so far assumed you were at the keyboard. **A scheduled task fires on
its interval whether you are there or not, and every fire sends its full
context** — not a slice of it, all of it. Attached to a bloated session, that is
the entire context paid for on every fire, indefinitely.

Then the cache makes it worse. **Your prompt cache has a lifetime — currently an
hour on subscription plans.** If a task runs less often than the cache lives,
every single fire misses the cache and reprocesses everything at full price
instead of the cache-read rate.

**So the interval is a cost setting rather than just a scheduling one, and it
runs backwards from intuition.** A task firing every 45 minutes can be
substantially cheaper than the same task firing every two hours, because the
frequent one keeps landing on a warm cache.

Go and look at what you have scheduled, and compare each interval against your
cache lifetime. The audit workflow does that comparison for you and flags every
task that loses.

## Takeaways

- A scheduled task sends its **full context on every fire**, whether you're there or not.
- Your prompt cache has a lifetime — currently about an hour on subscription plans.
- **A task firing less often than the cache lives misses it every single time**, at full price.
- So intervals run backwards from intuition: every 45 minutes can be cheaper than every two hours.
- Compare each interval against your cache lifetime. The audit flags the losers.
