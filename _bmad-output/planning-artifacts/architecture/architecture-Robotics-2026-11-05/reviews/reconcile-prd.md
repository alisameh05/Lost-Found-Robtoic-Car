# PRD reconciliation review

Reviewed 2026-11-05. Read-only review of approved `docs/PRD.md` against draft `docs/ARCHITECTURE.md` and `docs/TRD.md`. No implementation or performance was tested. Only this report was written.

## Verdict

**Two narrow P2 inconsistencies require correction before these contracts guide implementation.** All FR-1–FR-17, NFR-1–NFR-6 and SM-1/SM-C1/SM-2–SM-4 have substantive coverage. No metric was relaxed, hardware procurement enlarged, or approved state vocabulary replaced. Later adopted architecture decisions are treated as legitimate resolution of PRD-deferred design details, rather than contradictions merely because the PRD left them open. This report describes the reviewed draft snapshot; the parent agent is preparing the repairs.

## Finding

### P2 — Make every expiry denial/display-clear rule conditional on absence of active-session grace

- **Location:** `docs/TRD.md:232`; related display-clearing instruction at `docs/TRD.md:236`.
- **Approved requirement:** PRD FR-15 (`docs/PRD.md:112` and its acceptance paragraph) allows an active session to finish before expired data are removed; expiry during an active session retains data until that session ends. FR-10/FR-11 also require paused evidence review and confirmation to remain possible within that session.
- **Conflict:** TRD section 8.2 first grants grace to Searching and Paused sessions at line 230, but line 232 then says, without qualification, “Crossed-expiry data are denied on every read/action even if a cleanup task is delayed.” Line 236 likewise tells the browser to clear displays “on expiry deadlines and session-end grace removal,” without explicitly exempting a currently active session at the expiry deadline. An implementer following those absolute instructions could deny the current reference/evidence or Confirm/Reject/Resume as soon as registration expiry crosses, although the same session remains active. The explicit grace-aware media contract at line 252 does not resolve the contrary general action/read rule.
- **Effect:** A paused match review crossing expiry could become unusable before the operator finishes it, weakening FR-15 and potentially FR-10/FR-11.
- **Correction:** State that every read/action applies expiry **and active-session grace**, denying crossed-expiry access only where grace does not apply. Likewise clear browser displays at expiry only for non-grace records, and immediately after the grace-granting session ends. Continue denying a *new* session on an expired record. Preserve the immediate purge/denial after terminal commit and the no-grace restart rule.
- **Verification:** Specify a trial crossing expiry while Searching and while Paused with pending review: existing-session data and permitted actions remain usable, no new session is allowed, and terminal completion promptly removes all owned data. This is already broadly called for by the TRD verification table; the normative instructions should agree with it.

### P2 — Do not add a rejected-candidate absence gate to deliberate recovery

- **Location:** `docs/TRD.md:145`, independently identified in the companion UX reconciliation and verified against the same draft here.
- **Approved requirement:** FR-12 requires suppression while the rejected candidate remains continuously visible, with eligibility following exit/re-entry. FR-17 requires restored paths, acknowledgment, Resume and fresh movement input after failure. Neither requires an absent-candidate view before Resume.
- **Conflict:** The draft requires staying Paused after continuity loss until the fixed-desk operator deliberately re-establishes a view where the rejected candidate is absent. A restored camera may still face that candidate, and movement remains disabled while Paused, so this adds a recovery prerequisite beyond the approved restoration sequence. AD-8's tracking implementation choice does not itself adopt that new user-facing gate.
- **Correction:** Remove the absent-before-Resume requirement. Preserve conservative suppression without interpreting uncertain continuity as proof of exit; define/qualify tracking behavior at T5 under the existing Resume/recovery rules. Do not demand robot repositioning before it can move.
- **Verification:** Reject a candidate, lose/recover video while it still occupies the view, then complete normal acknowledgment/Resume/fresh-input recovery without forcing absence first. Ensure the original candidate is not immediately re-alerted merely because continuity was uncertain.

## Functional requirement coverage

