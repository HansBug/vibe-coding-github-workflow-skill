# Readiness Checklist

Use this as the mechanical gate before moving a workflow artifact to the next stage.

## Issue Planning Ready

- [ ] Scope, non-goals, and intended artifacts are explicit.
- [ ] Phase table has `依赖项` and `完成状态` columns.
- [ ] Status uses emoji plus short text, for example `🚧 In progress`.
- [ ] Mermaid graph contains implementation phases only.
- [ ] Reviewer pool discovery is recorded or required before the next step.
- [ ] C/I/M review plan is clear.
- [ ] C/I = 0 for selected planning reviewers.
- [ ] The issue says who may merge, close, or publish.

## Empty PR Contract Ready

- [ ] PR type is marked as umbrella, leaf, or single.
- [ ] Upstream issue / parent PR links are present.
- [ ] Scope and forbidden paths are explicit.
- [ ] Executable validation commands are listed.
- [ ] Reviewer pool discovery table exists.
- [ ] Plan review C/I = 0.
- [ ] For umbrella PRs: sub PR table includes dependencies, conflict surfaces, validation, and emoji status.
- [ ] For leaf PRs: merge-back requirements to the umbrella are written.

## Implementation Ready

- [ ] TDD or characterization plan is executable.
- [ ] Focused tests pass.
- [ ] Repo-specific fast gate passes; slow tests are skipped or run according to repo policy.
- [ ] CI checks pass or failures are classified with evidence.
- [ ] Codecov comment is reviewed when present.
- [ ] Implementation reviewers have posted comments themselves.
- [ ] Implementation review C/I = 0.

## Umbrella Merge-Back Ready

- [ ] Leaf PR has merged to the umbrella branch.
- [ ] Umbrella body status table is updated.
- [ ] Umbrella Mermaid graph node label/class is updated.
- [ ] Umbrella comment records merge commit, files, validation, C/I/M residue, downstream impact, and next step.
- [ ] Newly unlocked or blocked leaf PRs are identified.

## Ready To Merge Handoff

- [ ] Body reflects current head and validation evidence.
- [ ] All required checks are green or explicitly waived by maintainer.
- [ ] Codecov and review comments are included in the final summary.
- [ ] C/I = 0 across selected final reviewers.
- [ ] M issues are either fixed or listed as non-blocking follow-up.
- [ ] The final comment says ready but does not merge without explicit maintainer instruction.
