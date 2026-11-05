# UX reconciliation — architecture/TRD

Reviewed: 2026-11-05  
Verdict: **Changes requested — two related P2 findings in the rejected-candidate continuity contract.** No branding approval drift found. No implementation or qualification executed.

## Scope and authority

Read the full UX DESIGN.md and EXPERIENCE.md under `_bmad-output/planning-artifacts/ux-designs/ux-Robotics-2026-11-05/`, `docs/ARCHITECTURE.md`, and `docs/TRD.md`.

This review accepts the parent's stated adoption boundary: AD-6 resolves G1–G3; AD-10/AD-11 resolve G4 mapping/images; AD-9 resolves G5; numeric calibration, G6/G7 and applicable qualification gates remain open by Alisa's authorization. Existing UX gate wording is historical and is not itself a reason to reopen the adopted decisions.

Only this report was written. Source documents remain untouched.

## Findings

### UX-01 — P2: Continuity-loss recovery introduces a driving dead end and an unadopted prerequisite

**Location:** `docs/TRD.md:145` (also T5 at line 341).

The TRD requires the operator to re-establish a view with the rejected candidate absent **before resuming** after tracking/video continuity loss. The same contract disables movement while Paused (lines 124, 131, 136), and the operator remains at a fixed desk driving a robot-mounted camera.

A realistic sequence is: reject a candidate; camera briefly disconnects while still facing it; reconnect and acknowledge. The candidate remains visible. The new prerequisite prevents Resume, while the motion needed to turn the robot away cannot occur before Resume. The document supplies no fixed-desk recovery action that can satisfy the condition. Stop/new-session is available, but silently requiring abandonment of the current session changes the deliberate same-session recovery described by EXPERIENCE.md:113–115 and J5.

The sources require suppression while the same candidate remains continuously visible and eligibility after exit/re-entry (EXPERIENCE.md:112, 238), and require explicit recovery from actual path loss. They do not adopt an absent-view prerequisite or choose an operator action when continuity becomes unknowable. AD-8 selects processing adapters; it does not settle this product outcome. AD-13 authorizes derived contracts, but this affects whether a restored session can resume at all.

**Required resolution:** Specify a feasible fixed-desk recovery path and explicitly record the policy as an adopted invariant or an open decision. Do not choose a new policy through this reconciliation report. In particular, distinguish technical continuity calibration at T5 from approval of the operator-visible consequence. Preserve safety, no automatic Resume, and the approved suppression rule.

### UX-02 — P2: Paused-result rejection conflicts with the paused tracking required for suppression

**Locations:** `docs/TRD.md:99` and `docs/TRD.md:145`; worker ownership at line 91.

Line 99 says the backend rejects results for paused generations. Line 91 assigns candidate tracking observations to the separate inference worker. Line 145 then requires minimal live tracking while matching/alerts are paused so a rejected candidate retains continuity across reject/pause/resume.

As written, an implementer can correctly reject every paused worker result and therefore lose the observations needed to maintain that continuity. This can lead directly to UX-01's recovery lock even during an ordinary review pause. Accepting paused tracking observations instead would contradict the unqualified result rejection rule.

**Required resolution:** Separate candidate-matching results from continuity-only observations in the worker/API contract. Define which tagged continuity observations may be accepted while Paused, prohibit candidate alerts/matching in Paused, and keep end/session/generation/freshness validation. This is a derivable implementation clarification rather than a new driving mode or state.

## Reconciliation coverage

