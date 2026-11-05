---
title: "Lost and Found — Implementation Guide"
created: 2026-11-05
updated: 2026-11-05
status: plan-only
scope: Complete approved MVP, laptop application and robot
---

# Lost and Found — Implementation Guide

Build the complete system in **18 phases, 00–17**, progressing from feasibility and safe hardware preparation to the assessed demonstration. Each phase has a linked checklist, acceptance criteria and required evidence. All phases start **Not started**: completed planning documents are not completed implementation.

This guide borrows the organization of the supplied [Pravaha implementation plan](../IMPLEMENTATION_PLAN.md). That document is a structural reference only. Its project instructions, technology choices, dates, completion claims, Git policies and expansion features do not govern Lost and Found. The reference file is preserved.

## Source of truth

| Source | Owns |
| --- | --- |
| [PRD.md](PRD.md) | Approved scope, FR-1–FR-17, NFR-1–NFR-6 and acceptance metrics |
| [ARCHITECTURE.md](ARCHITECTURE.md) | Adopted AD-1–AD-14; canonical technical decisions |
| [TRD.md](TRD.md) | Schema, interfaces, device/safety contracts, deployment and gates T1–T7 |
| [EXPERIENCE.md](../_bmad-output/planning-artifacts/ux-designs/ux-Robotics-2026-11-05/EXPERIENCE.md) and [DESIGN.md](../_bmad-output/planning-artifacts/ux-designs/ux-Robotics-2026-11-05/DESIGN.md) | User flows and visual guidance, with the later TRD decisions and remaining UX assumptions respected |
| This guide and phase checklists | Work order, deliverables, evidence and handoffs; no authority to alter approved requirements |

The selected stack stays **Next.js + React + TypeScript on a local Node server**, **FastAPI/Python**, **SQLite plus managed image files**, and local **OpenCV/MediaPipe/YOLOE/PyTorch/Pygame/pySerial** adapters. Commands use HC-05 → Uno; ESP32-CAM video uses local Wi-Fi. This plan selects no new versions, model checkpoint, electrical values or branding.

## Demonstration goal

The finished system must support this sequence from the operator's fixed desk:

1. Register a belonging using its name, a reference image and one selected target region.
2. Select a control mode and start only when all required capabilities are ready.
3. Drive through connected rooms using the live robot feed. Held input moves; release stops.
4. Receive a potential match: the robot stops and the session pauses with captured evidence.
5. Reject a candidate, remain Paused, then explicitly Resume; suppress the same continuously visible rejected candidate.
6. Confirm the intended candidate: save evidence, mark Found and end the session.
7. Restart the application and inspect unexpired history. Show that faults/reconnection cannot restart motion and retention deletes stored records and images correctly.

Demonstrate gestures and PS4/PS5 control in **separate sessions**. An unsuccessful Ended/Lost session may reuse its registration in another mode; a Found object requires a new registration. Do not switch modes during Searching or Paused. This walkthrough organizes the build; every approved requirement still applies, including the separate twenty-minute endurance trial.

## Phases

Dependencies are completion gates. Work inside a phase may begin against shared simulators/fixtures when its checklist permits; do not mark the phase Done until its real dependencies and acceptance criteria pass.

