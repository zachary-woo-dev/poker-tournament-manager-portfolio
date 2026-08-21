# Poker Tournament Manager v1.1.1

Version 1.1.1 is a focused Windows x64 maintenance release correcting the dedicated break workflow that failed during a real home tournament. It preserves the accepted v1.1.0 live table, timer pulse, position rules, seating, elimination, payout, recovery, and session-only architecture.

## Fixed

- Removed dedicated break timers and the normal `OnBreak` tournament workflow.
- Removed Start Break, End Break, and Complete Color-Up controls.
- Kept scheduled break and color-up entries as informational structure metadata.
- Made ordinary Pause and Resume the operational break mechanism.
- Kept Advance Level available while Paused.
- Kept Revert Level available while Paused.
- Corrected scheduled boundaries including Level 4 to 5 and Level 8 to 9 so they no longer divert into a separate countdown or trap live operations.
- Normalized legacy persisted `OnBreak` values to Paused at the storage boundary.
- Preserved the application-lifetime timer pulse across discard/completion and later tournaments in the same application process.

## Host Procedure

At a scheduled break:

1. Finish the current hand.
2. Select Pause.
3. Conduct the break and any listed color-up.
4. Select Advance Level while still paused.
5. Select Resume.

There is no dedicated break countdown or break-completion command.

## Validation

- 274 automated tests passed: 98 Core, 6 Application, and 170 Infrastructure/WPF.
- 0 failed and 0 skipped tests.
- Release build completed with 0 warnings and 0 errors.
- EF model/migration parity passed.
- Direct and transitive NuGet vulnerability audit passed.
- Focused physical-laptop acceptance completed 5/5.
- Final packaged-build acceptance completed 4/4.
- The real tournament failure path was physically reproduced and verified corrected.

## Unchanged Boundaries

PRE/POST ordering, dead-button and heads-up rules, seating, eliminations, payouts, timer-pulse ownership, backup/restore, and recovery algorithms were not redesigned.

## Deferred Validation

The following existing areas were not physically revalidated as part of the focused v1.1.1 maintenance scope:

- Crash recovery
- Backup/Restore
- Legacy-history cleanup

These were documented and were not represented as physically accepted.
