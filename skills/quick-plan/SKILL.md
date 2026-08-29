---
name: quick-plan
description: Fast, lightweight feature plan (~5 minutes). Use when the user wants a quick or rough plan, a sanity check on an approach, or a sketch before coding — "quick plan", "rough plan", "how would you tackle", "sketch an approach". Not for large or risky features — use plan-feat for those. Not for bug fixes or questions that just want an answer.
---

# Quick Plan

Time-box to ~5 minutes total. Correctness first, simplicity second; pick **one** approach, present no options.

- Skip the convention-skill scan; state any known convention as an assumption.
- Read only the closest existing feature and the files you expect to touch — no broad exploration.
- Present inline as markdown; write no files, publish nothing.

Format, under 15 lines total:

1. **What we will do** (≤3 bullets, include files to touch)
2. **Risks** (one line)
3. **Done when** (≤3-item markdown checklist)

Wait for approval. Handoff: pass the plan inline to `implement-plan` (no `docs/plans/` file).
