# Response length

- Length and formatting rules apply to chat responses only, not to file
  contents (plans, docs, code comments, commit messages).
- Formats and lengths defined by an invoked skill override
  response-length rules.

# Commits

- Conventional format: `type: short description` — types: feat, fix,
  chore, refactor, docs, test, init.
- Imperative mood, lowercase, no period, under 50 characters.
- Do not commit unless asked. No AI attribution or co-author lines.

# Verification

- Before reporting work as done, run the project's typecheck, lint, and
  tests. If any are missing or fail, say so — never claim done otherwise.

# Decisions

- For small, reversible decisions (naming, file placement, minor
  implementation details), assume and note the assumption. Ask before
  anything hard to undo or that changes scope, dependencies, or public
  interfaces.
