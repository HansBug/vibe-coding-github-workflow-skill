# Reviewer Discovery (WIP)

Use this reference before starting a review round. The reviewer set is environment-dependent and must not be hardcoded.

## Discovery Order

1. Check whether the current agent client exposes native subagent or spawn support. Use it for Codex-style local reviewers when available.
2. If a `$sub-agents`-style skill or plugin is available, list configured agents and use suitable definitions.
3. Probe local CLI executors with `command -v`, for example:

```bash
command -v codex || true
command -v claude || true
command -v codex-deepseek || true
command -v gemini || true
command -v cursor-agent || true
```

4. Prefer each executor's native agent mode when it exists. For example, Codex should use local spawn/subagent support; Claude should use its own agent capability when available.
5. Use model-wrapper commands such as `codex-deepseek` when the user explicitly names them or when the wrapper is detected locally.
6. Record the selected reviewer pool, skipped unavailable executors, time limits, and no-sub-subagent constraint in the issue or PR comment trail.

## Common Invocation Forms

Prefer the current client's native subagent/agent API when available. Use shell CLIs for reviewers that are not exposed through the current client.
Run direct CLI commands from the target repository root unless the CLI command includes an explicit working-directory option.

| Mechanism | Detect | Typical invocation | Notes |
|---|---|---|---|
| Codex native spawn/subagent | Current client exposes a spawn/subagent tool | Use the current session's native spawn/subagent tool, not a shell REPL | Best fit for Codex reviewers inside Codex-capable sessions. The exact trigger is client-provided, such as a spawn-agent tool call or a named local subagent entry. |
| `$sub-agents` skill | `python /path/to/run_subagent.py --list` | `python /path/to/run_subagent.py --agent <name> --prompt "<task>" --cwd "$PWD" --timeout 600000` | Agent definitions live in `$SUB_AGENTS_DIR` or `<cwd>/.agents/`; supported backends are `claude`, `cursor-agent`, `codex`, and `gemini`. Locate the dispatcher from the `$sub-agents` skill body, usually `<skill-dir>/scripts/run_subagent.py`, before copying the command. |
| Codex CLI | `command -v codex` | `codex exec --json --skip-git-repo-check "<task>"` | For yolo reviewer runs, `$sub-agents` maps this to `codex --dangerously-bypass-approvals-and-sandbox exec --json --skip-git-repo-check "<task>"`. Direct yolo form can also use `codex exec --dangerously-bypass-approvals-and-sandbox --json --skip-git-repo-check "<task>"`. |
| Claude CLI print mode | `command -v claude` | `claude -p "<task>"` | For structured headless runs, `$sub-agents` uses `claude --output-format stream-json --verbose -p "<task>"`; yolo mode adds `--dangerously-skip-permissions`. |
| Claude custom agent | `claude --help` shows `--agent` / `--agents` | `claude --agents '{"reviewer":{"description":"Reviews workflow contracts","prompt":"You are a reviewer."}}' --agent reviewer -p "<task>"` | Prefer Claude's own agent capability when available. `claude agents --json --cwd "$PWD"` can inspect background sessions. |
| Gemini CLI | `command -v gemini` | `gemini --skip-trust --output-format stream-json -p "<task>"` | `$sub-agents` uses `--skip-trust` for headless runs in untrusted folders; yolo mode adds `-y`. |
| Cursor Agent CLI | `command -v cursor-agent` | `cursor-agent --output-format json -p "<task>"` | `$sub-agents` forwards `CLI_API_KEY` as `CURSOR_API_KEY`; yolo mode uses `-f --trust`. |
| DeepSeek via Codex wrapper | `command -v codex-deepseek` | `codex-deepseek exec --json --skip-git-repo-check "<task>"` | Use when the user requests this wrapper or it is detected locally. This wrapper may follow Codex CLI flags; yolo form is typically `codex-deepseek exec --dangerously-bypass-approvals-and-sandbox --json --skip-git-repo-check "<task>"`. |

## `$sub-agents` Agent Definition Shape

When using a `$sub-agents`-style dispatcher, define local agents as Markdown files under `<cwd>/.agents/` or `$SUB_AGENTS_DIR`:

```markdown
---
run-agent: claude
permission: yolo
---

# Reviewer

Review the target issue or PR, post your own GitHub comment, and do not use sub-subagents.
```

Valid `run-agent` values in the observed dispatcher are `claude`, `cursor-agent`, `codex`, and `gemini`. Valid permissions are `read-only`, `safe-edit`, and `yolo`. Use `read-only` for contract checks, and use stronger permissions only when implementation-stage validation needs local repro code or tests.

## Copyable Headless Review Snippets

Use these forms for long prompts to avoid shell quoting problems.

### Codex CLI

```bash
codex exec --json --skip-git-repo-check - <<'PROMPT'
You are reviewer A. Read the GitHub issue/PR with gh, post your own review comment, and do not use sub-subagents.
PROMPT
```

### Claude CLI With A Custom Agent

```bash
claude \
  --agents '{"workflow-reviewer":{"description":"Reviews GitHub workflow contracts","prompt":"You are a strict workflow reviewer. Post your own GitHub comment and do not use sub-subagents."}}' \
  --agent workflow-reviewer \
  -p "$(cat <<'PROMPT'
Read the GitHub issue/PR with gh, classify findings as C/I/M, and post your complete review comment yourself.
PROMPT
)"
```

### `$sub-agents` Dispatcher

```bash
# Replace this with the absolute script path from the $sub-agents skill body,
# commonly <skill-dir>/scripts/run_subagent.py.
python /path/to/run_subagent.py \
  --agent reviewer \
  --prompt "$(cat <<'PROMPT'
Read the GitHub issue/PR with gh, classify findings as C/I/M, and post your complete review comment yourself.
PROMPT
)" \
  --cwd "$PWD" \
  --timeout 600000
```

### DeepSeek Through A Codex Wrapper

```bash
codex-deepseek exec --json --skip-git-repo-check - <<'PROMPT'
You are the DeepSeek-backed reviewer. Read the GitHub issue/PR with gh, classify findings as C/I/M, and post your own review comment.
PROMPT
```

## Selection Rules

- Use what is available; do not require Codex, Claude, DeepSeek, or any exact three-reviewer shape.
- Aim for multiple independent reviewers when practical. If only one reviewer mechanism is available, run it and clearly record the reduced pool.
- Reviewer comments must still be posted by the reviewer process itself through `gh issue comment` or `gh pr comment`.
- Treat executor names as current-run evidence only, not as reusable skill requirements.

This file is intentionally a placeholder until FS-C expands reviewer orchestration examples.
