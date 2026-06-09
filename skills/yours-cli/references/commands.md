# Yours CLI Command Reference

Use these commands as stable patterns. If the installed CLI differs, adapt the command name while preserving the validation-first workflow.

The CLI is optional. Some mobile agent environments will not have it installed. In that case, do manual static validation and leave final import validation to the Yours app inbox importer.

## Doctor

```bash
yours --json doctor
```

Expected use:

- Confirm the CLI is installed.
- Confirm the app data location or Vault path can be found.
- Confirm JSON output is available.

## Vault Export and Inspect

```bash
yours --json vault export --out /path/to/Yours\ Vault
yours --json vault inspect /path/to/Yours\ Vault
```

Use `export` when the user asks to create or refresh a Vault from app data. Use `inspect` before reading an existing Vault.

## Plan Validation and Import

```bash
yours --json vault validate-plan /path/to/Yours\ Vault/inbox/plan.plan.json
yours --json vault import-inbox /path/to/Yours\ Vault --dry-run
yours --json vault import-inbox /path/to/Yours\ Vault
```

Run in this order. The dry-run should come before the real import.

## Exercise Validation

```bash
yours --json vault validate-exercise /path/to/Yours\ Vault/inbox/exercise.exercise.json
```

Validate custom exercise files before importing an inbox that includes them.

## Exercise and Plan Lookup

```bash
yours --json exercise list
yours --json plan list
```

Use exercise lookup before generating training plans when exact names matter.

## Record Modes

Plan JSON may use:

- `recordMode: "standard"` for set-based strength work.
- `recordMode: "free"` for activity-style work recorded with duration and notes.

Missing `recordMode` should be treated as `standard`.

## Server Sync

Do not use the Vault CLI as a replacement for server sync. Server sync is configured inside the Yours app with a server URL and API key.

## Legacy or Development Builds

Some development builds may still expose older command names. Do not teach new users those names in public documentation. If a user has a local development build, adapt locally and explain that the public workflow is still the Yours CLI workflow.

Local app repository checkouts may expose `tool/yours_cli/yours_cli.py` or `yours-cli`. Do not tell mobile users those binaries must exist.
