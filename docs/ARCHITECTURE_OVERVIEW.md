# Architecture Overview

## Platform

- Windows
- C#
- WPF
- .NET 10
- Entity Framework Core
- SQLite
- xUnit
- Self-contained win-x64 deployment

## Layered Design

### Core

Owns deterministic tournament rules and calculations, including:

- Seating
- Starting-stack validation
- Payout calculations
- Elimination order
- BTN/SB/BB progression
- Dead-button behavior
- Heads-up transition
- Tournament clock calculations

### Application

Coordinates use cases and workflow boundaries, including:

- Tournament creation and validation
- Player registration and seating
- Hand advancement and undo
- Elimination and restoration
- Level advancement and reversion
- Completion and discard
- Recovery decisions

### Infrastructure

Implements external concerns:

- EF Core and SQLite persistence
- Migrations
- Backup and restore
- Exports
- Local application-data paths
- Repository implementations

### WPF

Owns presentation and interaction:

- Main window and navigation
- Fullscreen live workspace
- Commands and dialogs
- Drag/drop seating
- Visual timer projection
- Zoom and fullscreen preferences
- Optional local audio cues

Business-rule authority remains outside XAML and presentation code.

## Timer Architecture

The authoritative clock is timestamp-based rather than a UI counter.

A reusable application-lifetime WPF pulse refreshes the visible timer projection. It does not write to SQLite every second.

Session identity and generation checks reject late asynchronous observations from a prior tournament, preventing Tournament A from overwriting Tournament B.

## Position Architecture

The application persists canonical hand-position state, including:

- Hand number
- Physical or dead button position
- Small blind
- Big blind
- Preflop order
- Postflop order
- Heads-up state
- One prior undo state

For three or more active players, the next state is derived from the previous canonical positions. Heads-up rules activate only when exactly two active players remain.

## Persistence Model

The active tournament is a temporary crash-recoverable aggregate.

- Unclean exit can offer recovery.
- Confirmed discard removes the tournament aggregate.
- Completed data is not retained as a permanent event-history ledger.
- Preferences, presets, inventory, references, and independent reviews may persist.

## Break Workflow

Version 1.1.1 removed the dedicated break state.

Scheduled breaks remain informational structure metadata. Runtime operation uses ordinary Paused state, Advance Level, and Resume.

Legacy persisted `OnBreak` values are normalized safely to Paused at the storage boundary.
