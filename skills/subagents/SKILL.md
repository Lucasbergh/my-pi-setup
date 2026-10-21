---
name: subagents
description: invoke this skill when the user asks you to use subagents
---

# Subagents

Each subagent is headless, has its own context window, cannot see the parent conversation, cannot ask the user, and cannot spawn subagents or workflows. Give every child a self-contained prompt with paths, constraints, and the expected report.

## Harness

**Harness:** `pi` — the only one. Every subagent is an in-process pi session.

Children inherit the parent's model and thinking level when `model` or `reasoning_effort` is omitted. Every model here is billed per token to an API key (Anthropic Console or OpenRouter). Four children running at once cost roughly four times as much, so pick a cheaper model for simple work.

Never use the `claude-code` provider for subagents, even if it appears in the model list.

| Model                              | Use for                               | Recommended effort |
| ---------------------------------- | ------------------------------------- | ------------------ |
| inherited (default)                | anything                              | inherited          |
| `anthropic/claude-sonnet-5-5`      | most delegated coding/research tasks  | `medium`           |
| `anthropic/claude-haiku-5-5`       | cheap lookups, summaries, bulk scans  | `low`              |
| `anthropic/claude-opus-5-5`        | hard reasoning, large codebases       | `high`             |

OpenRouter chat models (`openrouter/<vendor>/<model>`) are fine for cheap bulk work once `OPENROUTER_API_KEY` is configured. `pi --list-models` shows everything available. Prefer `provider/model-id`; a bare id resolves against the current provider.

**Thinking levels:** `off`, `minimal`, `low`, `medium`, `high`, `xhigh`, `max` — pi thinking levels.

## Spawn and Manage

Call `subagent_spawn` with a complete `prompt`, short `name`, `harness: "pi"`, and optional `working_dir`, `model`, and `reasoning_effort`. At most four subagents run concurrently.

- `subagent_check({ id })`: peek without blocking.
- `subagent_list()`: list all runs.
- `subagent_wait({ ids })`: block only when results are required to proceed.
- `subagent_cancel({ ids })`: stop runs while preserving partial transcripts.
- `/subagents`: inspect or take over a run interactively.

Results return automatically. After spawning, continue useful parent work instead of immediately waiting.
