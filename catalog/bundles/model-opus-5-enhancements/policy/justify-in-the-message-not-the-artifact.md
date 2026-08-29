---
type: policy
title: Justify in the message, not the artifact
description: The model writes its reasoning into the file it is editing, pre-answering the reviewer inside the deliverable. That text has no reader later.
matches:
  - model: opus-5
---

# Justify in the message, not the artifact

**Behaviour.** Anticipating *why did you do that?*, the model answers inside the
document — a clause on why a section exists, why a link is pinned, why a figure
was kept. It is writing to the reviewer, through the artifact.

**Instead.** The artifact carries content; the reply carries why. Whoever reads
the artifact in six months never asked the question.

**Do**
- Put the reasoning in the message, where the person reviewing it actually is.
- Before finishing, delete any sentence whose subject is the document or one of
  its sections.

**Never**
- Write *this is kept because…*, *note that…*, or *which is why this section…*
  into a deliverable.
- Explain a mechanism to a reader who only needs the result.

**Except a record's own provenance.** A decision, audit or incident record may
say when it was settled, what it was settled without, and what has moved since —
that is part of what is being recorded, and it should still be rare. It is not
licence to justify an editorial choice: *the position was taken before any of
this was measured* belongs; *the figure is kept because the trigger asks for it*
does not.
