# Local GitHub CLI access

On this Windows host, Codex's offline sandbox cannot read the signed-in GitHub CLI configuration or reach GitHub. For `gh` commands, use `exec_command` with `sandbox_permissions: "require_escalated"` from the first attempt. Invoke one direct `gh` command per call so the existing command rules can match it. The rules allow common read-only commands; GitHub writes still require the normal approval review. Do not copy credentials into the workspace, print a token, or refresh authentication because a sandboxed `gh` command says "Access is denied". If an outside-sandbox command fails, diagnose and report its actual error.

<!-- bmad:context -->
<!-- Verified 2026-11-06 against 0470e2e853ac85b42beba0632b4f7d6df2937ed0. Managed by bmad-project-context; re-verify on refresh. -->

## Orientation

Lost and Found is a local Windows application for manually searching connected rooms with a camera robot and human-reviewed visual matches. The adopted application uses Next.js/React/TypeScript, FastAPI/Python, SQLite with managed images, and local vision/device adapters. Approved requirements and technical decisions live in `docs/`; supporting planning and review artifacts live in `_bmad-output/planning-artifacts/`.

## Policy

- Preserve source authority: PRD owns scope and acceptance; architecture decisions own technical invariants; TRD derives contracts and gates; the implementation guide and phase checklists own sequence and evidence. Change the owning source explicitly before changing an approved requirement.
- Follow the hardware-first schedule: complete Phase 00 acceptance, then Phase 01 before starting Phase 02. Preserve all later dependency and acceptance gates.
- Resolve T2 before relevant wiring or energizing. Keep motor power disconnected and outputs disabled during preparation and stationary subsystem work; actual movement begins only after Phase 12 entry gates pass.
- Keep unverified inventory, versions, model settings, electrical compatibility, thresholds, timing and approvals pending at their named gates. Open gates block their dependent work; continue other permitted work.
- Escalate hardware incompatibility to Alisa and the supervisor. Obtain required supervisor approval before procuring a power-component replacement.
- Keep credentials, runtime databases, private/reference media and unsanitized evidence outside Git. Sanitize tracked evidence before creating it; ignore patterns do not protect already tracked files.

## Where things are

- For scope, state meanings and acceptance metrics, read `docs/PRD.md`.
- For system boundaries and adopted ADs, read `docs/ARCHITECTURE.md`.
- For UI, state/recovery, device/safety, storage, API, security, release or gate work, read the corresponding sections of `docs/TRD.md`: 4, 5, 6, 7–8, 9, 10, 11 or 12–13.
- For any phase task, read `docs/IMPLEMENTATION_GUIDE.md` and its matching `docs/phases/PHASE-XX-*.md` checklist; preserve both guide requirements and checklist deliverables.
- For Phase 00, read `docs/specs/PHASE-00-project-baseline-spec.md` and `docs/phase-00/BASELINE.md` for scope, ownership, inventory, blockers and acceptance disposition.
- For verification and reporting, read `docs/phase-00/ACCEPTANCE-INDEX.md` and `docs/phase-00/REPORT-OUTLINE.md`.
- For interface work, read `_bmad-output/planning-artifacts/ux-designs/ux-Robotics-2026-11-05/DESIGN.md` and `EXPERIENCE.md`, applying later adopted PRD/architecture/TRD decisions first.
- Treat dated PRD copies, architecture snapshots, reconciliation files and validation reports under `_bmad-output/planning-artifacts/` as supporting historical artifacts; use canonical `docs/` sources for current requirements.
- For hardware documentation, follow the implementation guide's MCP-assisted wiring requirements: source-backed connection table, EasyCircuit checks where supported, and editable Fritzing/custom-part/render artifacts. Verify tool availability; diagrams and checks do not establish electrical approval.

## Running and verifying

- TODO: establish reproducible Next.js/Node and FastAPI/Python setup, build and test commands when application manifests exist; qualify exact versions at T1.
- Read the governing phase acceptance criteria before selecting verification. Planning reviews, simulations and component benches do not establish integrated or assessed passes.
- Preserve stable FR/NFR/metric IDs. Record configuration, conditions, checks, failures, evidence and remaining issues; distinguish result status from planned, simulated, bench, integrated or assessed evidence.
- Link evidence only after the artifact exists and has been reviewed. Re-run affected qualification after configuration or implementation changes.

## Conventions that differ from defaults

- Keep presentation in Next.js; keep authoritative session state, device access and serialized storage writes in one FastAPI service. AI runs separately and supplies observations only.
- Keep stopping independent of inference and storage work. Preserve Uno command expiry, fresh-input/video requirements and rejection of stale commands, frames and generations.
- Keep object states Lost/Found separate from session states Searching/Paused/Ended. Paused remains active and disables movement and matching; only committed human confirmation establishes Found.
- Keep rejection Paused until explicit Resume. Recovery requires restored and acknowledged causes, explicit Resume and fresh input; reconnection or restart never restores motion automatically.
- Preserve gestures and PS4 DualShock 4 as the control modes. HC-SR04 warnings are silent and advisory; they cannot change motion, session or readiness, and invalid readings do not mean clear.
- Bind application services to loopback and protect control, data and media channels under TRD section 10. Keep operation local without application accounts or cloud inference.
- Keep backend ownership of SQLite and managed images. Preserve durable evidence commits, crash recovery and registration-based retention with active-session grace.
- Apply current adopted decisions over older UX references to PS5, excluded ultrasonic sensing or unresolved architecture choices. Preserve applicable UX flows, accessibility targets and required implementation evidence.

<!-- /bmad:context -->
