---
name: adversarial-review
description: Launch a subagent to adversarially review the current change for correctness and simplicity, then write up the assumptions and design decisions behind the change and why, and publish that write-up as an artifact. Use whenever the user asks for an adversarial review, a review plus design write-up, to "document the decisions and review this", or invokes /adversarial-review — especially right after an implementation or refactor is finished, even if they don't use the word "adversarial".
---

# Adversarial Review + Design Write-up

Two deliverables: an adversarial review of the change by an independent subagent, and a published artifact documenting the assumptions and design decisions behind the change. Do both — the review makes the write-up honest, and the write-up makes the review useful later.

## 1. Identify the change

"The change" is whatever was just worked on: the uncommitted diff (`git diff` / `git diff --staged`), the current branch vs. the default branch, or the edits made earlier in this conversation. If more than one of these plausibly applies and they differ, ask which one before spending subagent tokens on the wrong diff.

## 2. Launch the adversarial reviewer

Spawn one subagent (general-purpose, or fork if the conversation context would help it understand intent) with a prompt along these lines:

> Adversarially review the following change for **correctness** and **simplicity**. Your job is to break it, not to praise it. Read the changed files in full, not just the diff hunks. Hunt for: logic errors, unhandled edge cases (empty inputs, concurrency, error paths), behavior changes callers don't expect, and places where the change is more complex than the problem requires (dead branches, needless abstraction, code that duplicates something that already exists). For each finding, give file:line, a concrete failure scenario or simpler alternative, and your confidence. If something looks wrong, verify against the actual code before reporting it. Return findings ranked by severity; say explicitly if you found nothing significant.

The adversarial framing matters: a reviewer told to "check" a change tends to confirm it. Tell it to assume the change is broken and prove otherwise.

## 3. Write up assumptions and design decisions

While the reviewer runs, draft the write-up from your own knowledge of the change (you made it — recover intent from the conversation and the code, not guesswork). Cover:

- **What the change does** — one short paragraph of context so the write-up stands alone.
- **Assumptions** — what was taken as given (input shapes, invariants, environment, "callers never do X"), and what breaks if each assumption is wrong.
- **Design decisions** — each meaningful choice, the alternative(s) it beat, and *why*. The why is the whole value: "used a map keyed by id because lookups dominate and order doesn't matter" ages well; "used a map" doesn't.
- **Review findings** — the subagent's confirmed findings and what was done about each (fixed, accepted with rationale, or disputed with evidence). Don't launder findings away; an honest "known sharp edge" section is the most useful part of these documents.

Fold real findings back into the code only if the user asked for fixes or the finding is a clear correctness bug in work you were asked to complete; otherwise report them.

## 4. Publish as an artifact

Load the `artifact-design` skill before writing the page (required for any artifact). Author the write-up as an HTML page — a readable engineering document, not a slide deck: title naming the change, prose sections per the structure above, code snippets only where a decision is hard to explain without one. Publish with the Artifact tool and give the user the link.

Finish by telling the user: the review verdict in one or two sentences (what was found, what was done), and the artifact link.
