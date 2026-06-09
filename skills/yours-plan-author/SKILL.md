---
name: yours-plan-author
description: Create training plans for the Yours fitness app. Use when Codex needs to turn a user's goals, schedule, equipment, or natural-language program into both a readable Markdown plan and a machine-readable `.plan.json` file for Yours Vault inbox import.
---

# Yours Plan Author

## Overview

Create two deliverables for every Yours training plan: a Markdown version for the user and a `.plan.json` version for the app. Use Yours Vault for delivery and Yours CLI for validation when available. The CLI is optional; the app inbox importer is the final authority.

Yours supports both strength-style standard records and activity-style free records. Use both when a plan mixes lifting, cardio, sports, stretching, or mobility.

Read `references/plan-schema.md` when you need exact JSON examples.

## Intake

Before writing a plan, use the user's available context. Ask only when the missing information changes safety or usefulness:

- Goal: strength, hypertrophy, fat loss, general fitness, return to training.
- Schedule: days per week and session length.
- Equipment: gym, home, bodyweight, machines, free weights.
- Experience and constraints: beginner/intermediate, injuries, movements to avoid.
- Progression preference: fixed progression, RPE/RIR, double progression, simple linear progression.

If context is missing and the user wants speed, make conservative assumptions and state them in the Markdown plan.

## Deliverables

Produce:

1. `YYYY-MM-DD-plan-slug.md`: readable plan with schedule, exercise list, progression, and notes.
2. `YYYY-MM-DD-plan-slug.plan.json`: importable Yours plan data.

When working inside a Yours Vault, put the `.plan.json` file in `inbox/`. Put the Markdown file beside it only if the user wants the plan saved there; otherwise return the Markdown in the response or save to the requested location.

## JSON Rules

- Use `format: "yours-plan"` and `formatVersion: 1`.
- Prefer `actions[].exercise` for exercise names. The app also accepts legacy `actions[].name`.
- Use stable exercise names that match the user's Yours exercise library when possible.
- Use `recordMode: "standard"` for set-based strength work.
- Use `recordMode: "free"` for running, basketball, cycling, stretching, mobility, or other work that should be recorded as one activity with duration and notes.
- `sets` must be numeric.
- `reps` may be a number or range string such as `"6-8"`.
- Put coaching notes, RIR, tempo, substitutions, and safety cues in `note` unless the schema explicitly supports a separate field.
- Use `restSeconds` for rest time when known.
- Do not invent unsupported fields such as `distance`, `pace`, `heartRate`, or `score` in v1 plan JSON; place those details in `note`.

## Exercise Matching

Prefer this order:

1. Exact names from `exercises/` export or CLI `exercise list`.
2. User-provided names.
3. Common names, then report that validation may find missing exercises.

Do not silently invent obscure exercise names. If a plan needs new movements, create separate `.exercise.json` files in `inbox/` so the app can import exercises before the plan.

Built-in exercises may be displayed in the current app language, but user-created exercise names and notes should remain as written.

## Validation

After creating JSON:

1. Parse the JSON.
2. Validate through the Yours CLI when available.
3. Run a dry-run import before a real import.
4. If validation fails, fix format issues or report missing exercises; do not import.

If the CLI is not installed or not available on the device, do not stop at "CLI missing". Instead:

1. Confirm the file name ends with `.plan.json`.
2. Parse the JSON locally.
3. Check the referenced exercise names against `exercises/custom-exercises.json` when available.
4. Create needed `.exercise.json` files or report missing exercises.
5. Tell the user that CLI dry-run was not run and the Yours app inbox import must perform the final validation.

When modifying an existing plan, use `action: "upsert"` plus `matchName` or `syncId`. Do not claim workout logs changed; the app should preserve training history and update only the plan structure.

## Tone

Keep plans practical. Avoid pretending the plan is personalized medical advice. Include clear progression and deload/rest guidance when useful, but keep app JSON concise.