| Requirement | Coverage in drafts | Result |
| --- | --- | --- |
| FR-1 Register usable name/image/target, initial Lost/time | AD-7/AD-11; TRD 4 registration, 5 registration transition, 7 objects/media constraints, 8.1 complete durable registration | Covered; validation/ROI format limits are adopted design details. |
| FR-2 One Lost target and one active session including Paused; reuse after unsuccessful Ended | AD-13 and consistency conventions; TRD 2, 5, 7 active-session unique index and Lost guard, 9 Start | Covered. |
| FR-3 Left webcam/gesture and right robot/AI workspace, target/mode/state/connections | TRD 4 workspace/readiness and 6.2 video; AD-2/AD-13 | Covered. Inactive/unavailable webcam in controller mode is explicitly labeled and does not invent an unrelated required input. |
| FR-4 Gestures plus PS4/PS5 actions, exclusive mode selected before Start and locked through Pause | AD-5/AD-10; TRD 5 immutable mode, 6.1 mappings, 9 Start and adapters | Covered. Actual PS4/PS5 mappings/availability remain qualified gates. |
| FR-5 Held input, release/recognition loss stops, no paused/ended movement | AD-5/AD-10; TRD 5 release transition, 6 input samples/arbitration and command expiry | Covered. |
| FR-6 Emergency stop, explicit stopped/Paused state and deliberate recovery | AD-5; TRD 4 modeless accessible stop, 5 failure transition, 6.1 UI/Circle, 6.3 priority stop, 9 emergency endpoint | Covered. |
| FR-7 Required command/input/video loss including frozen feed stops/pauses and names cause | AD-3/AD-5; TRD 4 recovery, 5 latches, 6.2 acquisition/display freshness, 6.3 watchdog, 9.2 failure rules | Covered; whole-system timing remains required. |
| FR-8 Start/Pause/Resume/Stop; Pause matching, same target/session, fresh input, no duration cap | TRD 5 state table, 6 neutral/fresh rearm, 9 actions, 14.1 explicit absence of time cap | Covered. Minimal continuity tracking in Paused is expressly distinguished from prohibited candidate matching. |
| FR-9 Similarity candidates with bounding box, human authority, SM-1/SM-C1 | AD-8; TRD 3 worker isolation/tagging, 5 potential match, 6.2 tagged box/evidence, 12 metrics | Covered; no identity guarantee or automatic Found is introduced. |
| FR-10 Candidate stops/pauses for screenshot/box review, Confirm/Reject/Stop | AD-6/AD-7; TRD 4 review, 5 potential-match transition, 8 save ordering | Covered except expiry-grace inconsistency above. |
| FR-11 Explicit confirmation saves evidence/time, Found and Ended, restart persistence | AD-6/AD-7; TRD 5 Confirm/restart, 7 constrained data, 8.1 atomic confirmation | Covered except expiry-grace inconsistency above. |
| FR-12 Reject saves decision/time, Lost/Paused, explicit Resume and continuous-view suppression | TRD 5 Reject and suppression paragraph, 7 match history, 8.1 commit; T5 and 12 continuity trials | Covered subject to removal of the extra absence-before-Resume gate above; suppression is session-local. |
| FR-13 Local name-searchable Lost/Found history with images/times/every session/reviews and restart survival | AD-7; TRD 4 history/detail, 7 schema/indexes and parameterized name lookup, 8 durable media, 9 reads | Covered. |
| FR-14 Found cannot reopen; new independent Lost registration | TRD 5 registration/terminal rules, 7 Lost-session guard, 10 API authorization, 14.1 explicit rule | Covered. |
| FR-15 Configurable registration-based retention, seven-day default, active grace, runtime/startup physical purge | AD-9; TRD 7 settings, 8.2 formula/journal/purge, 9 settings/media, 12 verification | Substantive coverage; repair inconsistent absolute denial/display-clear wording as finding above. |
| FR-16 Offline local access without account, public publication or normal upload | AD-1/AD-12; TRD 2 local assets, 9 no SaaS/upload, 10 no-login loopback access, 11 local deployment | Covered; automatic request capability is not a login gate. |
| FR-17 Acknowledge, restore all required paths, explicit Resume, release/reapply held input | AD-5/AD-6; TRD 5 recovery and leases, 6 input/generation/watchdog, 9 acknowledgments and freshness | Covered subject to removing the additional rejected-candidate absence gate above. Reconnect/restart cannot auto-resume. |

## Cross-cutting requirement coverage

