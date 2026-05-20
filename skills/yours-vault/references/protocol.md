# Yours Vault Protocol

Yours Vault is an open folder protocol for agent collaboration with the Yours fitness app.

## Principle

Yours uses its internal database for app runtime state. Agents should use Vault files as an exchange layer:

```text
Yours app database
  -> export
Yours Vault files
  -> agents and CLI read/write reviewable files
Yours Vault/inbox
  -> validation and import
Yours app database
```

Do not treat Markdown as app data. Markdown is for humans; JSON is for import.

## Folder Layout

```text
Yours Vault/
  manifest.json
  plans/
  logs/
  exercises/
  inbox/
  reports/
```

- `manifest.json`: Vault metadata such as protocol version and export time.
- `plans/`: Exported training plans from the app.
- `logs/`: Exported workout logs.
- `exercises/`: Exported custom exercise library.
- `inbox/`: Agent-authored import files waiting for validation and app import.
- `reports/`: Markdown analysis reports created for the user.

## Plan JSON

Use `.plan.json` for importable plans.

```json
{
  "format": "yours-plan",
  "formatVersion": 1,
  "name": "Two Month Strength Plan",
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
              "sets": 4,
              "reps": "6-8",
              "weight": 60,
              "restSeconds": 120,
              "note": "Keep 1-2 reps in reserve."
            }
          ]
        }
      ]
    }
  ]
}
```

Required in practice:

- `format`
- `formatVersion`
- `name`
- `weeks`
- `days`
- `actions`
- `exercise`
- `sets`
- `reps`

Optional fields:

- `weight`
- `restSeconds`
- `note`
- future extension fields added by the app

## Exercise JSON

Use `.exercise.json` for custom exercise changes.

Single exercise:

```json
{
  "format": "yours-exercise",
  "formatVersion": 1,
  "action": "upsert",
  "name": "Barbell Row",
  "category1": "Back",
  "category2": "Barbell",
  "description": "Keep the torso stable and row the bar toward the lower ribs."
}
```

Batch:

```json
{
  "format": "yours-exercises",
  "formatVersion": 1,
  "exercises": [
    {
      "action": "upsert",
      "name": "Barbell Row",
      "category1": "Back",
      "category2": "Barbell"
    }
  ]
}
```

Use `matchName` when renaming:

```json
{
  "format": "yours-exercise",
  "formatVersion": 1,
  "action": "upsert",
  "matchName": "Old Name",
  "name": "New Name"
}
```

## Naming

Use predictable file names:

```text
YYYY-MM-DD-plan-slug.md
YYYY-MM-DD-plan-slug.plan.json
YYYY-MM-DD-exercises-slug.exercise.json
YYYY-MM-DD-report-slug.md
```

Keep slugs lowercase ASCII when possible. User-facing content inside files may be in the user's language.

## Validation Expectations

Validation should check:

- JSON parses.
- `format` and `formatVersion` match supported values.
- Required fields exist.
- Exercises referenced by a plan exist or are reported as missing.
- Import would not overwrite or hide existing data unless the user asked for replacement.

If validation is unavailable, inspect the JSON manually and say that CLI validation was not run.