| UX concern | Draft coverage / assessment |
| --- | --- |
| G1 AI unavailable | AD-6 and TRD:129,137,268 block Start or stop/pause; deliberate recovery and local-only behavior retained. Resolved decision correctly identified in TRD:26. |
| G2 interruption | AD-6 and TRD:139–143 end durable unfinished sessions Interrupted, preserve committed Found/reviews and only durable evidence; restart is disarmed. No extra object/session state. Correct supersession of historic UX gate. |
| G3 Stop during review | AD-6 and TRD:135,141 save Not reviewed rather than inventing rejection. End remains Lost. Save failures remain visibly pending/stopped. |
| G4 inputs and images | AD-10/AD-11 and TRD:149–159 specify mappings, ordinary release/ambiguity stop, Circle/UI emergency stop, mirrored coordinates, JPEG/PNG limits and normalized ROI. Actual profiles/calibration remain T4/T6. Keyboard fields preserve a non-drag method. |
| G5 retention | AD-9 and TRD:226–236 preserve registration-based expiry, active grace, immediate confirmed settings effects, inaccessible expired data and actual tracked deletion. Retention unavailable during Searching/Paused; safety Stop/Pause remain permitted during integrity recovery. |
| Left/right live workspace and inactive webcam | TRD:109,116 retain prescribed split and inactive label; controller operation does not require an available webcam. |
| Review versus live imagery | TRD:169 preserves exact immutable evidence frame, Captured evidence label and frame-associated boxes. Stale video becomes Not live, with no fabricated wheel telemetry at line 177. |
| Emergency precedence and persistence | TRD:89,97,114,118,143,173 separate immediate revocation from persistence, keep emergency access during saving/failure, and preserve committed outcomes across later faults. |
| Navigation/focus/operational layout | TRD:118 retains pause-before-navigation, modeless operational panels and no auto-resume. Detailed focus restoration/review-heading announcements and paused readable layout remain in the linked UX guidance; TRD:120 retains documented accessibility/reflow targets rather than replacing them. |
| Accessibility | TRD:120,325 retains keyboard operation, ROI fields, focus, beyond-color state, meaningful announcements, 200% text, contrast and documented reflow. UX Narrator, non-drag selection, no timeout/flashing, keyboard stop, and image labeling remain applicable guidance, subject to G6/T7. Their absence as individually repeated TRD bullets is not a deletion because section 1 explicitly retains the UX documents. |
| Registration/history/detail preservation | TRD:105–107,114,203–214,224 cover search/filtering, duplicate names, immutable registration, sessions/reviews and missing-media placeholders. UX form preservation, return context and screen microcopy remain linked guidance. |
| Branding | DESIGN:119 declares all visual tokens and nonmandated layouts provisional. TRD:24,38,120 and T7 retain that condition. No palette/type/UI-kit/font/icon approval was inferred from document finalization or framework choice. |
| Performance/equipment | AD-14, TRD:28,310–345 preserve exact equipment, electrical, route, thresholds, versions and measurements as gates. Complete-system evidence and prescribed scope are retained; no apparent achieved target or procurement authorization. |

## Non-findings and implementation cautions

- No request to revise the old UX files merely because adopted later decisions resolve historic gates. TRD:26 explains this chronology.
- User authorization permits documentation completion with gates open. This review does not require closing G6/G7, exact runtime versions, image/device calibration, numeric timeouts, wiring or branding before documentation finalization.
- The retained 44px/56px provisional sizing, 320 CSS pixel reflow, focus details and Narrator tests need eventual implementation checks. The references preserve those proposed goals; no evidence currently claims they pass.
- Single backend/device ownership, browser lease, request protection, schemas, revisions/action IDs and frame acknowledgment are derivable technical mechanisms. Their presence alone is not scope expansion.
- No new account, cloud dependency, autonomous behavior, confidence percentage, delete/export screen, public sharing, telemetry upload or extra hardware is introduced.
- No local source of truth says interrupted/unreviewed evidence should become a fourth session/object status; the drafts correctly keep these as dispositions/reasons.

## Recommended disposition

Resolve UX-01's operator-visible continuity recovery policy without silently choosing a new outcome; clarify UX-02's tracking-result exception. Then rerun a narrow reconciliation of those passages against ADs and UX suppression/recovery requirements. Remaining open qualification/branding gates can stay open under AD-14.

