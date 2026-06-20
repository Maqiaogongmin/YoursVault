# Yours Plan And Exercise Import Schema

## Plan File

Use `YYYY-MM-DD-slug.plan.json` in `inbox/`.

```json
{
  "format": "yours-plan",
  "formatVersion": 1,
  "action": "upsert",
  "matchName": "Existing Plan Name",
  "name": "Existing Plan Name",
  "weeks": [
    {
      "week": 1,
      "days": [
        {
          "day": 1,
          "name": "Push A",
          "actions": [
            {
              "exercise": "Barbell Bench Press",
              "recordMode": "standard",
              "sets": 4,
              "reps": "6-8",
              "weight": 60,
              "restSeconds": 120,
              "note": "Keep 1-2 reps in reserve."
            },
            {
              "exercise": "Brisk Walk",
              "recordMode": "free",
              "sets": 1,
              "durationSeconds": 1200,
              "weight": 0,
              "restSeconds": 0,
              "note": "Outdoor walk, easy pace."
            }
          ]
        }
      ]
    }
  ]
}
```

- `action`: `create`, `update`, or `upsert`; missing means safe upsert in the App importer.
- `matchName`: existing plan name to update. Prefer `syncId` if the exported plan provides one.
- `actions[].exercise`: preferred exercise field. Legacy `actions[].name` is accepted by the App.
- `recordMode`: `standard` for sets/reps/weight; `free` for duration/activity records.
- Standard actions use `sets`, `reps`, optional `weight`, optional `restSeconds`, and `note`.
- Free actions still require `exercise`. Use `durationSeconds` for target duration. `sets` can represent repeated free items, usually `1`; `weight` and `restSeconds` are optional. Do not use `reps` as meaningful free-record progress.
- Put RIR, tempo, distance, substitutions, free-record context, and coaching notes in `note`.

## Exercise File

Use `YYYY-MM-DD-slug.exercise.json` in `inbox/`.

```json
{
  "format": "yours-exercise",
  "formatVersion": 1,
  "action": "upsert",
  "name": "New Exercise",
  "category1": "Back",
  "category2": "Machine",
  "description": "Short user-facing description."
}
```

Use `matchName` when renaming an existing exercise.

## Validation Checklist

- JSON parses.
- File extension is `.plan.json` or `.exercise.json`.
- Plan names and exercise names are non-empty.
- Plan actions use library exercises, or matching `.exercise.json` files exist in `inbox/`.
- Free-record activities also need library exercises; create entries for activities such as walking, running, stretching, basketball, or cycling when missing.
- Existing-plan updates use `action: "upsert"` plus `syncId` or `matchName`.
