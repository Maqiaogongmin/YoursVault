# Yours Vault Protocol

Yours Vault is an open folder protocol for agent collaboration with the Yours fitness app. It is not the app database and it is not the self-hosted sync server.

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
  "name": "Two Month Mixed Plan",
  "weeks": [
    {
      "week": 1,
      "days": [
        {
          "day": "D1",
          "name": "Push And Run",
          "actions": [
            {
              "name": "Bench Press",
              "recordMode": "standard",
              "sets": 4,
              "reps": "6-8",
              "weight": 60,
              "restSeconds": 120,
              "note": "Keep 1-2 reps in reserve."
            },
            {
              "name": "Easy Run",
              "recordMode": "free",
              "note": "20 minutes at conversational pace."
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
- action `name`

Standard actions should include `sets` and `reps`. Free actions should include useful context in `note`.

Optional fields:

- `recordMode`
- `weight`
- `restSeconds`
- `note`
- future extension fields added by the app

Missing `recordMode` is treated as `standard`.

## Data Semantics

- Plans may be active or archived.
- A training week can be manually marked complete; this does not prevent repeating the week or plan.
- Plan actions support `recordMode`:
  - `standard`: strength-style set logging.
  - `free`: activity-style logging for running, basketball, stretching, mobility, and similar training.
- User-created names, notes, and remarks should remain unchanged.
- Built-in exercise display names may be localized by the app. Do not rely on localized display text as a permanent cross-device identity.

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

## Sync Boundary

Yours Vault is for files a user can inspect and import. Self-hosted server sync is a separate service using `protocolVersion: 2` and `identityMode: syncId`.

## Validation Expectations

Validation should check:

- JSON parses.
- `format` and `formatVersion` match supported values.
- Required fields exist.
- Exercises referenced by a plan exist or are reported as missing.
- Import would not overwrite or hide existing data unless the user asked for replacement.

If validation is unavailable, inspect the JSON manually and say that CLI validation was not run.