| # | Phase | Depends on | Produces | Status |
| --- | --- | --- | --- | --- |
| [00](phases/PHASE-00-project-baseline.md) | Project baseline and execution setup | — | Requirement/evidence index, owners, equipment/deadline questions | Not started |
| [01](phases/PHASE-01-hardware-readiness.md) | Hardware review and preparation | 00 | Supervisor-reviewed variants, power/wiring/programming plan; T2 clearance | Not started |
| [02](phases/PHASE-02-laptop-and-vision-spike.md) | Laptop environment and vision feasibility | 00 | Recorded laptop, compatible candidate environment, offline model spike | Not started |
| [03](phases/PHASE-03-application-foundation.md) | Application foundation and shared contracts | 02 | Next.js/FastAPI shell, contracts, protected local services, simulator interfaces | Not started |
| [04](phases/PHASE-04-registration-and-persistence.md) | Registration and persistent records | 03 | SQLite schema, managed media, image/ROI registration and initial history | Not started |
| [05](phases/PHASE-05-camera-and-video-freshness.md) | Camera streaming and video freshness | 01, 03 | Actual camera → backend → browser video, timestamps/epochs/display acknowledgments | Not started |
| [06](phases/PHASE-06-firmware-and-command-expiry.md) | Command firmware and expiry stopping | 01, 03 | Uno/HC-05 protocol, reset-disabled outputs and command-expiry bench evidence | Not started |
| [07](phases/PHASE-07-gesture-and-controller-input.md) | Gesture and controller input | 03 | Qualified sample mappings and fresh/neutral input adapters | Not started |
| [08](phases/PHASE-08-local-matching-worker.md) | Local matching and continuity worker | 02, 04, 05 | Separate inference worker, visual prompts, tagged candidates and suppression context | Not started |
| [09](phases/PHASE-09-session-and-safety-coordinator.md) | Session and safety orchestration | 04, 05, 06, 07, 08 | State machine, readiness, leases, latches and measured initial timing configuration | Not started |
| [10](phases/PHASE-10-review-and-history.md) | Match review, evidence and full history | 09 | Confirm/Reject/Not reviewed outcomes, consistent saves, searchable histories | Not started |
| [11](phases/PHASE-11-retention-and-crash-recovery.md) | Retention and crash recovery | 10 | Registration-based purge, active grace, failure recovery and restart reconciliation | Not started |
| [12](phases/PHASE-12-controlled-robot-integration.md) | Controlled physical integration | 09, 10, 11 | Guarded movement with the full application and both modes; initial physical timing | Not started |
| [13](phases/PHASE-13-ux-and-visual-handoff.md) | UX completion and visual handoff | 03, 10, 11 | Complete usable screens, Alisa's visual approval and operational layout checks | Not started |
| [14](phases/PHASE-14-offline-release.md) | Offline production release | 12, 13 | Production build, Windows launcher, dependency/firmware manifest and cold-start evidence | Not started |
| [15](phases/PHASE-15-multi-room-readiness.md) | Fixed-desk multi-room readiness | 14 | Stable actual route, integrated tuning and frozen qualification configuration | Not started |
| [16](phases/PHASE-16-system-qualification.md) | Whole-system qualification | 15 | Complete FR/NFR results, all five metrics and fault/security regression evidence | Not started |
| [17](phases/PHASE-17-report-and-demonstration.md) | Report, demonstration and handoff | 16 | Assessed report/demo package, release archive and honest limitations | Not started |

Phase 09 is the convergence point for persistence, video, firmware, input and matching. From there the main sequence is **09 → 10 → 11 → 12 → 14 → 15 → 16 → 17**, with Phase 14 also requiring Phase 13. Phases 01 and 02 can run in parallel. Phase 13 can overlap Phase 12 once its own dependencies are complete; operational safety/legibility cannot wait for final branding.

## Milestones and scheduling

The PRD records an expected three-to-six-week assessment window as of 2026-11-05, but no exact date, staffing capacity or hardware lead time is confirmed. The following is an **execution order, not a calendar commitment**. During Phase 00, assign people and dates using actual availability; reserve explicit time for failed trials, fixes and reruns.

| Milestone | Phases | Show this before progressing |
| --- | --- | --- |
| M1 — Feasibility established | 00–02 | Equipment gaps known; compatible local inference spike; supervisor-reviewed hardware plan |
| M2 — Components work without driving | 03–08 | Persisted registration, actual camera freshness, command expiry, both input families, local worker |
| M3 — Complete logic while stationary | 09–11 | Full search/review/history/retention and failure sequences using disabled motors or controlled fixtures |
| M4 — Safe integrated robot | 12–13 | Held-input movement and physical stops with all required services active; complete usable UI |
| M5 — Release and route frozen | 14–15 | Offline production launch and fixed-desk multi-room operation on the recorded configuration |
| M6 — Qualification and assessment | 16–17 | Recorded complete-system passes, report, rehearsed demonstration and release archive |

