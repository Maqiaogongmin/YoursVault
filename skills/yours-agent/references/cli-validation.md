# Yours CLI And Manual Validation

The CLI is optional. Mobile agents may not have it installed.

## CLI When Available

```bash
yours --json doctor
yours --json vault inspect /path/to/YoursVault
yours --json vault validate-plan /path/to/YoursVault/inbox/example.plan.json
yours --json vault import-inbox /path/to/YoursVault --dry-run
```

Only run a real import when the user asked for it and validation passed.

## If CLI Is Unavailable

Do not stop at "CLI missing". Perform static checks:

1. Confirm the Vault path and inbox file locations.
2. Parse JSON.
3. Check `.plan.json` / `.exercise.json` extensions.
4. Compare plan action names with `exercises/custom-exercises.json` when available.
5. Create needed `.exercise.json` files or report missing exercises.
6. Tell the user that CLI dry-run was not run and the Yours App inbox importer must perform final validation.

Development checkouts may expose `tool/yours_cli/yours_cli.py` or `yours-cli`, but do not assume those binaries exist on a user's phone.
