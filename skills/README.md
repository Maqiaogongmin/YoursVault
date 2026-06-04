# Yours Skills

This folder contains Codex / AI agent skills for working with Yours through reviewable files instead of private app databases.

## Skills

- `yours-vault`: Understand the Yours Vault folder protocol and prepare import files.
- `yours-cli`: Use the Yours CLI as a validation and dry-run safety layer.
- `yours-plan-author`: Turn training ideas into readable plans and importable `.plan.json` files.

## Current Yours Concepts

- Yours is local-first. The app database is internal state and should not be edited directly.
- Yours Vault is a file exchange format for exports, imports, reports, and agent collaboration.
- Self-hosted server sync is separate from Vault. It uses sync events and backup snapshots for cross-device sync.
- Training plans can be active or archived. Archive status does not delete plans or history.
- Training weeks can be manually marked complete, but a plan can always be reused.
- Exercises can use `standard` or `free` record mode:
  - `standard`: sets, reps, weight, rest, and note.
  - `free`: activity duration, exercise name, and note.
- User-created names and notes must remain as written by the user.
- Built-in exercises may be displayed in the current app language, but stable identities should not depend on display text.

## Safety

Do not put secrets, personal training data, local app paths, or server API keys in this repository. Generated import files should go into a user's own Vault `inbox/`, not into this release kit.
