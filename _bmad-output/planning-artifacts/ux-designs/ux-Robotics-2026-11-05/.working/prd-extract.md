# Approved PRD extraction

Source: `docs/PRD.md`, final version 1.0, approved by Alisa 2026-11-05. The planning PRD is byte-identical (SHA-256 `9DE5152C346FB41BD3513EC831B8D2E0379A46E7E7BDEC47C16A836C12B208E6`). No upstream UJ IDs or named personas exist; named journey protagonists in UX must be explicitly illustrative.

## Product boundary

Lost and Found is a university project: one operator at a fixed desk, one Windows laptop with dedicated NVIDIA GPU, one manually driven four-wheel camera robot, and one target/session at a time. It searches multiple connected furnished rooms on one floor. Local Wi-Fi exists; internet must not be required after setup. Wireless preferred, wired demonstration permitted only if it still supports fixed-desk room-to-room operation. Visible targets are on floor/low shelves. Stationary obstacles; people kept clear. Live video supports human steering. No normal-operation image/video/evidence uploads and no account/login.

## Exact feature/requirement inventory

| PRD feature | Exact requirement name | Load-bearing UX rule |
| --- | --- | --- |
| 4.1 Object registration and target selection | FR-1 — Register an object. | Name + usable reference image + selected target region are mandatory; invalid image produces visible validation and no completed record. New record Lost; preserve registration time/reference. |
| 4.1 | FR-2 — Select a search target. | Select registered Lost record; identify active target. One active session, including Paused. Ended unsuccessful sessions allow same Lost record in a new session. |
| 4.2 Live view and manual navigation | FR-3 — Show the search workspace. | Required split: laptop webcam/gesture feedback left; live robot video + AI results right. Show target, active mode, session state, results, required-connection availability. |
| 4.2 | FR-4 — Provide exclusive control modes. | Gestures and PS4/PS5 support forward/backward/left/right/stop. Choose before Start, locked until Ended, including while Paused. Inactive mode cannot move. |
| 4.2 | FR-5 — Require held movement input. | Valid direction held = movement; release or loss of recognition = stop. Paused/Ended ignore movement. |
| 4.2 | FR-6 — Provide emergency stop. | Always available during operation; stop movement + pause active session; explicit stopped state; held input cannot clear. Recovery FR-17. |
| 4.2 | FR-7 — Stop on required-input or video loss. | Command-path loss, selected-control disconnection, or robot live-video loss => movement stop + Paused; identify cause, FR-17. Frozen/stale frame is loss and cannot be labeled Live. |
| 4.3 Search and review | FR-8 — Control the session. | Start/Pause/Resume/Stop. Pause disables movement and AI matching. Resume same target/session. No automatic duration limit. Stop saves + ends unsuccessful session, retains Lost. Start/Resume require selected input + live robot feed; fresh movement input only. |
| 4.3 | FR-9 — Suggest visually similar candidates. | Bounding box + potential-match notification, human identity decision. AI never marks Found. |
| 4.3 | FR-10 — Pause for review. | Candidate automatically stops robot and pauses AI; evidence screenshot/box remains visible. Confirm/Reject/Stop. Held input cannot move. |
| 4.3 | FR-11 — Confirm a match. | Explicit confirmation => Found, detection screenshot + confirmation time saved, session Ended without separate Stop. Persists until retention expiry. |
| 4.3 | FR-12 — Reject a match. | Save rejection/review time + screenshot; object Lost; remain Paused until Resume. Suppress same candidate while continuously visible after Resume; eligible after leaves/re-enters. Session-only suppression, not identity recognition. |
| 4.4 Local history and retention | FR-13 — Preserve searchable history. | Local Lost/Found feed, search by name. Name/reference/status/registration time/every session/confirmed and rejected matches/screenshots/review times. Unexpired persists across restart. No public publication. |
| 4.4 | FR-14 — Register Found belongings again. | Found record never reopens Lost; new independent registration needed. Preserve previous Found evidence/status until expiry. |
| 4.4 | FR-15 — Enforce configurable retention. | Default seven days from registration, not session. Delete object + related sessions/decisions/reference/screenshots when expires, including actual data. Startup cleanup before displaying/searching expired records. Active includes paused session: defer expiry until it ends, then remove. New session/settings change never resets registration time. |
| 4.4 | FR-16 — Use local access without login. | No account; anyone using that laptop can access local records. Search/history offline. No normal-operation uploads. |
| 4.5 Recovery | FR-17 — Require deliberate recovery. | E-stop/required failure stays stopped until explicit acknowledgment + restored required connections + Resume. Resume cannot bypass unresolved failure; previous held input must release then reapply before wheels move. |

## State and transition invariants

- Object statuses exactly Lost / Found. Session states exactly Searching / Paused / Ended. Setup/no-session is a UI condition, not an additional persisted session state.
- Pause is not Ended; stopped robot does not imply ended session. Match review, manual Pause, recoverable failures pause. Stop and confirmation end. Rejection stays Paused and Lost.
- Ended never resumes; new attempt uses Lost record only. Active/Paused keeps target/mode locked and prevents second session.
- Manual Pause/review/recovery disable matching and movement; Start/Resume establish readiness but require fresh held movement command.
- Review evidence is captured screenshot, separate from live robot view; stale frozen video must be distinctly labeled.
- Recovery cause identification and acknowledgment must coexist with match review if failure occurs while paused. No restored connection or held input alone can move.
- Retention can expire while active/paused; defer removal until Ended. Explicit UI warning needed before ending an already-expired active record because removal follows immediately (a UX proposal, not an upstream explicit warning requirement).

