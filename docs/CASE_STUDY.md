# Case Study: From Live-Operations Failure to a Validated Desktop Release

## Project Summary

Poker Tournament Manager is a Windows desktop operations console for structured single-table No-Limit Hold'em tournaments.

The project became a serious product and release-management case study because real tournament use repeatedly exposed failures that were not obvious from isolated development checks.

## My Role

**Product Owner and Release Lead | AI-Assisted Software Development**

My responsibilities included:

- Defining product direction and scope
- Converting live-use problems into requirements
- Setting acceptance criteria
- Interpreting tournament procedures
- Directing UX priorities
- Reviewing implementation reports
- Reproducing defects on physical hardware
- Separating blockers from polish
- Planning regression tests
- Approving or blocking releases
- Verifying packaged builds and release integrity

OpenAI Codex supported implementation. I do not claim sole authorship of the code or every visual detail.

## The Original Problem

The early application could manage tournament data, but it behaved too much like an administrative database tool and not enough like a live operations console.

During a tournament, the host needs immediate answers to a small set of questions:

- What level and blinds are active?
- How much time remains?
- Who has BTN, SB, and BB?
- Who acts first preflop and postflop?
- Which players remain?
- What routine action comes next?

The interface did not initially prioritize that information strongly enough.

## Product Direction

The central design principle became:

> Information needed every hand belongs on the live table. Occasional administrative actions should not permanently consume screen space.

The redesign emphasized:

- One canonical fullscreen live workspace
- A dominant poker table
- A central timer and blind display
- Per-player position and action-order indicators
- Compact routine controls
- Secondary workflows moved under More
- Clear separation between routine and destructive actions

## Defects Found Through Real Use

### Timer display and lifecycle

The authoritative timer could remain correct while the fullscreen frontend failed to refresh. A later lifecycle defect caused the visible timer to work for Tournament 1 but freeze for Tournament 2 and later tournaments in the same application process.

The correction used one reusable application-lifetime WPF pulse and generation-based stale-callback protection.

### Dead-button and position logic

Physical QA exposed multiple edge cases:

- Ordinary unused seats incorrectly generated dead positions
- Legitimate dead BTN and dead SB states needed to propagate correctly
- A four-player to three-player transition lost a legitimate dead position
- Heads-up rules had to begin only at exactly two active players

The fixes were tested through exact seat-by-seat reproductions, action-order checks, undo determinism, and persistence/reload scenarios.

### Fullscreen navigation

F11 and the visible Enter Fullscreen control initially followed different paths. One opened the canonical live workspace while the other only changed window chrome.

Both entry paths were unified.

### Break-workflow failure

After v1.1.0 passed extensive QA, real tournament use exposed another issue: the dedicated break state prevented the host from advancing cleanly to the next blind level.

A printed tournament packet kept the event running. The failure was then converted into a focused v1.1.1 maintenance release.

The dedicated break timer and `OnBreak` workflow were removed. Breaks now use:

1. Pause
2. Conduct break and color-up
3. Advance Level while paused
4. Resume

## QA Method

The project used both automated and physical validation.

Physical QA was especially important for:

- Fullscreen behavior
- Timer refresh across real elapsed time
- Drag/drop seating
- Elimination and restoration
- Dead-button progression
- Heads-up transition
- Multiple sequential tournaments
- Packaged-build behavior on a physical laptop

Results were judged by decision quality and expected state transitions, not by whether a particular hand or tournament outcome was favorable.

## Release Results

Version 1.1.1 completed:

- 274 automated tests passed
- 0 failed
- 0 skipped
- 0 build warnings
- 0 build errors
- EF model/migration parity passed
- NuGet vulnerability audit passed
- Focused physical candidate QA: 5/5 passed
- Final packaged-build QA: 4/4 passed
- SHA-256 artifact verification completed

## What I Learned

The main lesson was that passing automated tests is not the same as operational readiness.

Real users, physical hardware, repeated lifecycles, and state transitions exposed failures that isolated checks did not. My strongest contribution was translating those failures into precise requirements, bounded implementation work, reproducible QA, and disciplined release decisions.

## Professional Relevance

This project demonstrates experience in:

- Product ownership
- Requirements engineering
- UX-informed software delivery
- Stateful workflow analysis
- Quality assurance
- Release management
- Security and privacy hygiene
- AI-assisted development governance
- Technical communication
