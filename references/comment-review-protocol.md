# Comment Review Protocol

Use this reference when extracting review state from a GitHub issue or PR. Ordinary comments are a first-class review ledger.

## Data Sources

Read all of these when available:

- issue or PR body;
- ordinary issue / PR comments;
- formal PR reviews;
- CI status and check logs;
- Codecov or coverage bot comments;
- labels, draft state, merge state, and linked PRs;
- commit history when body claims depend on a specific head.

Do not treat formal PR reviews as the only authoritative review state. In this workflow, reviewer findings, merge-back summaries, and readiness decisions often live in ordinary comments.

## Reviewer Comment Shape

Each reviewer comment should include:

- identity at the top;
- scope and evidence read;
- C/I/M findings;
- reproducible commands or example code for implementation-stage defects;
- ready / not ready conclusion;
- whether Codecov and CI comments were considered.

Use these levels:

| Level | Meaning | Required action |
|---|---|---|
| C / Critical | Breaks correctness, evidence integrity, workflow validity, or merge readiness | Must fix or maintainer must explicitly override |
| I / Important | Likely to cause wrong execution, substantial rework, or misleading artifacts | Must fix before readiness |
| M / Minor | Useful improvement that does not block progress | Fix when cheap; do not churn purely for M |

If any selected reviewer has a live C or I, the issue or PR is `not ready`, even if other reviewers say ready. After fixing, request targeted re-review of the fixed finding.

## Iteration Loop

1. Record reviewer pool discovery and selected executors.
2. Start reviewers with no sub-subagent permission unless explicitly allowed by the task.
3. Wait for each selected reviewer to post its own GitHub comment.
4. Summarize C/I/M into an orchestrator comment.
5. Edit issue body, PR body, or code to address all C/I.
6. Post a fix summary mapping each finding to a revision.
7. Run targeted re-review for each C/I fix.
8. Claim ready only when C/I = 0 and required CI/Codecov gates have been read.

## Codecov As Review Input

When Codecov comments exist, treat them as reviewer evidence:

- modified uncovered lines are at least an I-level concern unless explicitly justified;
- coverage drops should be explained in the PR body or fixed with tests;
- if no Codecov comment exists and the PR is docs-only, record that coverage is not applicable.

## Umbrella Progress Comments

For umbrella PRs, merge-back comments are part of review state. After each leaf merge, the comment must record the leaf PR, merge commit, main files, validation, C/I/M residue, downstream impact, and next step. See `sub-pr-planning.md`.