## Implied application surfaces (names/layout beyond split view are UX proposals)

1. Local Lost/Found feed / launch: searchable name list, status, registration time, reference, empty/loading/cleanup/error conditions.
2. Register object: name, image picker/preview, one-region target selection, validation, cancel/discard handling.
3. Object detail: immutable registration facts/status, reference/target, all sessions and decisions/evidence, new search for Lost / new registration for Found.
4. Search setup: chosen target, exclusive mode, selected-device/command/video readiness, mode instructions, Start gating.
5. Search workspace: required left/right split, live/stale feed, target/mode/state, matching/results, Pause/Resume/Stop/E-stop.
6. Potential-match review: captured screenshot/box, reference comparison, Confirm/Reject/Stop, stopped indicator; can be part of workspace.
7. Recovery: cause(s), acknowledgment, restored readiness, explicit Resume then release/reapply; can be part of workspace.
8. Session/decision detail: review times, confirmed/rejected evidence, outcomes, no-match unsuccessful session.
9. Retention settings: seven-day default, registration-derived expiry preview/explanation, impact of shortened period, save/error states.
10. Connection/mapping guidance: needed readiness explanations/instructions without prescribing architecture.

## Cross-cutting / acceptance mapping

| ID | Requirement/metric | UX consequence |
| --- | --- | --- |
| NFR-1 | Complete offline searching including AI after setup | No internet/login dependency, cloud retry, or upload queue. Distinguish local robot connectivity from internet. |
| NFR-2 | Fixed-desk connected-room operation | Keep controls/video/readiness visible without physical device intervention as normal journey; do not promise qualified coverage. |
| NFR-3 | Windows team's laptop + dedicated NVIDIA GPU | Desktop/laptop experience; no supported mobile/macOS product claim. Exact Windows/device qualification deferred. |
| NFR-4 | Local persistence until registration retention expiry | Persisted outcome labels only after durable save; expiry handling across restart. |
| NFR-5 | Stationary obstacles, people clear, visible floor/low shelf | Operating guidance; no autonomous avoidance claims. |
| NFR-6 | Complete-system metrics | UX cannot claim compliance from mock/spec. |
| SM-1 | Five agreed objects, ten presentations each; >=7 alerts/object within 3s | Target, not guaranteed detection; no fixed confidence/identity promise. |
| SM-C1 | <=1 false-alert scene among ten distinct 10s dissimilar scenes | Human review mandatory; no “certain match” copy. |
| SM-2 | Wheel stop <=0.5s incl detection after release/E-stop/actual required loss | Safety action independent of UI animations/dialogs/network waits; show requested vs verified state honestly if actual stop cannot be sensed. |
| SM-3 | 20min full-system endurance without recharge/restart/crash | No automatic search duration cap; elapsed time informational. |
| SM-4 | Live camera event displayed <=0.5s under movement+AI | Live vs stale distinction, feed-age indication; stale threshold needs architecture qualification within stop budget. |

Acceptance protocols freeze object/reference/placement/lighting/matching settings before detection trials; negative scenes exclude visually similar candidates; fresh presentations avoid suppression contamination. Every failure recorded. Direction/release/E-stop/loss tested in both modes; video disconnection and freeze tested. Room-to-room route dimensions/arrangement and equipment are recorded. These are qualification/report activities, not required product analytics/admin screens.

## Explicit exclusions / boundaries

No autonomy, obstacle detection/avoidance, ultrasonic/servo functions, GPS, map/room mapping, pickup/retrieval, guaranteed unique identity, concurrent operators/robots/targets, in-session mode changes, public/social sharing/cloud accounts, non-Windows support. Only prescribed components may be bought; architecture/procurement choices remain deferred. No extra hardware, cloud service, or framework should be silently introduced by UX.

## Open decisions requiring labels (not approved requirements)

- Brand/color/type/UI system/density, navigation labels/layout outside mandated split; no visual preference supplied in approved PRD.
- Gesture poses and controller mappings; image formats/limits; target region input mechanics; matching settings. UX can propose specifics but label assumptions and require qualification.
- AI unavailable behavior (recommend stop+pause, but this is not yet approved upstream).
- Application interruption semantics: stopped restart recovery; cannot assume session can resume after process restart. Need agreed end/pause/history outcome and robot stop verification.
- Stop during unreviewed candidate: screenshot/history disposition and review outcome label remain explicitly undecided upstream; never imply rejected or confirmed.
- Retention allowed range, change application timing, save-failure behavior. Never change registration timestamp.
- Exact hardware, route, assessment date, measured performance remain unqualified.
- No requirement for login, cloud sync, manual deletion/export, confidence percentages, live-video recording, battery telemetry, room selection/map, gesture-calibration workflow, settings for algorithm thresholds, or a telemetry dashboard. Do not add as MVP obligations.

## Concern scan

Desktop keyboard/pointer accessibility and gesture/controller alternative; status not conveyed by color alone; focus/state announcements; persistent emergency stop; error recovery without automatic motion; local privacy on shared laptop; offline runtime; motion/reduced-motion; large text/Windows scaling; safe small-window behavior; explicit control-mode lock; precise candidate-vs-identity language. PRD does not specify accessibility standard, dark mode, localization, audio, notifications, or branding: any commitment beyond necessary usability needs labeled UX decision/assumption.
