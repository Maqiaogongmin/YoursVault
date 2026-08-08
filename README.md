# Yours Vault

**An open interface between your training data and the AI you choose.**

Yours is a local-first workout tracker for iOS and Android.

Yours Vault is the structured data layer that connects the app to backup, import/export, training analysis, and **user-chosen AI tools**.

This repository also contains **Yours Skills** — Markdown-based instructions that teach AI agents how to understand Yours data, generate exercises, prepare workout plans, read exported training records, and produce files that the app can validate and import.

The main app source code lives here:

https://github.com/Maqiaogongmin/yours-app

## AI-native customization

Yours intentionally includes only a small built-in exercise set.

That gives users freedom to maintain an exercise library and training structure that match how they actually train, while Yours Vault + Yours Skills let AI handle much of the repetitive setup and analysis work.

A typical workflow is:

```text
User goals, schedule, equipment and preferences
                    ↓
             User's AI agent
                    ↓
          Yours Vault + Yours Skill
                    ↓
     Exercises / training plan / analysis
                    ↓
                Yours App
                    ↓
          Real workout records
                    ↓
               Yours Vault
                    ↓
             User's AI agent
```

The agent can follow the Skill to generate missing exercises, prepare workout plans, read exported training records, and help adjust the next training cycle.

**AI plans and analyzes. Yours records reality.**

## What this repository contains

YoursVault publishes:

- Android APK release information and checksums
- App Store download information
- Version notes
- Privacy policy
- Training disclaimer
- The Yours Vault open file protocol
- Yours Skills for AI agents and Codex-compatible workflows

The public repositories are separated by responsibility:

- Main app: https://github.com/Maqiaogongmin/yours-app
- Self-hosted sync server: https://github.com/Maqiaogongmin/yours-sync-server
- Releases, Vault protocol and skills: this repository

## Install Yours

### iPhone

Download from the App Store:

https://apps.apple.com/app/id6772104994

### Android

Use the latest APK from GitHub Releases or the official website:

https://github.com/Maqiaogongmin/YoursVault/releases

https://yours-app.uk

For APK installs, use an official source and verify the published SHA-256 checksum when available.

## Core app features

- **Training plans** — create, archive, and restore your own training structure.
- **Workout logging** — record sets, reps, weight, rest, completion status, and notes.
- **Standard and free-form logs** — suitable for strength training as well as running, ball sports, stretching, and other activities.
- **Custom exercises** — maintain an exercise library that matches your own training language.
- **Multilingual UI** — Simplified Chinese, English, and Japanese.
- **Local-first storage** — no mandatory account for core logging; workout data is stored locally first.
- **Data management** — local backup, Vault export, file restore, and optional self-hosted synchronization.

## Yours Vault

Yours Vault is the structured exchange layer between Yours and external tools. It supports long-term data storage, backup and restore, plan/exercise import and export, training-record analysis, and reviewable AI workflows.

It is designed around a few rules:

- The app manages its own internal database.
- External tools do not directly edit the app database.
- External tools collaborate through reviewable files.
- Validation and dry runs come before import.
- Training data remains under the user's control.
- Server synchronization is optional and self-hosted.

## Agent Skills

The main skill is:

- `skills/yours-agent`

It teaches AI agents how to:

- understand the Yours Vault structure
- analyze exported workout records
- generate a training plan from goals, schedule, equipment, and preferences
- generate missing custom exercises
- prepare compatible plan and exercise files
- use the `inbox/` workflow
- perform available validation steps
- avoid directly modifying the app database

A simple way to use it is to ask your AI agent to access Yours Vault, load the skill from this repository, and then follow the Skill when generating plans, maintaining exercises, or reading training records.

The Skill itself is documentation and operating logic. It does not contain user workout data, secrets, or private local paths.

See [`skills/README.md`](skills/README.md).

## Optional self-hosted sync

Users who want synchronization between supported devices can deploy:

https://github.com/Maqiaogongmin/yours-sync-server

It is intended for a NAS, home server, or VPS.

Yours does not require an official cloud account for core use and does not host your workout records as a mandatory service. The server address, API key, backups, and sync events remain under the user's control.

The sync service uses:

- `protocolVersion: 2`
- `identityMode: syncId`

Self-hosted sync and Yours Vault solve different problems:

- **Yours Vault** — structured data exchange, backup, portability, AI collaboration, and reviewable imports.
- **Sync server** — cross-device incremental synchronization and snapshot recovery.

## Privacy

Yours does not require an account for core workout logging.

Workout records are stored locally by default. Unless the user explicitly exports, backs up, synchronizes, or shares them, Yours does not intentionally upload those workout records as part of its core local workflow.

See `privacy-policy.md` for the complete policy.

## Disclaimer

Yours is a workout logging tool. It does not provide medical advice.

Train according to your own circumstances and seek qualified professional help when dealing with injury, pain, or medical concerns.

See `disclaimer.md` for the complete disclaimer.

## Source and license

The main Yours app is released under `AGPL-3.0-or-later` with an App Store additional permission.

License terms, source-release policy, provenance audit, and third-party attribution are maintained in the main app repository:

https://github.com/Maqiaogongmin/yours-app

## Acknowledgements

Yours originally grew from the open-source wger project before substantial restructuring, rewriting, and a different product direction.

The data-ownership approach behind Yours Vault was also influenced by the general idea that users should be able to keep, inspect, move, and reuse their own files instead of depending entirely on a closed service.

## Feedback

Bug reports, suggestions, and technical discussion are welcome through GitHub and the official project channels.
