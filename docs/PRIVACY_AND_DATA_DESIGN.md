# Privacy and Data Design

## Session-Only Tournament Data

Poker Tournament Manager intentionally does not maintain a permanent tournament-history ledger.

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

## Activity-Based Eligibility

The software does not use prior activity to allow or deny tournament creation. User-specific participation safeguards remain outside the application and are neither collected nor enforced.

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

The full development archive remains private because historical source mappings referenced unpublished documents and internal QA material.

This public portfolio package excludes:

- Private source-document filenames and hashes
- Unpublished user-specific policy material
- Internal source-alignment reports
- Historical internal policy documentation
- Real player or event data
- Production source history

The public package focuses on product decisions, architecture, QA, and release evidence.
