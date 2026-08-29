---
name: implement-plan
description: Execute an approved implementation plan. Use after a plan-feat or quick-plan plan is approved, or when the user hands over a written plan and asks to build it.
---

# Implement Plan

Read the plan from `docs/plans/<slug>.md` if one exists; otherwise use the most recent plan in the conversation.

Decide execution strategy, state the choice and why in one sentence, then proceed without further prompting:

- **Subagents** — the work splits into independent pieces with no shared state (separate modules, parallel migrations, independent test suites). Launch them concurrently in one message.
- **Main stack** — sequential, tightly coupled, few files, or benefits from continuous context. Default for a typical single feature.

Verify against the plan's **Done when** list before reporting completion.