| Requirement | Evidence | Result |
| --- | --- | --- |
| NFR-1 Full search/AI offline after setup | AD-1/AD-8; TRD 2 installed assets/no hosted inference, 12 offline complete-flow trial | Preserved. |
| NFR-2 Fixed desk and connected-room operation even for wired demonstration | AD-3; TRD 2 scope, 12 route evidence, T3/T6 and explicit no-scope-reduction rule | Preserved; multi-room Bluetooth/Wi-Fi performance remains unproved. |
| NFR-3 Team Windows laptop with dedicated NVIDIA GPU | AD-8/AD-14; TRD 2 NVIDIA inference, 12 machine evidence, T1/T3 | Preserved; no unsupported exact laptop/version compatibility claim. |
| NFR-4 Durable local data/default seven-day registration retention | AD-7/AD-9; TRD 7–8 and 12 | Preserved subject to grace wording correction. |
| NFR-5 Furnished rooms, stationary obstacles, people clear, floor/low-shelf visible targets | TRD 2 operating conditions, 12 layout/visible-target evidence; PRD remains authority | Preserved. The precise floor/low-shelf condition is inherited by reference rather than contradicted. |
| NFR-6 Metrics apply to complete system | TRD 12 opening and verification table; T6 | Preserved; no component-only benchmark is presented as acceptance. |

## Metrics and protocol reconciliation

| Metric/protocol | Draft contract | Result |
| --- | --- | --- |
| SM-1 | TRD 12: each of five objects, at least 7/10 alerts within three seconds; all fifty records include late/missed trials | Same approved threshold and per-object denominator. |
| SM-C1 | TRD 12: at most one alerted scene among ten separate ten-second scenes lacking visually similar target | Same scene-level count and intended-negative definition. |
| SM-2 | TRD 6.3 and 12: physical wheels stopped within 0.5 seconds of actual event, including detection, transport/lease, output and mechanical stopping | Same threshold; every direction/both modes, emergency, selected device/command/disconnected/frozen video and recovery are retained. Additional backend/queue tests strengthen evidence. |
| SM-3 | TRD 12: twenty minutes without recharge/restart/crash exercising movement/video/AI/review/history | Same whole-system duration and failure conditions. |
| SM-4 | TRD 6.2 and 12: camera event displayed within 0.5 seconds under movement plus AI; observe scene/display together | Same threshold and load condition. |
| Frozen qualification conditions | TRD 12 and T5 freeze objects/references/placements/lighting/model settings, avoid suppression contamination, record failures | Preserved. |
| Room-to-room route/equipment recording | TRD 12 and T3 record route dimensions, links/dropouts and exact equipment | Preserved; same-room results explicitly insufficient. |

## Hardware, state and scope checks

- The full prescribed procurement list and quantities remain owned by PRD section 6 and explicitly incorporated by TRD line 82. Architecture uses one Uno, HC-05, ESP32-CAM, L298N and 4WD chassis rather than replacing them. No extra network hardware, encoders or programming accessory is silently authorized. T2 explicitly gates motor current/driver capability, cell configuration, BMS/charger/regulator compatibility, logic/wiring and programming access, with escalation if the approved list cannot support the design.
- AD-3 selects Bluetooth commands and Wi-Fi video from PRD-deferred communication arrangements. Selecting wireless is within the approved preferred option; it does not promise coverage. Fixed-desk connected-room scope and timing are retained at gates.
- Object statuses remain exactly Lost/Found; session statuses remain Searching/Paused/Ended. Interrupted is an end reason and NotReviewed is an evidence disposition, avoiding accidental new primary states. One Paused session still prevents another active session and still locks mode/target.
- AI failure, interrupted sessions, and Stop during review resolve the PRD's explicitly deferred outcomes: fail closed, end interrupted sessions without fabricating reviews, and retain NotReviewed evidence while Lost. The documents explicitly attribute their adoption to the later architecture session. They do not contradict the earlier baseline simply by supplying these details.
- Retention settings bounds (1–30 whole days), confirmation/impact preview, image formats/limits, gesture mappings, focused workspace, local request capability and detailed API/schema/protocol contracts are recorded as architecture design decisions. None changes a PRD numeric success target or claims measured qualification. Registration remains timestamp-based; changing settings or reusing a Lost object does not reset registration.
- Autonomous navigation/obstacle avoidance, ultrasonic/servo/GPS/mapping, pickup, public sharing, accounts, multiple robots/operators/targets, mode changes within a session and non-Windows support remain excluded.

## Limitations

This reconciliation establishes documentary coverage only. It does not validate technology claims against external documentation, confirm the session's adoption history independently, certify hardware safety/compatibility, run acceptance tests, or close T1–T7. Exact equipment, model settings, clock/lease thresholds, wiring/power and branding remain appropriately gated.
