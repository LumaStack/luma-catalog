---
type: luma/tutorial_step
title: Start by measuring your own setup
step: 3
pause: apply_elsewhere
---

# Start by measuring your own setup

Everything after this step is a general fix, and general fixes rank differently
on different machines. Someone with a dozen MCP servers connected has a different
top problem from someone with a bloated memory file, and both have a different
one from someone with a scheduled task firing every three hours.

So before changing anything, measure. This bundle carries an audit workflow for
exactly that. It reads your memory files and reports their size, checks whether
tool deferral is genuinely on, lists your MCP servers, finds scheduled tasks
whose interval is longer than your cache lifetime, and parses a real session log
to work out how much of it was re-reading history rather than doing new work.

**It changes nothing.** It reports, sorted by cost, and finishes with the single
highest-leverage change available to you.

**Run it in a second window rather than this one.** It reads a lot of files and
produces a substantial report, and everything it produces would sit in this
conversation and be resent on every remaining step. That is the previous
step's lesson arriving early, and you may as well collect it now.

**Then run it again in a few weeks, and periodically after that.** Setups drift
in one direction only — you add a server, install a plugin, change a setting, and
six weeks later you are back to wondering why you keep hitting limits. Nothing
announces that it has happened.

## Takeaways

- Measure before you change anything: the top problem differs on every machine.
- The audit reads your memory files, MCP servers, deferral status, schedule intervals and cache hit rate.
- It changes nothing — it reports, ranked by cost.
- **Run it in a second window**, or its report rides along on every step left.
- Re-run it every few weeks. Setups drift in one direction only.
