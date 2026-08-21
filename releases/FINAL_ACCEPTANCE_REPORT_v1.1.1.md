# Poker Tournament Manager v1.1.1: Final Acceptance Report

## Release Decision

**PASS: finalized locally**

- Product: Poker Tournament Manager
- Version: `1.1.1`
- Release commit: `0ab87ada542e74e316d2fd7f6f7f4799dda99efe`
- Annotated tag: `v1.1.1`
- Tag target: `0ab87ada542e74e316d2fd7f6f7f4799dda99efe`
- Tag message: `Poker Tournament Manager v1.1.1`
- Working tree: clean

## Final Validation

| Validation | Result |
|---|---:|
| Core tests | 98 passed |
| Application tests | 6 passed |
| Infrastructure/WPF tests | 170 passed |
| Total tests | **274 passed** |
| Failed | **0** |
| Skipped | **0** |
| Build warnings | **0** |
| Build errors | **0** |
| EF model/migration parity | PASS: no pending changes |
| NuGet vulnerability audit | PASS: no vulnerable packages |
| TODO/NotImplementedException scan | Clean |
| Repository/diff hygiene | Clean |
| Migration changes | None |

## v1.1.1 Correction

The previous scheduled-break workflow diverted level advancement into a dedicated `OnBreak` state, separate break countdown, and additional completion controls. That behavior caused problems at real break boundaries.

Version 1.1.1 removes:

- Dedicated break countdowns
- Normal `OnBreak` workflow
- Start Break
- End Break
- Complete Color-Up

The host workflow is now:

1. Pause the tournament.
2. Conduct the physical break and color-up.
3. Advance Level while paused.
4. Resume play.

Scheduled breaks and color-ups remain informational structure metadata. Legacy persisted `OnBreak` states load safely as Paused.

The release did not change PRE/POST ordering, dead-button rules, heads-up logic, seating, eliminations, payouts, or application-lifetime timer-pulse behavior.

## Physical Acceptance

Focused candidate QA: **5/5 passed**

- Pause and Advance Level while paused
- Resume the newly advanced level
- Revert Level while paused
- Cross scheduled break boundaries without entering break mode
- Discard and create another tournament in the same process

Final packaged-build QA: **4/4 passed**

- Clean extracted launch
- Create/start tournament and pause/advance/resume
- Level 4 to Level 5 scheduled boundary
- Discard and second tournament with a working timer

The real event failure path was verified in the actual packaged application.

## Final Verified Build

- Configuration: Release
- Runtime: self-contained Windows x64
- Deployment: folder-based, untrimmed
- Final archive: `PokerTournamentManager-v1.1.1-win-x64.zip`
- Exact archive size: **71,486,363 bytes**
- SHA-256: `43761D555F02B75575E5C138E73D484830C1556306B4A67CB6D2C42BB2BD1912`

The tag, commit, ZIP size, and SHA-256 were reverified on August 18, 2026. No rebuild, republish, repackage, checksum regeneration, or source change occurred during final report generation.

## Deferred Validation

The following remain outside the physically accepted scope:

- Crash recovery
- Backup/Restore
- Legacy-history cleanup

The release was complete locally. No hosted release was created during the acceptance process.
