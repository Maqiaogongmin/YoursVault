# Yours CLI Command Reference

Use these commands as stable patterns. If the installed CLI differs, adapt the command name while preserving the workflow.

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

## Legacy or Development Builds

Some development builds may still expose older command names. Do not teach new users those names in public documentation. If a user has a local development build, adapt locally and explain that the public workflow is still the Yours CLI workflow.
