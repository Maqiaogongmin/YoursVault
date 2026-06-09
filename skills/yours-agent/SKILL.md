---
name: yours-agent
description: Main entry for all Yours fitness app agent workflows. Use for any task involving Yours Vault, training logs, plan analysis, plan creation, existing plan updates, custom exercises, inbox import files, or CLI/manual validation.
---

# Yours Agent

Use this as the single entry point for Yours App collaboration. Do not ask the user to choose between Vault, plan-author, or CLI skills.

## Core Model

Yours App owns the database. Agents work through reviewable files:

```text
Yours App database -> Yours Vault export -> agent reads plans/logs/exercises
agent writes inbox/*.plan.json and inbox/*.exercise.json -> App imports inbox
```

`plans/`, `logs/`, and `exercises/` are exported reference data. Agent-authored app changes go in `inbox/`.

## Workflow

1. Locate the Yours Vault folder and inspect `manifest.json` when present.
2. Read only the data needed:
   - `plans/*.plan.json` for current plans.
   - `logs/**/*.workout.json` for training history.
   - `exercises/custom-exercises.json` for the exercise library.
3. Classify the task:
   - **Analyze training**: read plans/logs, optionally write Markdown to `reports/` if asked.
   - **Create a new plan**: write `inbox/*.plan.json` with `action: "create"` or omit action.
   - **Update an existing plan**: write `inbox/*.plan.json` with `action: "upsert"` plus `syncId` or `matchName`.
   - **Add missing exercises**: write `inbox/*.exercise.json` before or alongside the plan.
4. Validate:
   - Use the Yours CLI when available.
   - If CLI is unavailable, do manual static checks and say that App inbox import is the final validation step.
5. Report exactly what was prepared and what the user must do next in the Yours App.

## Import Rules

- Prefer `actions[].exercise`; the App also accepts legacy `actions[].name`.
- For existing-plan updates, preserve history: do not claim workout logs changed.
- If a plan references an exercise not in `exercises/custom-exercises.json`, create a matching `.exercise.json` or report the missing action.
- Never write SQLite, Drift files, app containers, or server databases unless the user explicitly asks for low-level repair.
- Never claim import succeeded unless the Yours App or CLI confirmed it.

## References

- Read `references/vault-protocol.md` for folder layout and safety boundaries.
- Read `references/plan-schema.md` before writing `.plan.json` or `.exercise.json`.
- Read `references/cli-validation.md` when the CLI is available or when you need fallback validation rules.