**Discover expensive failures early:** test model compatibility before building the full UI; check programming/power compatibility before assembly; probe room-to-room video/serial coverage with motor outputs disabled in Phases 05/06. Repeat the route with the actual moving application in Phase 15. An early bench probe never counts as final route qualification.

## Team split

Assign names in Phase 00; these are responsibility groups, not assumed team members. One person can cover several groups. Hardware assembly and movement still wait for their entry gates even when software work runs in parallel.

| Track | Owns | Coordination points |
| --- | --- | --- |
| Hardware/firmware | 01, 05 camera firmware, 06, physical setup for 12/15 | Shared protocol from 03; safety configuration with 09; evidence with 16 |
| Backend/vision | 02, 04, 05 ingestion, 07, 08, 09, 10/11 persistence | Sole session/data ownership; publish schemas before frontend integration |
| Frontend/experience | 03 UI, 04 registration, 05 display acknowledgments, 09/10 controls/review, 11 settings, 13 | Consume shared types; never duplicate backend state authority |
| Integration/evidence | 00 tracking, 12, 14–17 | Record results throughout; coordinate fixes with the owning track |

For a solo build, follow the dependency table rather than trying to finish every screen before touching hardware. Keep the report/evidence index current from Phase 00 onward; Phase 17 assembles the report instead of reconstructing missing measurements.

## Open-gate ownership

These implement TRD T1–T7; they do not replace them. A gate can have an early configuration checkpoint and a later measured exit.

| Gate | Work phases | Exit required |
| --- | --- | --- |
| T1 Runtime/dependency lock | 02 → 03/08 → 14 | Exact compatible packages/runtimes/GPU/assets and reproducible offline release manifest |
| T2 Hardware/electrical design | 01; reconfirm at 05/06/12 | Supervisor-reviewed purchased variants, current/power/logic/wiring/programming arrangement before relevant assembly/energizing |
| T3 Equipment/network/route | 00/02 inventory, 05/06 probes, 15 | Recorded actual devices/network and fixed-desk connected-room route |
| T4 Input/UI operating setup | 07/09; verify at 12/13 | Mappings, neutral/ambiguity rules, device profiles and usable operational layout before driving |
| T5 Matching/continuity | 02 spike, 08 integration, 15 freeze, 16 trials | Recorded checkpoint/settings/tracking criteria and agreed five-object test conditions |
| T6 Protocol/timing | 03 contracts, 05/06 implementation, 09 budgets, 12/15 integration, 16 qualification | Frozen exact parameters before moving tests; complete stop/video/endurance evidence before acceptance |
| T7 Visual/assessment | 00 date/roles, 13 visual approval, 17 delivery | Alisa's visual decisions, verified UI criteria and actual assessment instructions/date |

An open hardware or numeric configuration question blocks its dependent implementation/test, not all independent work. Use mocks only for clearly labeled development. Do not ship a mock as the actual device, silently disable required AI, select arbitrary watchdog values or buy extra components to bypass a gate.

## Definition of Done and evidence

Each phase is Done only when its checklist tasks, acceptance checks and applicable gate evidence are complete. Record **what changed, release/configuration identifiers, checks run, results, failures, evidence location and remaining issues**. “UI looks finished,” a library example or simulated success alone is insufficient.

Create the planned evidence index in Phase 00, with one row per FR/NFR/metric and links to relevant trials. Suggested working locations are `evidence/phase-XX/`, `evidence/qualification/` and `evidence/acceptance-index.md`; these names are organizational suggestions, not existing artifacts. Runtime media and secrets stay in their approved local storage/configuration locations, outside source control. Use the agreed assessment test objects for shared evidence.

Phase 16 must preserve these exact targets:

