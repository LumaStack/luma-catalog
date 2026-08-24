---
type: tutorial_step
title: Put cheap models where they cannot cost you anything
step: 6
pause: apply_here
---

# Put cheap models where they cannot cost you anything

Choosing your model once, at the start, sounds like it forces the whole session
to run at one tier. It does not.

A good share of what you ask for is small. Rename these files. Write a commit
message. Tidy up this list. The useful heuristic is **the least capable model
that will still finish the job** — and there are places you can apply it without
touching your session's cache at all.

**Subagents.** A subagent's model is set in its own frontmatter, and it runs in
its own context. Point it at a small model and the isolated work gets several
times cheaper while your main session's cache sits untouched.

**Skills and commands.** Same idea. The grunt work runs on the model you
configured for it rather than on whatever your session happens to be using.

That is how to collect the saving without paying the switching cost. Reaching for
`/model` in the middle of a session is how to pay the cost and not collect the
saving.
