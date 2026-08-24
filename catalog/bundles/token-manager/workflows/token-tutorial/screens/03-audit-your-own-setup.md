# Start by measuring your own setup

Everything after this screen is a general fix, and general fixes rank differently
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
conversation and be resent on every remaining screen. That is the previous
screen's lesson arriving early, and you may as well collect it now.

**Then run it again in a few weeks, and periodically after that.** Setups drift
in one direction only — you add a server, install a plugin, change a setting, and
six weeks later you are back to wondering why you keep hitting limits. Nothing
announces that it has happened.
