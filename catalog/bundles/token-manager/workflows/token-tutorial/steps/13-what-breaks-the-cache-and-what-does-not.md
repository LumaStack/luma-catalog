---
type: luma/tutorial_step
title: Do not treat every change as expensive
step: 13
pause: practice
---

# Do not treat every change as expensive

The opposite mistake is becoming afraid to touch anything. Most of what you do in
a session leaves the cache completely alone, and both lists are worth knowing —
guessing produces paralysis in one direction and surprise bills in the other.

| rebuilds your cache | leaves it alone |
| --- | --- |
| switching model | editing files in your repo |
| changing effort level | editing your memory file |
| turning on fast mode | changing output style |
| connecting or disconnecting an MCP server, where tools load up front | changing permission mode |
| enabling a plugin that ships an MCP server | invoking a skill or a command |
| compacting | recaps and rewinds |
| upgrading Claude Code, then resuming a long session | spawning a subagent |

**The last entry on the left is the nastiest**, because it does not feel like a
change to the session at all. Anthropic's own documentation describes resuming a
long session after an upgrade as about the most expensive request you will send.

And note where a subagent sits. **Spawning one is cache-safe** — which is a
different question from whether it was worth spawning.
