---
name: github-workflow-review
description: Use when a user wants a disciplined GitHub issue/PR workflow for agent-assisted work: planning in an issue, creating an empty contract-first PR, decomposing large work into sub PRs, running multi-reviewer C/I/M comment rounds, iterating through CI/Codecov-aware readiness, and stopping before merge for maintainer approval.
---

# GitHub Workflow Review

This skill is a WIP skeleton. It defines the intended collaboration protocol for Codex/Claude agents working through GitHub issues and pull requests.

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
6. Run multi-reviewer C/I/M review through GitHub comments.
7. Fix all C/I issues before implementation or readiness.
8. During implementation, run tests with slow-test skips when the repository defines them.
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
- For reviewer prompts, read `references/reviewer-prompt-template.md`.

Load only the template needed for the current task.
