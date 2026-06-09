# Yours Skills

This folder contains Codex / AI agent skills for working with Yours through reviewable files instead of private app databases.

Use `yours-agent` as the main entry skill for normal work. It gives agents one clear workflow for Vault reading, plan creation, existing-plan updates, custom exercises, inbox files, and validation.

## What You Can Do

After installing these skills, an agent can:

- Turn a user's goals, schedule, equipment, and constraints into a readable training plan.
- Create a matching `.plan.json` file for `Yours Vault/inbox/`.
- Validate plan and exercise files before import.
- Inspect exported workout logs and summarize frequency, progress, and likely bottlenecks.
- Prepare the next training cycle from the user's accumulated training history.

## Skills

- `yours-agent`: Main entry for all Yours Vault, plan, log, exercise, inbox, and validation workflows.
- `yours-vault`: Reference / compatibility skill for the Vault folder protocol.
- `yours-plan-author`: Reference / compatibility skill for plan JSON details.
- `yours-cli`: Reference / compatibility skill for CLI validation when a CLI is available.

## What Users Should Say

Tell agents:

```text
Use $yours-agent to work with my Yours Vault.
```

Users normally do not need to choose among `yours-vault`, `yours-plan-author`, and `yours-cli`. Those skills remain for older agent setups and as focused references.

## Suggested Install

Copy the folders under `skills/` into the skills directory used by your agent. For Codex-style skills, that is commonly:

```bash
~/.codex/skills/
```

Use your agent's own installation process if it differs.

## Current Yours Concepts

- Yours is local-first. The app database is internal state and should not be edited directly.
- Yours Vault is a file exchange format for exports, imports, reports, and agent collaboration.
- Agent-authored changes should be written to `inbox/`; exported `plans/`, `logs/`, and `exercises/` are reference data.
- The CLI is optional. If unavailable, agents should do manual static checks and let the app inbox importer be the final authority.
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
