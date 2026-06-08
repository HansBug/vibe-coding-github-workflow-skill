# Vibe Coding GitHub Workflow Skill

[中文说明](README_zh.md)

This repository is a work-in-progress home for a skill that standardizes a multi-agent vibe coding workflow over GitHub issues and pull requests.

The intended skill is not about any specific technical domain such as debugging, research corpus maintenance, or package implementation. It focuses on the general collaboration protocol:

- plan work in a GitHub issue before implementation;
- create an empty pull request from the upstream issue or umbrella PR;
- make the PR body executable enough that a developer or agent can follow it with little ambiguity;
- split large work into sub PRs with task tables and dependency diagrams;
- run multi-reviewer C/I/M review rounds through GitHub comments;
- iterate until Critical and Important findings are closed;
- use CI, tests, and Codecov comments as part of the readiness gate;
- stop at ready-to-merge and wait for the human maintainer's explicit merge instruction.

## Current Status

This repository is currently an initial skeleton. The first planning issue will define the actual skill scope, file layout, templates, reviewer prompts, and validation gates. The repository should be treated as WIP until that issue is reviewed and accepted.

## Repository Layout

```text
.
├── README.md
├── README_zh.md
├── CLAUDE.md
├── AGENTS.md -> CLAUDE.md
├── SKILL.md
└── references/
    ├── comment-review-protocol.md
    ├── issue-planning-template.md
    ├── pr-body-template.md
    ├── readiness-checklist.md
    ├── sub-pr-planning.md
    └── reviewer-prompt-template.md
```

`CLAUDE.md` is present because some agent clients auto-discover that filename. The instructions are not Claude-specific; `AGENTS.md` is a symlink to the same content for clients that prefer that convention.

## Planned Skill

The planned skill will help an agentic coding session run a disciplined GitHub workflow:

1. Read upstream issue/PR context with `gh`.
2. Draft or validate an issue plan.
3. Create an empty PR with a contract-first body.
4. Start reviewer agents or external reviewer processes.
5. Require reviewers to post their own GitHub comments.
6. Summarize Critical / Important / Minor findings.
7. Update issue or PR body until C/I findings are resolved.
8. Guide implementation, CI watching, Codecov-aware review, and final ready-to-merge reporting.

## Non-Goals

- This repository does not yet contain a mature production skill.
- This repository does not implement domain-specific debugging or research workflows.
- This repository does not automate merge decisions.
- This repository does not assume GitHub inline reviews are the primary review source; issue and PR comments are first-class.

## License

License is not selected yet. This should be decided before the skill is advertised for reuse.
