---
name: implement-plan
description: Execute an approved implementation plan. Use after a plan-feat or quick-plan plan is approved, or when the user hands over a written plan and asks to build it — "implement the plan", "build it", "go ahead", "looks good, do it". Not for planning — if no approved plan exists, use plan-feat or quick-plan.
---

# Implement Plan

## Plan lookup

Read the plan from `docs/plans/` matching the current feature; if ambiguous, ask which one. Otherwise use the most recent plan in the conversation. If none exists, do not invent one — recommend `quick-plan` or `plan-feat`.

Invoke `project-conventions` if it exists.

## Execution strategy

Decide, state the choice and why in one sentence, then proceed without further prompting:

- **Subagents** — the work splits into independent pieces with no shared state (separate modules, parallel migrations, independent test suites). Launch them concurrently in one message; brief each with the plan, its slice, and the files it owns. Run the full test suite once all return.
- **Main stack** — sequential, tightly coupled, few files, or benefits from continuous context. Default for a typical single feature.

## Deviations from the plan

- Minor (naming, file placement, small helpers): proceed and note in the report.
- Material, found by a subagent: stop; report what was found and the proposed change to the orchestrator. Do not ask the user directly.
- Material, in the main session: revise the plan via plan-feat's revision step (surgical edit, show only the change), wait for approval, then continue.

## Verification

Run tests, typecheck, and lint. Check each Done-when item with evidence. Report unmet items as unmet — never claim completion otherwise.

## Report

End with exactly three sections:

1. **What changed** (files)
2. **Done-when status**
3. **Deviations**
