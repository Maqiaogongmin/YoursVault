---
name: yours-plan-author
description: Create training plans for the Yours fitness app. Use when Codex needs to turn a user's goals, schedule, equipment, or natural-language program into both a readable Markdown plan and a machine-readable `.plan.json` file for Yours Vault inbox import.
---

# Yours Plan Author

## Overview

Create two deliverables for every Yours training plan: a Markdown version for the user and a `.plan.json` version for the app. Use Yours Vault for delivery and Yours CLI for validation when available.

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
- Use stable exercise names that match the user's Yours exercise library when possible.
- `sets` must be numeric.
- `reps` may be a number or range string such as `"6-8"`.
- Put coaching notes, RIR, tempo, substitutions, and safety cues in `note` unless the schema explicitly supports a separate field.
- Use `restSeconds` for rest time when known.

## Exercise Matching

Prefer this order:

1. Exact names from `exercises/` export or CLI `exercise list`.
2. User-provided names.
3. Common names, then report that validation may find missing exercises.

Do not silently invent obscure exercise names. If a plan needs new movements, create separate `.exercise.json` files or ask the user whether to add them.

## Validation

After creating JSON:

1. Parse the JSON.
2. Validate through the Yours CLI when available.
3. Run a dry-run import before a real import.
4. If validation fails, fix format issues or report missing exercises; do not import.

## Tone

Keep plans practical. Avoid pretending the plan is personalized medical advice. Include clear progression and deload/rest guidance when useful, but keep app JSON concise.
