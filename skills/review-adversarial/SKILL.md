---
name: review-adversarial
description: Adversarial review of the current change by a subagent, plus a write-up of assumptions and design decisions. Invoke via /review-adversarial after an implementation or refactor.
disable-model-invocation: true
---

# Adversarial Review + Design Write-up

## 1. Identify the change

The uncommitted diff, the current branch vs. default, or the edits made in this conversation.
If more than one plausibly applies and they differ, ask which before launching the reviewer.

## 2. Launch the adversarial reviewer

Check for a plan file at `docs/plans/<slug>.md` matching the change. Spawn one subagent (general-purpose, or fork if conversation context helps):

> Adversarially review the following change for **correctness** and **simplicity**. Your job is to break it, not to praise it. Report only — do not edit files. Read the changed files in full, not just the diff hunks. Hunt for: logic errors, unhandled edge cases, unexpected behavior changes, and needless complexity (dead branches, needless abstraction, duplication of existing code). For each finding: file:line, a concrete failure scenario or simpler alternative, confidence, and severity (blocker / major / minor). Verify against the actual code before reporting. Say explicitly if you found nothing significant.

If a plan file exists, pass its path to the subagent and append: "Also check the change against the plan's approach and Done-when list."

## 3. Write up assumptions and design decisions

After the review completes:

- If `docs/plans/<slug>.md` exists: read it and record only what changed during implementation — new assumptions, decisions the plan didn't cover, and deviations. Do not repeat the plan's content.
- If no plan exists, cover: what the change does, assumptions (and what breaks if each is wrong), design decisions with the alternatives they beat and why, and review findings.
- Every finding is fixed, accepted with rationale, or disputed with evidence — never dropped.
- Fix clear correctness bugs in the requested work; report everything else.

## 4. Output

- Slug: reuse the plan's filename from `docs/plans/` if one exists, otherwise the current branch name.
- Write the full write-up (including all findings) to `docs/reviews/<slug>.md`.
- Inline, show only the findings: a ranked list with severity, file:line, one-line description, and resolution (fixed / accepted / disputed). Do not print the rest of the file.
- After writing, open the file in the user's editor: run `code <path>` if available, otherwise `open <path>`.
- Do not load artifact-design and do not publish by default. Only if the user asks to share: publish the file as a Markdown artifact (not HTML, no artifact-design) unless HTML is explicitly requested.
- Finish with the verdict in one or two sentences and the file path (or link if published).
