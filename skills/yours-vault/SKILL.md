---
name: yours-vault
description: Compatibility/reference skill for the Yours Vault protocol. Prefer `yours-agent` as the main entry for normal Yours tasks; use this only for focused Vault folder protocol details.
---

# Yours Vault

Prefer `yours-agent` for normal Yours tasks. This skill remains as a focused reference for the Vault folder protocol and for older agent setups that already call `yours-vault`.

## Overview

Yours Vault is the open file interface for the Yours fitness app. Treat the app database as internal state; use Vault files for agent collaboration, imports, exports, reports, and reviewable data exchange.

Yours Vault is not the self-hosted sync server. Vault files are meant to be inspected by people; server sync uses protocol v2 events and backup snapshots.

Read `references/protocol.md` when you need the folder layout, JSON formats, or naming conventions.

## Core Rules

- Write Markdown for people to read.
- Write JSON for Yours to import.
- Treat `plans/` and `logs/` as read-only exports. Put every agent-authored change in `inbox/`; do not modify exported plans or logs in place.
- Validate import files before telling the user they are ready. If the Yours CLI is unavailable, perform the manual checks below and say that App import remains the final validation step.
- Do not edit SQLite, Drift files, app containers, or server databases unless the user explicitly asks for a low-level repair.
- Do not claim that iCloud sync, app import, or database writes happened unless you actually verified them.
- Preserve user-created plan names, exercise names, and notes exactly as written.
- Use current Yours product semantics: active/archived plans, manual week completion, and `standard` / `free` record modes.

## Workflow

1. Locate the Vault folder from the user's path, app setting, environment variable, or current workspace context.
2. Inspect `manifest.json` when present to confirm this is a Yours Vault.
3. For imports, create files under `inbox/` using the appropriate extension:
   - `.plan.json` for training plans.
   - `.exercise.json` for custom exercises.
4. Run validation through the Yours CLI when available.
5. If the CLI is unavailable, parse JSON manually, check file extensions, check exercise names against `exercises/custom-exercises.json`, and report that dry-run validation was not run.
6. If validation finds missing exercises, create separate `.exercise.json` files when the user wants the plan to import cleanly.
7. Tell the user exactly what files were prepared and whether they still need to open Yours to import them.

## Training Plan Imports

When the user asks for a plan that Yours can import:

1. Create a readable Markdown version for the user.
2. Create a matching `.plan.json` file for Yours.
3. Prefer exact exercise names from `exercises/` or CLI exercise search.
4. Put the `.plan.json` file in `inbox/`.
5. Validate the file. If validation cannot be run, say so clearly.

For actions that do not naturally use sets, reps, weight, and rest, set `recordMode` to `free` and put duration, distance, pace, sport rules, or coaching details in `note`. Do not invent unsupported fields.

To update an existing plan, write `action: "upsert"` and include either `syncId` or `matchName`. The app should preserve workout history and update only the plan structure.

## Training Analysis

When the user asks to analyze training:

1. Read `logs/**/*.workout.json`, `plans/*.plan.json`, and relevant exercise files.
2. Summarize frequency, standard training volume, free-record activity time, progression, missed sessions, and likely bottlenecks.
3. Write reports as Markdown in `reports/` only when the user asks for a saved report.
4. Keep coaching claims modest; do not present medical advice.

## Custom Exercises

Use `.exercise.json` files for custom exercise additions or edits. Include `matchName` when renaming an existing exercise. If an exercise is missing from a plan, create exercise files separately instead of embedding undefined metadata inside the plan or claiming the plan is ready without the action definition.

## Safety Checks

Before reporting success, check:

- The target folder path is correct.
- Generated JSON parses successfully.
- Import files are in `inbox/`, not mixed into exported folders.
- Validation ran or the reason it could not run is stated.
- Plan actions use names present in `exercises/custom-exercises.json`, or matching `.exercise.json` files exist in `inbox/`.
- No private local paths, secrets, account names, or unrelated app data were copied into generated files.
