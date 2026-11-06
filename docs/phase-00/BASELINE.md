# Phase 00 — Project baseline package

- **Baseline date:** 2026-11-06
- **Status:** Draft; acceptance review incomplete
- **Baseline source revision:** `b5036e396e7c808c0df5ae323318de38e7e2d623`
- **Next phase:** Phase 01, after Phase 00 review; finish Phase 01 before Phase 02.

This package records the available project baseline and assigns explicit follow-up for facts that have not been confirmed. `Pending` means no evidence was available in the repository or current work session; it does not mean the requirement passed. A plan, purchase report, picture, or source document is not an equipment inspection, owner assignment, supervisor confirmation, safety approval, or qualification result.

## Package contents

- [Acceptance and evidence index](ACCEPTANCE-INDEX.md): all 29 stable acceptance IDs.
- [Evidence conventions and report outline](REPORT-OUTLINE.md).
- The [Phase 00 specification](../specs/PHASE-00-project-baseline-spec.md) and [phase checklist](../phases/PHASE-00-project-baseline.md).

## Source baseline and authority

The Git revision below is the inspected repository snapshot for this package. Source files are linked to their current workspace copies; confirm their content identity again before using this baseline for a later release.

| Source | Identity in repository | Authority and use |
| --- | --- | --- |
| [PRD](../PRD.md) | *Lost and Found — Product Requirements Document*, v1.1; created 2026-11-05, updated 2026-11-06 | Owns product scope, FR/NFR requirements, acceptance metrics, approved purchased-item report, and assessment context. |
| [Architecture](../ARCHITECTURE.md) | *Lost and Found — Architecture Decision Record*; updated 2026-11-06; no declared version | Canonical technical decisions AD-1–AD-15. |
| [TRD](../TRD.md) | *Lost and Found — Technical Requirements Document*, v1.1; created 2026-11-05, updated 2026-11-06 | Implementation contracts, technical verification, security, operations, and gates T1–T7. |
| [Experience](../../_bmad-output/planning-artifacts/ux-designs/ux-Robotics-2026-11-05/EXPERIENCE.md) | UX handoff dated 2026-11-05; no declared version | User flows and journey detail, interpreted under later adopted PRD/architecture/TRD decisions. |
| [Design](../../_bmad-output/planning-artifacts/ux-designs/ux-Robotics-2026-11-05/DESIGN.md) | UX design handoff dated 2026-11-05; no declared version | Visual guidance; deferred brand and qualification choices remain at T7. |
| [Implementation guide](../IMPLEMENTATION_GUIDE.md) | Updated 2026-11-06; no declared version | Phase order, dependencies, ownership tracks, evidence and requirement-to-phase coverage. |
| [Phase 00 checklist](../phases/PHASE-00-project-baseline.md) | In repository revision above | Phase 00 work, acceptance boundary, save artifacts and handoff. |
| [Phase 00 specification](../specs/PHASE-00-project-baseline-spec.md) | Created 2026-11-06; published as GitHub issue [#1](https://github.com/alisameh05/Lost-Found-Robtoic-Car/issues/1) | Detailed Phase 00 scope and package-level acceptance checks. |

**Precedence:** PRD owns scope and acceptance. Adopted architecture decisions govern technical invariants. TRD derives implementation contracts and gates. Later adopted decisions override conflicting older UX assumptions. The guide and phase checklists define sequence and evidence handoffs but cannot change the approved requirements. The structural reference implementation plan does not govern this project.

## Phase ownership and dependency record

On 2026-11-06, Alisa confirmed she is the accountable owner for Phase 00, Phases 01–17, and gates T1–T7. Her actual availability/capacity and any supporting contributors remain unconfirmed. The rows below preserve the supporting track and required work without implying that supporting people or time have been committed.

| Phase | Accountable owner | Supporting track | Depends on / entry constraints | Expected output | Availability |
| --- | --- | --- | --- | --- | --- |
| 00 — Baseline | Alisa | Integration/evidence | None | Reviewed source, ownership, inventory, schedule, acceptance and evidence registers, blockers, report outline | Pending confirmation |
| 01 — Hardware readiness | Alisa | Hardware/firmware | 00; T2 review before relevant assembly; keep motor power disconnected and outputs disabled | Inspected inventory, source-backed pin-to-pin wiring list, editable Fritzing/custom parts and rendered diagram, supervisor-reviewed power/wiring/programming plan, safe physical readiness | Pending confirmation |
| 02 — Laptop/vision spike | Alisa | Backend/vision | 00 in dependency graph; under hardware-first schedule, complete 01 before starting 02; T1/T3 inputs | Recorded local inference feasibility and exact machine/configuration evidence | Pending confirmation |
| 03 — Application foundation | Alisa | Frontend/experience and backend/vision | 02; shared contracts and T1 | Local application shell and service boundary | Pending confirmation |
| 04 — Registration/persistence | Alisa | Backend/vision and frontend/experience | 03; T2/T3 as applicable | Registration, local durable records and managed media | Pending confirmation |
| 05 — Camera/video freshness | Alisa | Hardware/firmware, backend/vision | 01, 03; T2/T3/T6; motor outputs disabled during probes | Camera path, fresh-frame handling, display acknowledgment and probe evidence | Pending confirmation |
| 06 — Firmware/command expiry | Alisa | Hardware/firmware | 01, 03; T2/T6; outputs disabled until controlled integration | Command protocol, expiry stop, failure handling and bench evidence | Pending confirmation |
| 07 — Gesture/controller input | Alisa | Frontend/experience and backend/vision | 03; T4/T6 | Exclusive input modes and qualified device profiles | Pending confirmation |
| 08 — Local matching worker | Alisa | Backend/vision | 02, 04, 05; T1/T5 | Local inference adapter and candidate output | Pending confirmation |
| 09 — Session/safety coordinator | Alisa | Backend/vision and frontend/experience | 04, 05, 06, 07, 08; T4/T6 | Authoritative session state, readiness and safety coordination | Pending confirmation |
| 10 — Review/history | Alisa | Backend/vision and frontend/experience | 09 | Review decisions and searchable histories | Pending confirmation |
| 11 — Retention/crash recovery | Alisa | Backend/vision and frontend/experience | 10 | Registration-based cleanup and deliberate recovery evidence | Pending confirmation |
| 12 — Controlled robot integration | Alisa | Integration/evidence with hardware/firmware | 09, 10, 11; T2/T4/T6 exit evidence; supervised controlled movement | Integrated motion, full physical stop evidence, FR-18 warning and system integration | Pending confirmation |
| 13 — UX/visual handoff | Alisa | Frontend/experience | 03, 10, 11; T7 visual decisions | Usable implemented UI and visual/accessibility evidence | Pending confirmation |
| 14 — Offline release | Alisa | Integration/evidence and software tracks | 12, 13; T1 release lock | Reproducible offline release and manifest | Pending confirmation |
| 15 — Multi-room readiness | Alisa | Integration/evidence and hardware/firmware | 14; T3/T5/T6 | Fixed-desk connected-room route evidence on frozen configuration | Pending confirmation |
| 16 — System qualification | Alisa | Integration/evidence and all tracks | 15; all applicable gates | Complete-system acceptance results and failure records | Pending confirmation |
| 17 — Report/demo | Alisa | Integration/evidence and all tracks | 16; T7 assessment instructions | Assessment-aligned report, rehearsed demonstration and release archive | Pending confirmation |

The implementation guide's hardware-first schedule overrides apparent graph parallelism: complete Phase 01 before starting Phase 02. Later phases follow the dependency and gate information above and in the linked guide. Phase 12 is the first planned movement integration; earlier assembly and probes remain motor-disabled. Gate owners are separately listed below.

## Schedule and assessment record

| Item | Current record | Confirmation evidence / next action |
| --- | --- | --- |
| Completion window | PRD reports four weeks as of 2026-11-06. | Reported planning context only; supervisor confirmation not recorded. Execution lead to confirm source and start date. |
| Conditional planning target | 2026-12-04 if the reported four-week window starts on 2026-11-06. | Not an assessment appointment or confirmed submission deadline. |
| Assessment date and time | Pending; timezone not confirmed. | Assessment coordinator to confirm directly with supervisor and record source/date/timezone. |
| Report format and submission instructions | Pending supervisor confirmation. | Assessment coordinator to obtain exact requirements and due condition. |
| Demonstration format | PRD reports supervised manual testing; exact assessment instructions pending. | Confirm room, setup, permitted connections, and demonstration duration with supervisor. |
| Team capacity and availability | Alisa owns all phases and gates; actual hours/dates and supporting contributor capacity remain pending. | Alisa to record actual capacity before assigning milestone dates. |
| Milestone dates and contingency | Pending; no dates assigned. | Schedule after assessment instructions and capacity are confirmed; include time for failures, repairs, and reruns. |

Milestone order is M1 Phase 00–01 physical readiness; M2 Phase 02–04 software feasibility/foundation; M3 Phase 05–11 and 13 stationary subsystems; M4 Phase 12 safe integration; M5 Phase 14–15 release and route; M6 Phase 16–17 qualification and assessment. See [implementation guide](../IMPLEMENTATION_GUIDE.md#milestones-and-scheduling) for exit evidence. No milestone dates are inferred here.

## Inventory record

Quantities below distinguish the PRD's owner-reported purchased baseline from inspection. No physical inspection, exact-variant verification, condition check, or electrical compatibility review was performed for this baseline. `Reported` is not `Inspected`; the reported quantity and model are not a safety clearance. Evidence references are pending unless noted.

| Item | Expected quantity / reported baseline | Inspected quantity and identity | Condition / evidence / inspection date | Owner / next action | Outstanding questions |
| --- | --- | --- | --- | --- | --- |
| 2-layer MDF 4WD chassis, 65 mm wheels | 1 kit; PRD reports purchased | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Confirm exact kit, completeness and condition. |
| DC geared dual-shaft motors, 3–12 VDC, up to 450 RPM | 4; assumed same model in PRD | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Verify exact model, winding/current and left/right pairing. |
| L298 motor driver module | 1 | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Exact variant, current/thermal suitability and cooling remain T2. |
| Arduino Uno R3 | 1 | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Confirm exact board and programming access. |
| ESP32-CAM OV2640 with CH340 | 1 | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Confirm exact board, programming-base arrangement and power. |
| HC-05 Bluetooth module | 1 | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Confirm variant, logic levels and paired configuration. |
| HC-SR04 sensor and holder | 1 each | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Confirm variant and calibration/clear-condition plan. |
| 18650 rechargeable cells, 1200 mAh | 6 (3 active, 3 spare), reported | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Verify cell identity, ratings, condition and compatibility. |
| 3-cell 18650 holder | 1 | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Verify exact connections and condition. |
| TG-008 two-bay 18650 charger | 1 | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Verify independent per-bay specification and cell compatibility at T2. |
| Single-bay 18650 charger | 1; model/output not recorded | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Record exact make/model/output and approved use at T2. |
| 3S 10 A BMS | 1 | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Verify exact board, cell-junction connections and suitability at T2. |
| 7805 regulator, listing marked 5 V/100 mA | 1 | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Verify exact rating/load suitability; no energizing inferred. |
| 20 mm, 3-pin rocker switch | 1 | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Verify exact rating and wiring arrangement at T2. |
| 400-point breadboard | 1 | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Verify type and condition. |
| Male-to-male jumper wires | 20–30 reported | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Count and inspect. |
| Male-to-female jumper wires | 15–20 reported | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Count and inspect. |
| Female-to-female jumper wires | 10 reported | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Count and inspect. |
| USB cable | 1 | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Identify connector/board compatibility and condition. |
| 220 Ω and 1,000 Ω, 1/4 W resistors | 5 each reported | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Count/measure as appropriate; verify circuit use in approved plan. |
| 0.22 Ω and 1 Ω, 0.25 W additional resistors | Purchased as extras; quantities/use unassigned | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Count, identify, and do not assign use without design review. |
| Laptop | PRD/TRD report Lenovo LOQ 15IRH8; Windows 11 Pro, RTX 4050, 16 GB | Exact system/OS/GPU/driver/browser inspection pending | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Verify actual machine, GPU/driver, OS/build, browser and available runtime. |
| Laptop built-in camera | One reported; exact identity not recorded | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Verify camera access and device identity. |
| Controller | One PS4 DualShock 4 reported; CUH-ZCT1 or CUH-ZCT2 to confirm | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Record CUH model and connection/mapping behavior. PS5 is out of scope. |
| Bluetooth and Wi-Fi | Existing laptop capability reported | Pending inspection | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Identify actual adapters and verify selected network endpoints at T3. |
| Network / proposed fixed-desk route | Local Wi-Fi and two adjacent connected rooms reported in PRD | No route or coverage inspection performed | Pending inspection; dated evidence reference pending | Alisa — inspect or verify this record and capture actual quantity/equipment/route details, exact variant where applicable, condition, dated evidence, and disposition of the open questions. | Record non-secret network arrangement, room layout, route and both-link coverage before qualification. |

The approved PRD also reports hardware photographs. Those photos are planning/purchase evidence only and do not establish inspection, ratings, condition, or electrical approval. Keep credentials outside tracked artifacts. T2 remains open for all power, charging, BMS, motor/driver, regulator, logic, wiring, reset-disabled output, and programming questions; T3 remains open for exact equipment and route evidence.

## Blocker and decision register

`Adopted` items below are source-backed decisions, not open assumptions. Alisa is the accountable owner for each open gate; required supervisor reviews and supporting contributor capacity remain separate pending items.

| ID | Gate / requirement | Blocker or decision | Owner | Affected work | Evidence required | Next action / due condition | Status / resolution |
| --- | --- | --- | --- | --- | --- | --- | --- |
| B-OWN | Phase 00 | Alisa is assigned as accountable owner for all phases/gates; actual availability and supporting contributor capacity remain unconfirmed. | Alisa | All phases; all gates | Confirmed capacity/availability and any supporting assignments | Record actual availability before milestone dates and Phase 00 acceptance review. | Open |
| B-ASSESS | T7 | Exact assessment date/time/timezone, report and demo instructions, and submission requirements unconfirmed. | Alisa (assessment coordinator) | Milestones, 13, 16–17 | Supervisor instructions with source and confirmation date | Confirm before dates and assessment plan are committed. | Open |
| B-INVENTORY | T2/T3 | Reported purchases and equipment details have not been reconciled by inspection. | Alisa (hardware/equipment lead) | 01, 02, 05, 06, 12, 15 | Itemized actual quantities, variants, condition and equipment record | Inspect and record before Phase 01 readiness review / route qualification. | Open |
| B-T1 | T1 | Exact software/runtime/dependency/model/GPU configuration is not locked. | Alisa (software/runtime owner) | 02, 03, 08, 14 | Compatible versions/assets, hashes/licenses, reproducible environment and offline manifest | Benchmark and lock before dependent build/release gates. | Open |
| B-T2 | T2 | Power/regulator, cells/chargers, BMS, motor/driver current/thermal, logic, wiring, switch, disabled outputs and programming access require exact-variant review. | Alisa (hardware lead), with supervisor review | 01; reconfirm at 05/06/12 | Supervisor-reviewed purchased variants and power/wiring/programming arrangement | Resolve before wiring/energizing relevant circuits. No approval or procurement is implied. | Open |
| B-T3 | T3 | Actual machine/devices/network and fixed-desk route are not verified. | Alisa (integration lead) | 00/02 inventory, 05/06 probes, 15 | Device inventory and measured two-room route on command/video links | Inventory early; qualify final route in Phase 15. | Open |
| B-T4 | T4 | Gesture/controller mappings and thresholds, neutral/ambiguity behavior, warning/clear condition, scaling and usable layout need actual-device qualification. | Alisa (input/UI owner) | 07/09, verify 12/13 | Frozen profiles and qualification evidence | Record before driving/function tests; accessibility/visual evidence at T7 as applicable. | Open |
| B-T5 | T5 | Matching checkpoint/assets/settings, candidate/continuity criteria and agreed object scenes remain unqualified. | Alisa (vision owner), with supervisor review | 02, 08, 15, 16 | Compatible checkpoint/settings, frozen objects/references/lighting/placements, trial records | Benchmark early; freeze before SM-1/SM-C1. | Open |
| B-T6 | T6 | Firmware/serial/video/display protocol parameters and end-to-end timing budgets are not frozen or qualified. | Alisa (integration/firmware owner) | 03, 05/06, 09, 12, 15, 16 | Frozen parameters/versions and stop/video/endurance timing evidence | Freeze before moving tests and assessed qualification. | Open |
| B-T7 | T7 | Branding/accessibility/visual decisions and assessment instructions/evidence remain outstanding. | Alisa (visual owner), with supervisor review | 00, 13, 17 | Approved visual decisions, verified UI criteria and assessment plan | Resolve before visual sign-off and assessed demonstration. | Open |
| D-SCOPE | Adopted PRD/ADs | PS4 DualShock 4 only; PS5 removed with supervisor approval recorded in PRD v1.1. | Recorded in PRD | 04, 07, 09, 12, 13 | PRD v1.1 and adopted ADs | Preserve approved scope; no further action unless formally revised upstream. | Adopted |
| D-SAFETY | Adopted AD/TRD | Movement requires fresh selected input and live video; failure stops/pauses and recovery is deliberate; Arduino expiry is independent. | Recorded in architecture/TRD | 05–12, 15–16 | AD-5/AD-6/AD-10 and TRD contracts; later qualification evidence | Preserve invariants; physical pass remains pending at T2/T6 and SM-2. | Adopted |
| D-PROX | Adopted PRD/AD | HC-SR04 gives silent advisory warning only; it never stops, pauses, or steers. | Recorded in PRD v1.1 / AD-15 | 01, 06, 12, 16–17 | PRD FR-18 and AD-15; later calibration and clear-condition evidence | Preserve behavior; threshold and sensor qualification remain pending. | Adopted |

No entry authorizes procurement, charging, wiring, energizing, movement, or gate closure. Open gates block only their dependent work; they do not waive other permitted work.

## Source-control and review baseline

- Repository: Git checkout with `origin` pointing to `https://github.com/alisameh05/Lost-Found-Robtoic-Car.git`; baseline revision above. A working branch `codex/phase-00-baseline` is used for this implementation.
- No root `.gitignore`, `CONTRIBUTING.md`, or documented team review/issue agreement was present at baseline. The project specification does not impose a new commit policy; contributors must agree a normal review process before treating it as team policy.
- A tracked-path scan found the approved planning component photos under `_bmad-output/.../components-page-*.png`. No tracked paths matching environment secrets, runtime SQLite/database files, or common private capture media extensions were found. This scan checked filenames only; it did not inspect or certify file contents.
- Root [.gitignore](../../.gitignore) added with protective patterns for secrets, local runtime records, and private captures. Ignore patterns do not remove already tracked files and do not replace local credential/storage controls.
- Keep approved planning documents and sanitized assessment evidence tracked. Store private/reference images, video, runtime records, credentials, and unsanitized trial media in approved local storage, not this repository.

## Baseline acceptance review

| Review field | Record |
| --- | --- |
| Reviewer | Pending independent/team review |
| Review date | Pending review |
| Baseline revision | `b5036e396e7c808c0df5ae323318de38e7e2d623` (source snapshot before this package) |
| Checks to complete in package review | Source authority, phase/gate coverage, reported-versus-inspected inventory, assessment status, 29 acceptance IDs, evidence semantics, gate blockers, source-control paths and ignore rules |
| Findings | Package artifacts drafted and Alisa named as accountable owner. Actual availability, physical inventory inspection, assessment instructions, milestone dates, and independent acceptance review remain pending. |
| Disposition | **Not accepted / Phase 00 remains in progress.** Availability and package review are incomplete. All unverified results remain Pending; no later phase or technical gate is marked complete. |
| Remaining gated items | B-OWN (capacity), B-ASSESS, B-INVENTORY, B-T1 through B-T7; see register above. |

Phase 00 may be marked Done only after the whole package is reviewed, accountable owners and availability are recorded, all 29 entries have planned verification routes, unresolved facts have real accountable owners and next actions, and findings are dispositioned. Technical gates may remain open with their dependent work blocked. This draft does not pass that review by itself.
