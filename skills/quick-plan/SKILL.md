---
name: quick-plan
description: Fast, lightweight feature plan. Use when the user wants a quick or rough plan or a sketch before coding — "quick plan", "rough plan", "sketch an approach". Not for changes involving shared state, cross-cutting concerns, a real tradeoff, or clearly more than ~5 files — use plan-feat for those. Not for bug fixes or questions that just want an answer.
---

# Quick Plan

Correctness first, simplicity second; pick **one** approach, present no options.

- Read the closest existing feature plus the files you expect to touch — ~6 files max, no broad exploration.
- Invoke `project-conventions` if it exists; do not scan for other skills.
- If exploration reveals shared state, cross-cutting changes, a genuine tradeoff, or clearly more than ~5 files to change, stop and recommend `plan-feat`.
- Present inline as markdown; write no files, publish nothing.

Format, under 15 lines total:

1. **What we will do** (≤3 bullets, include files to touch)
2. **Risks / assumptions** (one line)
3. **Done when** (≤3-item markdown checklist)

Wait for approval. Handoff: pass the plan inline to `implement-plan` (no `docs/plans/` file).
