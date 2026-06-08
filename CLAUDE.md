# Repository Instructions

This repository is a WIP skill repository for a Codex/Claude-compatible GitHub issue and pull request workflow.

## Operating Rules

- Use `main` as the only initialized branch unless a human maintainer explicitly asks for another branch.
- Prefer GitHub CLI (`gh`) for issue and PR operations.
- Treat issue and PR comments as first-class review data. Do not rely only on GitHub formal review objects.
- When reviewing, classify findings as:
  - `C / Critical`: blocks correctness, workflow validity, evidence integrity, or merge readiness.
  - `I / Important`: likely to cause wrong execution, substantial rework, or misleading artifacts.
  - `M / Minor`: useful improvement that does not block progress.
- C/I findings must be fixed or explicitly rejected by the maintainer before readiness is claimed.
- M findings should be fixed when cheap, but must not cause unnecessary churn.
- Do not merge pull requests without explicit human maintainer instruction.

## Reviewer Protocol

When asked to review an issue or PR:

1. Read the issue or PR body.
2. Read comments and timeline-relevant updates.
3. Check whether the plan is executable and has a clear exit gate.
4. Post a GitHub comment yourself when instructed to do so.
5. Include identity, scope, C/I/M findings, evidence, and conclusion.

## Skill Scope

This repository should stay focused on the general GitHub collaboration workflow:

- issue planning;
- empty PR contract;
- sub PR decomposition;
- task tables and dependency diagrams;
- multi-reviewer comment rounds;
- C/I/M iteration;
- CI, test, and Codecov readiness;
- ready-to-merge handoff.

Avoid embedding domain-specific debugging, research corpus, or product implementation rules in the core skill. Domain-specific guidance can be referenced as examples only.
