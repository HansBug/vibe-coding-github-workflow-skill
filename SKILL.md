---
name: vibe-coding-github-workflow
description: Use when a user wants a standardized multi-agent vibe coding workflow over GitHub: planning in an issue, creating an empty contract-first PR, decomposing large work into sub PRs, running multi-reviewer C/I/M comment rounds, iterating through CI/Codecov-aware readiness, and stopping before merge for maintainer approval. Do not use when the task is purely local single-agent work without GitHub issue/PR coordination, or when the need is code generation rather than workflow management.
---

# GitHub Workflow Review

This skill is a WIP skeleton. It defines the intended collaboration protocol for multi-agent vibe coding work coordinated through GitHub issues and pull requests.

## Core Workflow

1. Resolve the upstream issue or PR.
2. Read the upstream body, comments, labels, and linked PRs with `gh`.
3. Create or update a planning issue when the work is not yet ready for implementation.
4. Create an empty PR only after the issue has enough scope and acceptance criteria.
5. Write the PR body as an executable contract:
   - goal;
   - upstream links;
   - allowed scope;
   - non-goals;
   - sub PR split when needed;
   - task table;
   - dependency graph;
   - test and CI plan;
   - readiness gate.
6. Discover the available reviewer pool for the current environment, then run multi-reviewer C/I/M review through GitHub comments.
7. Fix all C/I issues before implementation or readiness.
8. During implementation, follow the target repository's own test and verification conventions.
9. Treat CI and Codecov comments as review inputs.
10. Stop at ready-to-merge and wait for explicit maintainer instruction.

## Comment-First Review

Do not assume GitHub formal review objects contain the real review. In the target workflow, issue and PR comments often carry the authoritative review state.

Prefer:

```bash
gh issue view <number> --repo OWNER/REPO --comments
gh pr view <number> --repo OWNER/REPO --comments
gh api repos/OWNER/REPO/issues/<number>/comments
```

Use formal PR reviews as additional data, not the only data.

## Reference Templates

- For issue planning, read `references/issue-planning-template.md`.
- For PR bodies, read `references/pr-body-template.md`.
- For reviewer discovery and executor selection, read `references/reviewer-discovery.md`.
- For reviewer prompts, read `references/reviewer-prompt-template.md`.
- For comment-first review state, read `references/comment-review-protocol.md`.
- For sub PR split planning, read `references/sub-pr-planning.md`.
- For readiness gates, read `references/readiness-checklist.md`.

Load only the template needed for the current task.
