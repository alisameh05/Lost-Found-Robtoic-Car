# Decision-provenance reconciliation

Date: 2026-11-05
Scope: Read-only review of the architecture run `.memlog.md`, `docs/ARCHITECTURE.md`, and `docs/TRD.md`. Targeted checks of the owning PRD and UX EXPERIENCE source distinguish adopted behavior from retained assumptions. No application code, hardware, or qualification was tested. Only this review report was written.

## Verdict

**Needs two narrow provenance corrections before finalization.** AD-1–AD-14, the selected stack, and open qualification gates are otherwise faithfully carried forward. Detailed schema/API, freshness, concurrency, storage-recovery, and local-request contracts are legitimately derived under AD-13; they do not need to have been individually selected by Alisa. Two user-visible restrictions go beyond those authorized technical contracts and are currently written as binding behavior even though the source leaves them unadopted/open. There is also one qualification wording ambiguity worth correcting.

## Findings

### P2 — An unadopted registration restriction becomes a mandatory backend guard

- Location: `docs/TRD.md:230`; related navigation rule at `docs/TRD.md:118`.
- Evidence: TRD says, “Registration/settings changes are blocked during an active session.” The memlog's adopted AD-9 blocks settings during Searching/Paused; it does not block registering an independent object. PRD FR-2 restricts concurrent active targets/sessions, not independent registration. The actual source of the wider restriction is `EXPERIENCE.md:43`, explicitly marked **[ASSUMPTION IA2]** and explicitly called a UX proposal. TRD authority text at lines 24–26 says remaining UX assumptions stay proposals unless adopted below, but does not identify registration blocking as a newly derived UI proposal or newly adopted decision.
- Why it matters: This adds a product eligibility rule beyond one active search. Backend enforcement prevents registration even through a noncontrolling read-only tab while the existing session is safely Paused. It is not necessary to implement SQLite consistency, single session ownership, or unchanged retention settings.
- Correction: Retain the approved no-second-session/no-mode-change and settings restriction. Either leave registration availability as an explicit UX proposal/open decision, or describe a narrow derived operational navigation guard with clear rationale and provenance instead of adding a global backend registration ban. If a mandatory global ban is intended, obtain its explicit adoption rather than attributing it to AD-9/AD-13.

### P2 — Continuity-loss recovery is fixed despite being left as a qualification/design gate

- Location: `docs/TRD.md:145`; compare gate T5 at `docs/TRD.md:341`.
- Evidence: PRD FR-12 requires suppression while a rejected candidate remains continuously in view and eligibility after exit/re-entry. The adopted decisions authorize detailed protocols and failure stopping; they do not select a new operator recovery policy for uncertain candidate continuity. TRD line 145 requires the operator to re-establish a view with the rejected candidate absent before any Resume, while T5 still lists “continuity-loss recovery” among decisions/evidence to freeze.
- Why it matters: This is a user-visible recovery condition, not merely a tracking threshold or API representation. With a stationary robot and rejected candidate still ahead, a transient tracking/video fault can make Resume impossible until the scene changes externally or the session is ended. The current text commits this behavior before checking its operability, yet the intended decision remains open at T5.
- Correction: Keep the non-negotiable invariant that uncertain tracking is not proof of exit and must not produce a duplicate alert. Describe the absent-view recovery as a **derived proposal pending T5 validation/adoption**, and retain conservative stopping while the policy is unresolved; or record explicit adoption if already supplied in the actual user conversation. Do not present this particular recovery interaction as a direct user selection.

### P3 — AD-8 can be read as asserting completed NVIDIA qualification

- Location: `docs/ARCHITECTURE.md:87`.
- Evidence: “NVIDIA inference is qualified on the selected laptop” uses completed/present qualification language. The memlog expressly says “subject to explicit qualification”; no laptop/model/runtime combination is selected or tested. Surrounding architecture/TRD caveats correctly say qualification is pending.
- Correction: Change to “NVIDIA inference must be qualified on the selected laptop” (or “remains subject to qualification”). This is a wording fix, not a new approval or test requirement.

## Reconciliation that passed

- AD-1/AD-2/AD-4: Browser UI is Next.js/React/TypeScript with a local production Node service and local FastAPI. No Vite/static-export substitution or remote backend appears.
- AD-3/AD-8/AD-14: HC-05/Uno commands and ESP32-CAM Wi-Fi video remain subject to route, timing, electrical, model and runtime qualification. Exact versions, checkpoints, numeric timeouts, board/power details and actual device mappings remain open. The docs do not authorize extra purchases or a same-room scope reduction.
- AD-5/AD-6/AD-10: Fresh selected input, displayed live video, focused workspace, firmware expiry, deliberate rearm, failure pausing, interrupted endings, Not reviewed evidence and human-only Found are retained. No extra object/session states are introduced.
- AD-7/AD-9: Backend-owned SQLite/media writes, registration-based retention, active grace, actual deletion, cleanup failure visibility and settings constraints are consistent with the adopted rules.
- AD-11/AD-12: Approved image limits/ROI behavior and automatic local protection preserve the no-login scope. A request capability is an implementation mechanism, not a new account/login requirement.
- AD-13: Separate worker, REST/events, explicit IDs/revisions/action receipts, single write owner, bounded frame delivery, source age checks and durable file-recovery ordering are reasonably necessary integration contracts, with correct statements that they are derived. Initial endpoint names, logical table/column names, UTC milliseconds, generated media paths and configuration conventions are appropriate implementation-team detail; no further user decision is needed merely because alternatives exist.
- T1–T7: Hardware/equipment/runtime/model/timeout/branding gates remain open with owners and exit evidence. No package/model version, pin, battery configuration, motor current, watchdog interval or measured performance is invented. Documentation finalization is distinguished from qualification.
- Approval history: Draft documents accurately state that AD-1–AD-14 were adopted while detailed TRD contracts were derived. They preserve the PRD/UX sources. There is no general false claim that every schema field or endpoint was personally selected by Alisa.

## Necessary detail versus over-specific detail

The level of schema/API detail is authorized and useful: separate builders need a common initial contract. Protocol freshness/challenges and display acknowledgments add work, but directly address the adopted prohibition on stale/replayed movement and frozen video. Their exact encodings/timing remain at T6, so this review does not require removing them or seeking separate approval for routine protocol design. No new cloud, tenancy, ORM, UI kit, CSS system or procurement choice was introduced.

The two P2 findings differ because they add operational restrictions that cannot be inferred merely from a safe API/schema implementation. Resolve their provenance explicitly rather than stripping otherwise useful implementation contracts.
