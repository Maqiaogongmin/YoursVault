---
name: yours-vault
description: Work with the Yours fitness app open Vault protocol. Use when Codex needs to create or inspect a Yours Vault folder, generate importable training plan JSON, place files in inbox, analyze exported workout logs, maintain custom exercise files, or help an agent connect to Yours without editing the app database directly.
---

# Yours Vault

## Overview

Yours Vault is the open file interface for the Yours fitness app. Treat the app database as internal state; use Vault files for agent collaboration, imports, exports, reports, and reviewable data exchange.

Read `references/protocol.md` when you need the folder layout, JSON formats, or naming conventions.

## Core Rules

- Write Markdown for people to read.
- Write JSON for Yours to import.
- Put agent-authored imports in `inbox/`; do not modify exported plans or logs in place.
- Validate import files before telling the user they are ready.
- Do not edit SQLite, Drift files, app containers, or server databases unless the user explicitly asks for a low-level repair.
- Do not claim that iCloud sync, app import, or database writes happened unless you actually verified them.

## Workflow

1. Locate the Vault folder from the user's path, app setting, environment variable, or current workspace context.
2. Inspect `manifest.json` when present to confirm this is a Yours Vault.
3. For imports, create files under `inbox/` using the appropriate extension:
   - `.plan.json` for training plans.
   - `.exercise.json` for custom exercises.
4. Run validation through the Yours CLI when available.
5. If validation finds missing exercises, stop and report them, or create separate `.exercise.json` files if the user asks.
6. Tell the user exactly what files were prepared and whether they still need to open Yours to import them.

## Training Plan Imports

When the user asks for a plan that Yours can import:

1. Create a readable Markdown version for the user.
2. Create a matching `.plan.json` file for Yours.
3. Prefer exact exercise names from `exercises/` or CLI exercise search.
4. Put the `.plan.json` file in `inbox/`.
5. Validate the file. If validation cannot be run, say so clearly.

## Training Analysis

When the user asks to analyze training:

1. Read `logs/**/*.workout.json`, `plans/*.plan.json`, and relevant exercise files.
2. Summarize frequency, volume, progression, missed sessions, and likely bottlenecks.
3. Write reports as Markdown in `reports/` only when the user asks for a saved report.
4. Keep coaching claims modest; do not present medical advice.

## Custom Exercises

Use `.exercise.json` files for custom exercise additions or edits. Include `matchName` when renaming an existing exercise. If an exercise is missing from a plan, create exercise files separately instead of embedding undefined metadata inside the plan.

## Safety Checks

Before reporting success, check:

- The target folder path is correct.
- Generated JSON parses successfully.
- Import files are in `inbox/`, not mixed into exported folders.
- Validation ran or the reason it could not run is stated.
- No private local paths, secrets, account names, or unrelated app data were copied into generated files.
