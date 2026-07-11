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
5. Treat known `built_in:*` references as valid even if an older CLI reports them as missing.
6. Check `recordMode`: only `standard` and `free` are supported. Free actions should include an `exercise` and usually `durationSeconds`.
7. Create needed `.exercise.json` files or report missing exercises.
8. Tell the user that CLI dry-run was not run and the Yours App inbox importer must perform final validation.

Development checkouts may expose `tool/yours_cli/yours_cli.py` or `yours-cli`, but do not assume those binaries exist on a user's phone.

Some development CLI builds may lag behind the app's free-record fields or built-in exercise references. If CLI output drops `recordMode` or `durationSeconds`, or does not recognize `built_in:*`, keep the JSON aligned with the App importer and say the App is the final authority.
