---
name: yours-cli
description: Use the Yours command-line interface as the safety layer for the Yours fitness app. Use when Codex needs to validate Vault import files, inspect or export a Yours Vault, list exercises or plans, dry-run imports, import inbox files, or avoid direct database edits while preparing agent-generated data for Yours.
---

# Yours CLI

## Overview

Use the Yours CLI to validate and move data between Yours Vault files and the app when the CLI is available. Prefer CLI validation and dry-runs over direct database writes, but remember that mobile agents may not have a CLI installed.

Do not use the Vault CLI as a substitute for self-hosted server sync. Server sync is configured inside the app with a server URL and API key.

Read `references/commands.md` for command patterns and expected behavior.

## Command Name

Use the public `yours` command in docs and generated instructions:

```bash
yours --json doctor
```

If the installed app version uses a different binary name, follow the user's installed CLI documentation, but keep the same validation-first workflow. Local development checkouts may still expose `tool/yours_cli/yours_cli.py` or `yours-cli`; do not assume those names exist on a user's phone.

## Safe Order

For any write:

1. Confirm the Vault path.
2. Validate the candidate file.
3. Run a dry-run import.
4. Only run the real import when validation and dry-run pass.
5. Report the command result and any files changed.

If the CLI is unavailable, do not abandon the task. Fall back to manual static checks: parse JSON, check `.plan.json` / `.exercise.json` extensions, compare plan exercise names with `exercises/custom-exercises.json`, prepare missing `.exercise.json` files, and tell the user that final validation must happen in the Yours app inbox import.

## Common Workflows

Health check:

```bash
yours --json doctor
```

Inspect a Vault:

```bash
yours --json vault inspect /path/to/Yours\ Vault
```

Validate and import inbox:

```bash
yours --json vault validate-plan /path/to/Yours\ Vault/inbox/example.plan.json
yours --json vault import-inbox /path/to/Yours\ Vault --dry-run
yours --json vault import-inbox /path/to/Yours\ Vault
```

List exercises before generating a plan:

```bash
yours --json exercise list
```

## Handling Missing Exercises

If validation reports missing exercises:

- Stop before import.
- Show the missing exercise names.
- Create or offer to create `.exercise.json` files in `inbox/`, depending on the user's request.
- Validate exercise files before importing them.

## Record Modes

When validating or preparing plan files, preserve `recordMode`:

- `standard`: sets, reps, weight, rest, and note.
- `free`: one activity item with duration handled by the app timer and details in note.

Missing `recordMode` should be treated as `standard` for compatibility.

## Do Not

- Do not write app databases directly for normal plan creation.
- Do not bypass validation because the JSON "looks fine".
- Do not use replacement or overwrite flags unless the user asks.
- Do not print secrets or app credentials.
- Do not claim an import succeeded unless the CLI or app confirmed it.
