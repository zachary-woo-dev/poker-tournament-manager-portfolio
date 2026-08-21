# QA and Release Process

## Release Philosophy

A release was not accepted merely because the application built or automated tests passed.

Physical Windows-laptop QA remained a required gate for live UI, timer, input, and state-transition behavior.

## Automated Validation

Version 1.1.1 results:

| Area | Result |
|---|---:|
| Core tests | 98 passed |
| Application tests | 6 passed |
| Infrastructure/WPF tests | 170 passed |
| Total | 274 passed |
| Failed | 0 |
| Skipped | 0 |
| Build warnings | 0 |
| Build errors | 0 |
| EF model/migration parity | PASS |
| NuGet vulnerability audit | PASS |

## Physical Candidate QA

Focused v1.1.1 candidate testing passed 5/5:

1. Pause and Advance Level while paused
2. Resume the newly advanced level
3. Revert Level while paused
4. Cross scheduled break boundaries without entering break mode
5. Discard and create another tournament in the same process

## Packaged-Build QA

The final ZIP was independently hash-verified on the physical laptop.

Packaged validation passed 4/4:

1. Clean extracted launch
2. Create/start tournament and pause/advance/resume
3. Cross Level 4 to Level 5 without a break trap
4. Discard and start a second tournament with a working timer

## Release Integrity

Final v1.1.1 release details:

- Version: 1.1.1
- Release commit: `0ab87ada542e74e316d2fd7f6f7f4799dda99efe`
- Annotated tag: `v1.1.1`
- ZIP size: 71,486,363 bytes
- SHA-256: `43761D555F02B75575E5C138E73D484830C1556306B4A67CB6D2C42BB2BD1912`

The packaged artifact was not rebuilt or repackaged after physical acceptance.

## Examples of Release-Blocking Defects

- Visible timer stopped updating after the first tournament lifecycle
- Ordinary unused seats generated false dead positions
- Four-player to three-player transition lost a legitimate dead position
- Visible fullscreen button did not open the canonical live workspace
- Dedicated break state prevented normal level advancement

## Examples of Accepted Non-Blockers

- Minor DEAD BTN/SB text overlap on some eliminated cards
- Deferred physical crash-recovery validation
- Deferred physical Backup/Restore validation
- Deferred legacy-history cleanup validation

## Decision Quality

Defects were classified by effect on live tournament operation:

- **Release blocker:** incorrect state, unusable workflow, or broken lifecycle
- **High priority:** serious usability or reliability issue without immediate corruption
- **Minor polish:** visual imperfection with no rules or state impact
- **Future work:** useful but outside the approved release scope
