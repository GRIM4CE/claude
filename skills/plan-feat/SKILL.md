---
name: plan-feat
description: Plan a feature before implementing it. Use when the user asks to plan, design, or scope a new feature or significant change — "plan this feature", "how should we build", "let's figure out the approach for" — or describes a feature idea and wants a plan before code. Not for bug fixes, one-file changes, or questions that just want an answer.
---

# Plan Feature

Plan with **correctness first, simplicity second**. This skill ends at plan approval; implementation is handled by `plan-implement`.

## Step 0: Project constraints

Check available skills for project conventions:
- Invoke `project-conventions` if it exists.
- Otherwise scan skill descriptions for conventions/standards/architecture/checklist, including nested `.claude/skills/` in monorepos, and invoke at most the two most relevant matches.

Treat their contents as constraints on the plan. If none found, say so under the plan's assumptions.

## Step 1: Develop the approach

Find the closest existing feature and follow its patterns; note the files you expect to touch. Pick **one** approach:
- Correctness first: invalid states hard to represent, edge cases explicit.
- Simplicity second: fewest moving parts; reuse existing patterns over new abstractions.

Present options only when a tradeoff genuinely needs the user's input, and never more than two.

## Step 2: Present the plan

Write the plan to `docs/plans/<feature-slug>.md` and print it inline. Do not publish an artifact and do not load `artifact-design`. Only if the user asks to share: publish the same file as a Markdown artifact (not HTML, without `artifact-design`).

Plan body under 40 lines. Sections, in this order — "What we will do" may use up to 5 bullets; every other section is one line; "Done when" is a markdown checklist:

1. **What we will do** (include files to touch)
2. **Out of scope**
3. **Risks**
4. **What we gain**
5. **Open questions / assumptions**
6. **Rejected alternative**
7. **Done when**

Format reference: `example.md` in this skill's directory.

On feedback: edit the file surgically and re-show only changed sections; never regenerate the whole plan. If published, republish to the same URL.

Wait for approval before any implementation. Handoff: `plan-implement` reads the plan from `docs/plans/<slug>.md`.
