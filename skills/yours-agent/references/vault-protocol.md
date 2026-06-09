# Yours Vault Protocol

Yours Vault is a reviewable file interface, not the app database and not the self-hosted sync server.

## Layout

```text
YoursVault/
  manifest.json
  plans/
  logs/
  exercises/
  inbox/
  reports/
```

- `plans/`: exported app plans; read for context, do not edit in place.
- `logs/`: exported workout history; read for analysis, do not edit in place.
- `exercises/`: exported exercise library; read for action matching.
- `inbox/`: write agent-authored `.plan.json` and `.exercise.json` files here.
- `reports/`: write Markdown analysis only when the user asks for saved reports.

## Boundaries

- App import is the final authority for applying inbox files.
- Server sync is separate from Vault and uses its own protocol.
- Do not copy private local paths, secrets, API keys, or unrelated app data into generated files.
- Do not claim iCloud sync, app import, or database writes happened unless directly verified.