| Metric | Pass threshold |
| --- | --- |
| SM-1 | Five objects × ten clearly visible presentations; **at least 7/10 per object alert within three seconds** |
| SM-C1 | Ten separate ten-second scenes without a visually similar target; **at most one alerted scene** |
| SM-2 | **Wheels stop within 0.5 seconds**, including detection, after release, emergency stop or actual required-path loss |
| SM-3 | **Twenty minutes** without recharge, restart or crash while exercising the complete system |
| SM-4 | Camera event → laptop display **within 0.5 seconds** with control and AI active |

## Required-feature coverage

| Requirement | Implementation phases | Final verification |
| --- | --- | --- |
| FR-1 Registration/target region | 04 | 16 |
| FR-2 Single target/session | 09 | 16 |
| FR-3 Split workspace/live state | 03, 05, 09, 13 | 16 |
| FR-4 Exclusive gesture/controller modes | 07, 09, 12 | 16 |
| FR-5 Held movement/release | 06, 07, 09, 12 | 16 / SM-2 |
| FR-6 Emergency stop | 06, 09, 12, 13 | 16 / SM-2 |
| FR-7 Command/input/video loss | 05, 06, 07, 09, 12 | 16 / SM-2 |
| FR-8 Start/Pause/Resume/Stop | 09, 10, 12 | 16 |
| FR-9 Similarity alerts/boxes | 02, 08, 09 | 16 / SM-1, SM-C1 |
| FR-10 Automatic pause/review | 09, 10 | 16 |
| FR-11 Confirm/Found/evidence | 10 | 16 |
| FR-12 Reject/Paused/suppression | 08, 09, 10 | 16 |
| FR-13 Searchable persistent history | 04, 10, 11 | 16 |
| FR-14 New registration after Found | 04, 10 | 16 |
| FR-15 Configurable retention/real deletion | 04 storage primitives, 11 full lifecycle | 16 |
| FR-16 Local/no login/no normal upload | 03, 14 | 16 |
| FR-17 Deliberate recovery/fresh input | 06, 07, 09, 11, 12 | 16 |
| NFR-1 Offline complete searching | 02, 03, 08, 14 | 16 |
| NFR-2 Fixed-desk multi-room operation | 05/06 early probes, 12, 15 | 16 |
| NFR-3 Windows/NVIDIA laptop | 02, 08, 14 | 16 |
| NFR-4 Durable local data/retention | 04, 10, 11 | 16 |
| NFR-5 Stated room/obstacle/target conditions | 01 planning, 12, 15 | 16 |
| NFR-6 Complete-system performance | 12, 14, 15 | 16 / all metrics |

## Scope control and working rules

- Keep all approved MVP features. If time is short, simplify optional decoration, development conveniences or report formatting; preserve usability, assessment content and mandatory checks.
- Never trade away either control family, safety/recovery, offline AI, evidence/history, real retention, multi-room scope or the measured targets without an explicit approved revision.
- Use short integration checkpoints and record blockers early. Do not import the reference's three-day schedule, arbitrary time limit or file-count rule.
- Agree shared schemas/protocols before parallel units diverge. Changes that affect an AD or PRD requirement need an explicit source revision; implementation convenience cannot silently change the architecture.
- Do not enable actual movement before Phase 12's entry gate. Firmware output/expiry benches in Phase 06 remain physically restrained/isolated under the approved hardware plan.
- Use development reload only with motors disabled. Ordinary release stops motion but may remain Searching; faults/emergency require the approved acknowledgment/restoration/Resume/fresh-input sequence.
- Test on the production offline release before claiming final qualification. A later change to a qualified component triggers affected regression/metric reruns.
- Freeze the final passing release for rehearsal/assessment. Record the real freeze date after the assessment date is known; do not invent one here.

## First action

Start with [Phase 00](phases/PHASE-00-project-baseline.md). Its first handoffs are the hardware review in Phase 01 and the laptop/vision spike in Phase 02. Creating this guide completes no phase and purchases, assembles, deploys or runs nothing.
