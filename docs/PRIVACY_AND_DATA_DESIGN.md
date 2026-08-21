# Privacy and Data Design

## Session-Only Tournament Data

Poker Tournament Manager intentionally does not maintain a permanent personal tournament-history ledger.

The active tournament may be persisted temporarily for:

- Crash recovery
- Forced process termination
- Power loss
- Windows shutdown

A confirmed discard removes the active tournament aggregate.

## What May Persist

- Application preferences
- Zoom and fullscreen choice
- Sound settings
- Tournament presets
- Equipment inventory
- Reference material
- Independent session and hand reviews
- Backup metadata

## What the Application Does Not Enforce

The software does not block tournament creation based on prior poker activity and does not enforce:

- Monthly gambling budgets
- Paid-session limits
- Loss limits
- Cooldowns
- Re-entry policy derived from personal history
- Personal responsible-play ledgers

Personal safeguards remain outside the application.

## Release Hygiene

Release and source-control checks excluded:

- Production databases
- Current tournament state
- Backups
- Logs
- Exports
- Screenshots with personal data
- Build output
- Publish folders
- ZIP artifacts
- Secrets and credentials
- Machine-specific absolute paths

## Public Portfolio Boundary

The full development archive remains private because historical source mappings referenced personal documents and internal QA material.

This public portfolio package excludes:

- Private source-document filenames and hashes
- Personal policy values
- Internal source-alignment reports
- Historical personal-limit documentation
- Real player or event data
- Production source history

The public package focuses on product decisions, architecture, QA, and release evidence.
