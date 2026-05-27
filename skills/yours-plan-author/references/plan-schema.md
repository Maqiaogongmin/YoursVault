# Yours Plan Schema

Use this as the first public schema for agent-authored Yours plans.

## Minimal Plan

```json
{
  "format": "yours-plan",
  "formatVersion": 1,
  "name": "Beginner Full Body Plan",
  "weeks": [
    {
      "week": 1,
      "days": [
        {
          "day": 1,
          "name": "Full Body A",
          "actions": [
            {
              "exercise": "Squat",
              "sets": 3,
              "reps": "8-10"
            }
          ]
        }
      ]
    }
  ]
}
```

## Recommended Action Fields

```json
{
  "exercise": "Barbell Bench Press",
  "sets": 4,
  "reps": "6-8",
  "weight": 60,
  "restSeconds": 120,
  "note": "Use double progression. Add weight after all sets reach 8 reps."
}
```

## Field Guidance

- `exercise`: Prefer exact library names.
- `sets`: Use a number, not text.
- `reps`: Use a number or a range string.
- `weight`: Use a number when a target load is known. Omit when unknown.
- `restSeconds`: Use an integer. Examples: 60, 90, 120, 180.
- `note`: Store RIR, tempo, substitutions, and coaching notes here unless the app schema adds dedicated fields.

## Markdown Companion

The Markdown version should include:

- Who the plan is for.
- Schedule and duration.
- Weekly progression.
- Exercise substitutions or missing-equipment notes.
- Recovery guidance.
- A note that the JSON file is the importable app data.

## Validation Checklist

- JSON parses.
- `format` is `yours-plan`.
- `formatVersion` is supported.
- Every day has actions.
- Every action has `exercise`, `sets`, and `reps`.
- Exercise names were checked against the user's library when possible.
