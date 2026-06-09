# Yours Plan Import Schema

Use this as the public import shape for agent-authored training plans. Keep files human-reviewable and validate them before import.

## Minimal Plan

```json
{
  "format": "yours-plan",
  "formatVersion": 1,
  "action": "upsert",
  "matchName": "Existing Plan Name",
  "name": "Example Plan",
  "weeks": [
    {
      "week": 1,
      "days": [
        {
          "day": "D1",
          "name": "Full Body",
          "actions": [
            {
              "exercise": "Bench Press",
              "recordMode": "standard",
              "sets": 3,
              "reps": "6-8",
              "weight": "",
              "restSeconds": 120,
              "note": "Leave 1-2 reps in reserve."
            },
            {
              "exercise": "Easy Run",
              "recordMode": "free",
              "note": "20-30 minutes at conversational pace."
            }
          ]
        }
      ]
    }
  ]
}
```

## Recommended Action Fields

Standard record:

```json
{
  "exercise": "Barbell Bench Press",
  "recordMode": "standard",
  "sets": 4,
  "reps": "6-8",
  "weight": 60,
  "restSeconds": 120,
  "note": "Use double progression. Add weight after all sets reach 8 reps."
}
```

Free record:

```json
{
  "exercise": "Basketball",
  "recordMode": "free",
  "note": "30 minutes. Record score or intensity here if useful."
}
```

## Fields

- `format`: must be `yours-plan`.
- `formatVersion`: currently `1`.
- `action`: Use `upsert` when a file may update an existing plan. Use `create` only when a new copy is intended.
- `matchName`: Existing plan name to update. Prefer `syncId` when the exported plan provides one.
- `name`: user-visible plan name.
- `weeks[].week`: week number.
- `weeks[].days[].day`: short day label such as `D1`.
- `actions[].exercise`: exercise name. Prefer names already present in the user's exercise library. The app also accepts legacy `actions[].name`.
- `actions[].recordMode`: `standard` or `free`. Missing values are treated as `standard`.
- `sets`, `reps`, `weight`, `restSeconds`: standard-record fields.
- `note`: optional user-visible note. Use this for RIR, tempo, duration goals, substitutions, distance, pace, score, or safety cues.

## Standard vs Free

Use `standard` for strength training that naturally uses sets, reps, weight, and rest.

Use `free` for cardio, sports, stretching, mobility, outdoor activity, or anything that is better recorded as one activity with duration and notes.

Do not invent distance, pace, heart-rate, or score fields in v1 import files. Put those details in `note`.

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
- Standard actions have `sets` and `reps`.
- Free actions have a clear `note` when the intended duration or activity detail matters.
- Exercise names were checked against the user's library when possible.
- Missing exercises have matching `.exercise.json` files in `inbox/`, or the user was told which exercises are missing.
- If the Yours CLI is unavailable, manual JSON and exercise-name checks were run and the user was told that App import remains the final validation.
