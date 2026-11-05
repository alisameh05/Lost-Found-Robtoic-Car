---
name: Lost and Found
description: Application flow, navigation, behavior, states and accessibility contract.
status: final
updated: 2026-11-05
sources:
  - '../../../../docs/PRD.md'
design: DESIGN.md
application-flow-equivalent: true
---

# Lost and Found — Application Experience

## Foundation

This document is the project's **APPLICATION_FLOW.md equivalent**. [The approved PRD](../../../../docs/PRD.md), version 1.0 approved 2026-11-05, owns product scope. [DESIGN.md](DESIGN.md) owns visual identity and tokens; this document owns navigation, behavior and interaction states.

The supported surface is the team's Windows laptop with a dedicated NVIDIA GPU. One operator stays at a fixed desk, driving one four-wheel camera robot through connected rooms on one floor. One target and one session can be active, including Paused. No native-versus-browser implementation stack or UI library is selected. No account or internet is required after setup; local Wi-Fi/robot connections are separate from internet availability.

**Decision convention:** PRD behavior is binding. **[ASSUMPTION]** marks a proposed UX resolution that is not new product approval. The navigation grouping, detailed interaction mechanics, accessibility floor, visual defaults and proposed handling of deferred cases below are assumptions. The [three product outcome decisions identified as gates](#open-decisions-and-handoff-gates) remain unapproved and must be agreed before implementation; this handoff does not hide them behind a “final” document label. Journey names/protagonists are illustrative because the PRD defines no named personas or UJ IDs.

Object status is exactly **Lost** or **Found**. Session state is exactly **Searching**, **Paused**, or **Ended**. “Setup”, “Saving”, “Review”, “Recovery” and “Loading” are UI conditions/reasons, not additional object/session statuses. Paused disables both movement and AI matching. A robot stop does not necessarily end a session.

No autonomous steering, obstacle avoidance/detection, pickup, maps, GPS, ultrasonic/servo functions, guaranteed identity, concurrent operators/robots/targets, cloud accounts, public sharing or non-Windows support is introduced. No manual-delete/export feature, battery telemetry, confidence-percentage display, full-video recording or algorithm-settings screen is required. Hardware, software stack and measured performance remain architecture/qualification work.

## Information Architecture

**[ASSUMPTION IA1]** Primary navigation is **History**, **Register object**, and **Retention settings**. History is the launch destination after startup expiry cleanup. Search setup/workspace and details are task destinations. Match review/recovery are persistent workspace regions, not separate pages that hide video or emergency controls.

| ID / surface | Entry and contents | Exit, Back and return context | Journey |
| --- | --- | --- | --- |
| S1 History | App open/navigation; local Lost/Found feed, name search, reference/name/status/registration/expiry. | Object row → S3; Register → S2; settings → S8. Returning restores name query/scope/scroll where record still exists. | J1, J7, J8, J9 |
| S2 Register object | S1 or Found record's Register again; name, image, target-region selection. | Register success → new S3. Cancel/Back → origin; ask to discard dirty inputs, no completed record on cancel. | J1, J8 |
| S3 Object detail | S1 row or registration success; reference/region/status/registration/expiry plus all sessions. | Lost Search → S4; Found Register again → independent S2; session → S7; Back → S1. Expired/deleted → S1 with explanation. | J1, J6, J7, J8 |
| S4 Search setup | Search on Lost S3; target, exclusive mode, readiness and control guidance. State the operating boundary: stationary obstacles, people kept clear of the robot's path, targets visible on the floor or low shelves. | Start → S5; Back → S3 with no active session created. Select another target only before Start. | J2 |
| S5 Search workspace | Start or return to the single active session; required split plus target/mode/session/readiness and controls. | Pause stays S5. Review → S5a, failure → S5b. Stop or saved confirmation ends → S3; expiry-at-end → S1. Proposed navigation guard below. | J2–J6, J10 |
| S5a Potential-match review | Automatic potential match within S5; captured screenshot/box and reference comparison. | Confirm → Ended/Found then S3 unless expired; Reject → Paused S5; Stop → Ended/Lost, with unreviewed-evidence disposition gate G3. Back does not dismiss or decide. | J3, J4, J6 |
| S5b Recovery | Emergency stop or required-path failure within S5; all causes, acknowledgment, restoration/readiness. | Restore + acknowledge + Resume → S5 Searching, awaiting fresh held input. Stop → Ended/Lost. Review remains if unresolved; no Back bypass. | J5, J10 |
| S7 Session detail | S3 history entry; session state/times and confirmed/rejected decisions/screenshots/review times. | Open evidence in the same detail region; close returns focus to entry. Back → S3. A missing/expired parent returns S1. | J7 |
| S8 Retention settings | Primary navigation when no active session; current period and registration-based effects. | Save → saved settings, explicit impact feedback; Back/Cancel discards unsaved change and returns origin. Proposed active-session restriction below. | J9 |
| S9 Connection & control guidance | Help beside readiness in S4/S5; selected-mode instructions, required paths and permission recovery. | Close returns focus to invoking readiness item; does not acknowledge failure or Resume. | J2, J5 |

**[ASSUMPTION IA2] Active-session navigation:** leaving S5 requests Pause before any page change. Offer Stay in search or Stop session and leave in an inline modeless panel; retain keyboard access to Emergency stop. Do not silently end or create another session. Stop remains distinct from emergency stop. Returning from a nonoperational overlay never resumes. Retention changes and registration/another target are unavailable until Ended, with a visible link back to the active workspace. This restriction avoids changing retention consequences underneath operation; it is a UX proposal, not an extra PRD state.

Window close requests an immediate stop before any discard/exit choice. Application crash, restart and lost focus handling follow Interaction Primitives and gate G2; UI navigation alone cannot guarantee stopping on process failure. Never show a login, onboarding carousel or internet-reconnection gate on launch. Startup cleanup completes before expired records can appear or be selected.

### Screen transitions and focus

**[ASSUMPTION IA3]** Page transitions are immediate; no animation delays stop, evidence capture or connection handling. Move focus to the new page heading, except modal/panel transitions described below. Back restores the invoking row/control and retained list query. If the row expired, focus History heading and announce its removal. Retry stays on the failed task and preserves valid inputs. No action silently switches the selected control mode or target.

## Voice and Tone

Brand posture lives in DESIGN.md. Microcopy reports observable state, the cause, and the next available action. Separate stop commands from physical feedback: display “Movement disabled; session paused” and any known command-path status; do not claim sensed wheel-stop verification unless the system actually has that evidence. The required stopped state must be clear without fabricating telemetry.

| Situation | Copy pattern |
| --- | --- |
| First history | “No objects registered. Register an object to begin.” |
| Name search has no result | “No objects match this name.” Action: Clear search. |
| Target required | “Select the object inside the reference image.” |
| Unusable reference | “This image could not be used. Choose another image.” Add the actual known reason. |
| Pre-start mode | “Choose Gestures or PS4/PS5 controller. The mode stays locked until this session ends.” |
| Searching | “Searching for [object name]. Hold a direction to move; release to stop.” |
| Manual pause | “Paused. Movement and matching are disabled.” |
| Potential match | “Potential match — review captured evidence.” Never “Object found” before confirmation. |
| Rejected | “Rejected. Still Lost. Resume when you are ready.” |
| Emergency stop | “Emergency stop active. Movement is disabled. Check connections, acknowledge, then Resume.” |
| Video frozen/lost | “Robot video is not live. Session paused.” Display known last-frame time/freshness. |
| Held input after Resume | “Release the direction, then hold it again to move.” |
| Unsuccessful end | “Session ended. [Object name] remains Lost.” Only after its outcome saves. |
| Saved confirmation | “Confirmed Found. Evidence saved. Session ended.” |
| Save failure | “Could not save [decision/session/registration]. Your action is not yet recorded.” Provide Retry; keep stopped where applicable. |
| Retention | “Records expire [period] after registration. A new search does not extend this time.” |
| Active record past expiry | “This record has expired. It remains available during this session and will be removed when the session ends.” |
| Local access | “Records stay on this laptop. Anyone using this application here can view them.” |

## Component Patterns

Component names match DESIGN.md.Components. Subcontrols inherit their parent's pattern. All clickable labels and focus indicators use `{typography.label}` and `{colors.focus}`; layout gaps use `{spacing.3}` or `{spacing.4}` as specified visually.

| Component | Behavior and state contract |
| --- | --- |
| Navigation | Names current destination. During active sessions follows IA2; never causes background motion or a second session. Keyboard and pointer access equivalent. |
| Action button | Activates once; repeated activation while pending does not duplicate records/decisions. Disabled eligibility has a visible reason. Retry preserves user context and must not create duplicate persisted actions. |
| Emergency stop | Always available during operation including review, saving, help and recovery. Stops immediately and pauses; no confirmation dialog. Cannot be cleared by reconnect, held input, or dismissing a panel. |
| Field | Persistent label/hint/error; validation on attempted save and correction, without erasing valid values. Search matches object name locally; whitespace-only name is invalid [ASSUMPTION]. Retention syntax/range follows G5. |
| Object row | Opens its record with keyboard/pointer; duplicate names remain distinguishable through reference and registration time. Lost/Found scope controls and name search do not modify records. |
| Status indicator | Separately identifies object status, session state and required-path availability. Announce meaningful changes, not every video frame or repeated input sample. |
| Image selector | Choose local image; preview then select one region. [ASSUMPTION] Drag a rectangle or use labeled position/size controls with keyboard or single-pointer clicks without dragging; preview, reset and explicitly accept selection. Replacing the image clears the prior region. Registration requires a usable image and valid nonzero region inside it. |
| Readiness list | Lists command path, live robot feed and selected input; Gestures requires webcam/input readiness, controller mode requires selected controller. Inactive mode is noncontrolling, not an irrelevant Start blocker. Show known failure/permission reason and guidance. |
| Video panel | Laptop webcam/gesture feedback left; robot video/AI results right. Controller mode retains left panel labeled “Gesture control inactive”; webcam denial must not block controller operation. Distinguish live frame from captured screenshot; stale frame is unavailable video. |
| Target summary | Always shows current target and locked mode/session in S5. It does not allow changing target/mode while Searching or Paused. |
| Session controls | Start only before a session; Pause while Searching; Resume only while Paused and eligible; Stop session ends. No automatic duration limit. Readiness/acknowledgment/review gates are explicit; Ended has no Resume. |
| Evidence review | Automatic stop/pause occurs before asking for a decision. Preserve detection screenshot/box; compare with reference. Confirm saves Found/time/evidence and ends; Reject saves rejection/time/evidence and stays Paused; Stop follows G3. No timeout or default identity decision. |
| Recovery panel | Persistent list of all failure causes, restoration states and explicit acknowledgment. New cause requires acknowledgment too [ASSUMPTION]. Restored connections never Resume; unresolved review also blocks Resume. Emergency stop remains reachable. |
| History list | Shows every session and saved confirmed/rejected decision with labeled times/screenshots. Evidence enlargement is read-only; it cannot change a historical decision or reopen Found. |
| Feedback panel | Persistent task-local loading/empty/error with clear next action; announce once on transition. Safety failures and unsaved decisions never disappear as a transient notification. |
| Confirmation dialog | Used for dirty-input discard and retention consequences only when no session is active. Trap focus, Escape cancels, restore invoking focus. Only one dialog level. During Searching or Paused, leave choices/help/review/recovery are modeless inline panels; Emergency stop stays in the keyboard focus order and operable. Cancellation never resumes motion. |

## State Patterns

### Session and decision transitions

| Current condition | Trigger | Result / next action |
| --- | --- | --- |
| No active session; Lost target selected | Start with selected input, command path and live video ready | Searching on same target/mode. Input must be neutral/released before a new hold can move. |
| Searching | Valid direction held in selected mode | Move only for duration of that valid hold. Inactive mode cannot command. |
| Searching | Release or lost gesture recognition | Stop movement; session may remain Searching if required paths remain available. Lost recognition is not silently replaced by last direction. |
| Searching | Pause | Stop movement and AI matching; Paused. Resume remains explicit. |
| Searching | Candidate alert | Stop movement and matching; Paused with captured screenshot/box and unresolved review. |
| Paused, unresolved review | Confirm | Persist confirmation time + screenshot; Found and Ended, then S3 or expiry removal. No separate Stop. |
| Paused, unresolved review | Reject | Persist rejection/review time + screenshot; Lost, Paused; Resume explicit. |
| Paused after rejection | Resume with readiness | Searching; suppress same continuously visible candidate until it leaves/re-enters. Require fresh movement input. |
| Searching or Paused | Emergency stop or required command/input/video failure | Stop/disable movement and matching; Paused with cause(s) and recovery latch. Preserve outstanding evidence. |
| Recovery latched | Reconnection only / held direction / acknowledgment alone | Stay Paused. None is a Resume action. |
| Paused | Resume after all required paths restored + acknowledged failures + no unresolved review | Same session/target/mode Searching; require old hold released and new hold applied. |
| Searching or Paused | Stop session | Stop movement/matching immediately; save unsuccessful Ended session, object Lost. G3 applies to unresolved review. |
| Decision/end save pending or failed | Repeated command / input | No movement or duplicate outcome. [ASSUMPTION] Remain Paused with pending outcome until save resolves; do not label Found/Ended as saved prematurely. |
| Ended | Resume / old held input | No effect; no movement. Lost may begin a new session; Found requires new registration. |

Operational precedence: emergency stop/required-path loss stops immediately even during candidate capture, confirmation, rejection or persistence. A failure panel must not erase evidence. A confirmed, durably saved outcome is not rolled back by a later connection loss. If saving and failure overlap, preserve the pending decision, show the failure, and never Resume through it. [ASSUMPTION] Serialize outcome commit and expiry cleanup so history never shows a partial confirmation.

### Per-surface states

Normal states are defined by IA and component rules. Focus follows Screen transitions and Accessibility Floor on every surface; internet offline is normal everywhere. Permission denial refers to actual Windows/device/file access, not account authorization.

| Surface | Loading / empty | Error / denial / unavailable | Recovery and preservation |
| --- | --- | --- | --- |
| S1 History | Startup: “Checking local records…” until expiry cleanup finishes; then local records. Zero records vs zero search matches have distinct messages. | Local database/read/cleanup failure: do not expose unfiltered expired data or pretend history is empty. Show Retry and actual reason. | Keep query/scope when retry succeeds. [ASSUMPTION] Block new data-changing tasks until record/retention integrity is established. |
| S2 Register object | No image: selection instructions; loading image: preview placeholder, Register unavailable. No region: explicit select-target hint. | Unusable/unsupported/inaccessible image, missing name/region or save failure shown inline; format/size limits G4. | Retain valid fields/image/region in current form; choose another image or Retry. Cancel image picker leaves form intact. |
| S3 Object detail | Load facts/history with labeled loading region; no sessions → “No searches yet.” | Missing/corrupt evidence has an unavailable placeholder, never a substitute image. Expired record → S1; file denied explains affected evidence. | Preserve other known facts. [ASSUMPTION] Disable Search if required reference/region cannot be read, with repair/new-registration decision left to scope owner. |
| S4 Search setup | No mode selected → choose mode. Connecting/checking paths shows pending separately from unavailable. | Required controller/webcam permission, command path or video unavailable: Start disabled with cause. AI initialization failure follows G1. | Retry device/path without changing target. Never auto-start when readiness becomes available. |
| S5 Search workspace | Before first frame: no “Live” label and no movement; normal no-candidate → “No potential match yet,” not an error. | Required disconnection/frozen frame → S5b. Selected webcam permission revoked stops gesture operation. Storage/AI failure follows proposed safe behavior and G1. | Keep target/mode/session and current evidence. Distinguish input direction stopped from session Paused. |
| S5a Review | Evidence preparation: already stopped/Paused, clear pending status. No decision yet is not a rejected result. | Screenshot/capture/read/save failure: no false saved result; Confirm unavailable if evidence cannot be persisted. | Keep current screenshot if available, provide Retry/Stop. G3 governs Stop without a reviewed decision. |
| S5b Recovery | Restoring paths: still Paused. No pending causes after restore: acknowledgment and Resume remain explicit. | Show all causes including a new loss during recovery; “unavailable” with actionable guidance. | Resolve causes independently; acknowledgment never conceals unresolved causes or unreviewed evidence. |
| S7 Session detail | Loading timeline; no match decisions → “No reviewed matches in this session.” | Missing/denied screenshot labeled unavailable with its saved decision metadata; parent expired → S1. | Retry evidence read; no mutation of original history or implied rejection/confirmation. |
| S8 Retention settings | Load saved value; calculating impact disables Save until known. No affected records gets explicit “No current records expire under this change.” | Invalid/unsupported period, settings-save or cleanup failure: show cause and saved value; G5 applies. | Keep typed proposal for correction. Do not display unsaved period as active or claim deletion completed after a failed cleanup. |
| S9 Guidance | Local instructions are available offline; missing mapping information states “Control mapping not yet configured.” | Actual denied permission explains which input/path is blocked and how to retry after local permission change. | Close returns to origin; help never substitutes for acknowledgment or readiness. |

**[ASSUMPTION ST1] Persistence failure while operating:** request movement stop and Paused before presenting a blocking local-storage error. Keep captured evidence/current inputs in memory where possible, visibly unsaved; Retry does not falsely promise crash durability. Stop/end remains a requested action until its outcome can save; emergency stop always remains usable. Actual write-atomicity and recovery design belongs in architecture.

## Interaction Primitives

### Input, movement and session actions

- Gestures and PS4/PS5 controller both support forward, backward, left, right and stop. Mode chosen before Start stays locked through every Pause/Review/Recovery until Ended. Gesture poses/controller buttons are gate G4; this document does not invent a tested mapping.
- Valid selected directional input must remain held; release/lost recognition stops. Opposing/ambiguous directional input requests stop rather than arbitrarily choosing a direction **[ASSUMPTION IN1]**. Input ignored while Paused/Ended cannot queue for later playback.
- Start/Resume never move by themselves. Require a neutral/released condition followed by a fresh direction hold; a direction held across Pause cannot rearm the robot. Expose “Release input” readiness feedback.
- Emergency stop acts immediately without a confirmation dialog; normal Pause/Stop also stop before persistence/UI transitions. Never wait for a modal, animation, screenshot, disk write or unrelated network response to request stopping. The whole-system SM-2 target includes failure detection and must be verified on physical wheels.
- **[ASSUMPTION IN2]** Losing application focus, minimizing, locking Windows or an unusably small operational layout requests stop and Paused. Return to focus/size never resumes. These are additional UX safeguards, not measured capabilities or a substitute for hardware/process-loss handling.
- No keyboard direction controls are added as a third driving mode. Keyboard/pointer operate application navigation and session/review controls. Keyboard activation of Emergency stop remains available through its focused button; no unqualified global hotkey is assumed.

### Pointer, keyboard and selection

**[ASSUMPTION IN3]** Tab/Shift+Tab follow visual reading order; Enter/Space activate the focused standard control; Escape cancels the topmost dismissible dialog/help region, never clears emergency stop or makes a review decision. Focus has a visible `{colors.focus}` outline. Hover offers explanation only; essential actions remain visible.

Image target selection offers a pointer rectangle plus labeled position/size controls usable by keyboard and ordinary single-pointer clicks/taps without dragging. Focus the selector, set position/size, preview the boundary, reset if needed and explicitly accept selection. Expose selected coordinates/region state as text; values stay within image bounds. This is a proposed interaction method, not a fixed image format/limit. Dragging is optional.

Name search is local and **[ASSUMPTION IN4]** case-insensitive substring search; typing does not navigate away. Announce result count after query settles, not on every keystroke. Clearing restores current Lost/Found scope. Result ordering is most recent registration first, with full registration dates to distinguish duplicate names.

## Accessibility Floor

**[ASSUMPTION A1]** The following is the proposed implementation/verification floor, not a claim that the PRD or unbuilt application already meets a certification. Use [WCAG 2.2 AA](https://www.w3.org/TR/WCAG22/) as the design target for applicable interaction/contrast criteria on the chosen Windows surface and test with Windows Narrator plus keyboard. Visual contrast and type rules live in DESIGN.md.

- Every navigation, form, session, review, recovery and settings action has an accessible name, role and state. Labels say “Confirm match as Found” and “Stop session” distinctly; required, unavailable, selected, locked, saving and invalid states are exposed programmatically.
- All application workflows are keyboard/pointer operable. Driving still uses one of the two required modes; a controller offers an alternative to webcam gestures but does not prove all motor/vision needs are met. Do not claim that audio descriptions can replace live video for safe steering.
- Region selection has the non-drag alternative described above; selected coordinates/region state are exposed as text. Reference/evidence images have names tied to object/session and capture event; AI boxes are labeled “potential match,” not identity claims.
- Emergency stop is always discoverable, operable and focusable during operation. Do not trap keyboard focus in help/review while hiding it. Critical pause/failure transitions announce state and cause once; ongoing frames/freshness ticks do not flood the screen reader.
- Candidate arrival moves focus to the review heading **[ASSUMPTION A2]**, announces movement/matching paused and provides Confirm/Reject/Stop in reading order. Failure during review announces its cause without discarding the operator's review context. Recovery focus lands on cause summary, then acknowledgment/readiness/Resume.
- Confirmation dialogs are limited to no-active-session tasks: trap focus, Escape cancels, and closing restores focus. Operational panels are modeless and keep Emergency stop reachable; page changes focus the heading. Focus never disappears under sticky controls, overlays or scaling. No keyboard traps or hover-only instructions.
- Controls use `{components.action-button.min-height}` minimum height; emergency action uses `{components.emergency-stop.min-height}`. Target 200% text enlargement without content/function loss. Ordinary reading/form screens reflow at a width equivalent to 320 CSS pixels without two-dimensional scrolling; for native Windows use equivalent logical sizing and accessibility tests. Maintain visible labels and operable controls. Contrast, shape and text distinguish all states; sound is not required.
- Motion is functional and minimal. Respect reduced-motion preference; never flash candidate/emergency states. No decision timeout, automatic review dismissal or inactivity-driven search end. Retention is a stated product data lifecycle, not a user-input timeout.
- Errors identify affected fields/actions and corrections; preserve valid input. Save/connection/expiry results are announced without relying on color. Validate reflow, keyboard-only registration through review/history/settings, Narrator reading order, and stop access at supported scaling before release.

## Responsive & Platform

**[ASSUMPTION RP1]** Optimize for a Windows laptop, not a mobile companion. No mobile/macOS support is promised. The supported operational minimum must be chosen on the actual laptop with Windows scaling during UX/architecture qualification; this document deliberately does not invent a tested resolution.

History/forms/details/settings reflow to a single column and scroll vertically at the enlargement/reflow targets above. The operational workspace retains laptop input/gesture feedback left and robot video/results right. Secondary descriptions can move below panels; target/state and Emergency stop/session controls cannot disappear offscreen. At a size/scale that makes driving unusable, request Paused and explain how to restore the layout; no auto-resume on resize. While Paused, provide a readable, modeless single-column arrangement for evidence, review decisions, recovery, Emergency stop and Stop session. Ordinary text/actions must remain usable without restoring the driving layout. Any essential two-dimensional exception applies only to the spatial video/image area, whose left/right relationship remains intact, not to navigation or controls. Evidence may expand while stopped without hiding the emergency action. Do not stretch or crop the robot feed to fill space.

Runtime resources/instructions/fonts must be local after setup. Distinguish Windows camera/file permission failures, controller disconnection and robot local connectivity from internet. Unavailable inactive gesture webcam in controller mode is informational, not a required-input failure. Exact Windows/webcam/controller support and display geometry must be qualified on the team's equipment.

## Local Data, Retention and Privacy

The feed, references, target regions, registrations, every session, saved decisions/screenshots and review times remain local. No login, upload queue, public feed or cloud synchronization is introduced. Inform the operator that anyone using this application on the laptop can access records. Do not promise encryption, backups, account isolation or secure forensic erasure that the PRD does not specify.

Registration time is immutable. Expiry derives from that time and the configured retention, default seven days. A new session, rejection, confirmation, restart or retention change never resets registration time. Lost and Found records both expire. Removal includes actual related local data, not just hiding a row.

| Event | Required behavior and proposed presentation |
| --- | --- |
| Startup | Clean expired data before showing/searching them. Loading/failed cleanup follows S1; never flash expired thumbnails first. |
| Expiry while idle | Remove object and related stored data; if detail is open, return S1 with “This record has expired and was removed.” |
| Expiry while Searching or Paused | Retain until this active session ends. [ASSUMPTION R1] Persistent warning explains removal-at-end before Stop or Confirm, but never adds a blocking confirmation before a stop. |
| Session ends after expiry | Remove object plus sessions, decisions, reference and screenshots. An attempted confirmation can establish the terminal outcome but must not promise retained history after cleanup; return S1 with removal explanation. |
| Shorter configured period | [ASSUMPTION R2] Preview affected records and confirm consequence before Save; saved change applies to existing registrations immediately, then clean expired idle data. G5 requires agreement on permitted values/application timing. |
| Settings save fails | Keep previously saved period active and unsaved proposal visible. Do not reset dates or claim a new period saved. |
| Cleanup fails | [ASSUMPTION R3] Hide expired records from search while reporting actual removal failure; block new data-changing tasks until integrity restored. Never claim stored data were removed until cleanup succeeds. |

Found cannot be reopened. “Register again” starts a complete independent registration with a new time and Lost status. It does not edit the original Found record or extend its evidence lifetime. No auto-copy of an old reference is assumed.

## Key Flows

Each protagonist below is an illustrative office operator at the fixed desk, not a researched persona. Failure branches are part of the flow contract. All journeys work without internet after setup; hardware-dependent paths still require local connections.

### J1 — Register an object and select a target (Mariam, before searching for her keys)

1. Mariam opens the application; startup expiry cleanup completes, then History appears without login.
2. She selects Register object, enters “Desk keys,” and chooses a local reference image.
3. She selects only the keys inside the image, checks the preview and submits Register.
4. **Climax:** Object detail shows a new Lost record, its reference/target, registration time and derived expiry; Search is available.

Failure: missing name/image/region or unusable image prevents completed registration, explains correction and retains valid inputs. Save failure stays in the form; Retry cannot create duplicates. Cancel/Back asks before discarding dirty input. Covers FR-1, FR-2, FR-16.

### J2 — Start and manually navigate connected rooms (Omar, using the fixed desk)

1. Omar searches History by name, opens a Lost object and selects Search.
2. In setup he chooses Gestures or PS4/PS5 controller, reads local control guidance and checks command/input/live-video readiness.
3. Start opens the required workspace split; target, locked mode and Searching are explicit. He releases any existing hold, then holds forward.
4. He follows setup guidance to keep people clear of the robot's path and search for visible targets on the floor or low shelves. He steers around stationary obstacles using the robot video while staying at the desk; releasing each direction stops movement.
5. **Climax:** He can continue the same search into another connected room without moving his workstation; video and controls remain visible.

Failure: unavailable required paths block Start; help/Retry never auto-starts. Lost recognition stops movement; actual required-path loss pauses into J5. Inactive mode cannot drive. Mapping/coverage/performance remain qualification gates, not a guaranteed outcome of this narrative. Covers FR-2–FR-5, FR-8, NFR-1–NFR-3, NFR-5.

### J3 — Review and confirm the intended belonging (Mariam, seeing a candidate)

1. A potential match appears with a bounding box; movement and AI matching stop automatically, leaving Paused.
2. Mariam sees the captured detection screenshot/box beside the reference; it is clearly separate from robot live video.
3. She explicitly selects Confirm match as Found after deciding it is her belonging.
4. **Climax:** Confirmation time and screenshot save, the object becomes Found and the session Ended; object detail shows the evidence without a second Stop action.

Failure: capture/save failure keeps movement disabled and does not show a false durable Found result; Retry or Stop stays available under the save/G3 rules. If already expired during this session, explain removal-at-end and return History after cleanup, without promising lasting evidence. Covers FR-9–FR-11.

### J4 — Reject a similar object and continue (Mariam, spotting another person's keys)

1. Candidate alert pauses movement/matching and opens evidence review.
2. Mariam compares the screenshot/reference and selects Reject.
3. Rejection/review time and screenshot save; object remains Lost and session Paused.
4. She chooses Resume, releases old input and makes a fresh hold to move.
5. **Climax:** The same continuously visible candidate does not immediately interrupt again; it becomes eligible only after leaving and re-entering view.

Failure: rejection save fails → remain Paused with unsaved decision and Retry; no silent Resume or suppression presented as persisted identity. New loss during review invokes J5 and does not discard evidence. Covers FR-9, FR-10, FR-12, FR-8.

### J5 — Emergency stop or required-connection recovery (Omar, during movement)

1. Omar activates Emergency stop, or the command path, selected input or live robot video is lost/frozen.
2. The system stops movement, pauses matching/session and identifies every known cause. A stale image is labeled Not live.
3. Omar restores required paths and explicitly acknowledges the interruption; an old held direction cannot clear it.
4. He chooses Resume only after readiness and any review decision are resolved, then releases/reapplies direction.
5. **Climax:** Operation resumes deliberately in the same locked mode/session, without surprise motion from reconnection or a held command.

Failure: unresolved cause keeps Resume unavailable with reason; a second cause remains visible and must be resolved. Omar may Stop session instead. Help is accessible without clearing recovery. Stop timing must pass physical SM-2, including loss-detection time. Covers FR-6, FR-7, FR-17 and S9 guidance.

### J6 — Pause, stop unsuccessful work and try again (Omar, after checking one room)

1. Omar selects Pause; movement and matching stop, while target/mode remain locked.
2. He either explicitly Resumes with fresh input or selects Stop session to finish the attempt.
3. Stop disables movement immediately and saves the unsuccessful Ended session; the object stays Lost.
4. **Climax:** Object detail contains the ended attempt and permits a new session on the same Lost record, including a newly selected mode.

Failure: save failure is explicit and stopped; no fake saved outcome. Stop during unresolved candidate review uses gate G3 rather than inventing a rejection. If the record has expired, it is removed at end and cannot start a new attempt. Covers FR-8, FR-10, FR-13, FR-15.

### J7 — Inspect local history after restart (Mariam, returning the next day)

1. Mariam restarts the application offline; expired records are cleaned before the feed appears.
2. She searches by object name, selects Lost/Found scope and opens object detail.
3. She opens a session and its saved confirmed/rejected screenshot and review time.
4. **Climax:** The unexpired registration, all sessions and decision evidence remain inspectable locally, with no account or upload.

Failure: no results offers Clear search; no sessions/decisions is distinct from read failure. Missing/corrupt evidence is labeled unavailable, not fabricated. Interrupted active-session recovery follows G2, rather than an assumed automatic restart/resume. Covers FR-13, FR-16, NFR-1, NFR-4.

### J8 — Search for a previously Found belonging again (Mariam, losing the keys another day)

1. Mariam opens the old Found record and sees its original evidence/time.
2. She chooses Register again, completes a fresh name/reference/region registration and saves.
3. **Climax:** A new independent Lost record is available for search while the unexpired original remains Found with its evidence.

Failure: cancelling/invalid new registration leaves the original untouched. No Reopen as Lost control exists. Expiry removes the old record on its own schedule, not based on the new registration. Covers FR-14, FR-1, FR-15.

### J9 — Configure retention and handle expiry (Omar, maintaining local records)

1. With no active session, Omar opens Retention settings and reads the default seven-day registration-based rule.
2. He proposes an allowed period; affected-record preview explains actual deletion and unchanged registration times.
3. He confirms and saves changes under the proposed R2 behavior, subject to gate G5.
4. **Climax:** The saved period and expiry results are clear; expired idle records and their related data are removed, while active/Paused grace still lasts only until Ended.

Failure: invalid period/save failure retains prior saved setting; deletion failure is reported without claiming erasure. During an active session settings are unavailable under IA2, and expiry-at-end is visibly explained. Covers FR-15, NFR-4.

### J10 — Handle interrupted capability without surprise movement (Omar, when the app loses focus)

1. Omar loses application focus or encounters unusable layout/AI/storage availability.
2. Proposed IN2/ST1/G1 behavior requests stop and Paused; the UI identifies the condition without marking the object Found.
3. On restoring availability he still needs the relevant acknowledgment, explicit Resume and fresh input; on process restart G2 must determine the durable session outcome.
4. **Climax:** Restoring the window or capability never silently restarts movement or invents a historical decision.

Failure: process loss cannot be handled by a live UI; architecture must ensure fail-safe stopping and agree G2 before implementation. This journey is an explicitly proposed extension, not a claim those open outcomes are approved. Covers proposed interruption/recovery and PRD section 8 gates.

## Requirement Coverage

This table traces the approved inventory without importing addendum proposals. “Covered” means specified here, not implemented, tested or accepted.

| Requirement (FR names verbatim; NFR descriptions summarized) | Surfaces / rules / journey |
| --- | --- |
| FR-1 — Register an object. | S2, Image selector/Field, J1/J8. |
| FR-2 — Select a search target. | S3/S4/S5, target lock and single-active guard, J1/J2/J6. |
| FR-3 — Show the search workspace. | S5, required split/readiness/live distinction, J2/J5. |
| FR-4 — Provide exclusive control modes. | S4/S5, mode lock through Paused, Input primitives, J2/J6. |
| FR-5 — Require held movement input. | Transition table, fresh hold/release, J2/J5. |
| FR-6 — Provide emergency stop. | Emergency stop/Recovery panel, J5. |
| FR-7 — Stop on required-input or video loss. | S5b, stale feed/cause/readiness rules, J5. |
| FR-8 — Control the session. | Session controls/transitions, no time cap, J2/J4/J6. |
| FR-9 — Suggest visually similar candidates. | Video panel/Evidence review, candidate language, J3/J4. |
| FR-10 — Pause for review. | S5a, stop before review, J3/J4/J6; G3 explicitly open. |
| FR-11 — Confirm a match. | S5a/S3/S7, durable Found+Ended evidence, J3/J7. |
| FR-12 — Reject a match. | S5a, Paused after rejection/suppression, J4/J7. |
| FR-13 — Preserve searchable history. | S1/S3/S7, local persistence/empty/error states, J7. |
| FR-14 — Register Found belongings again. | S3→S2, immutable original Found, J8. |
| FR-15 — Enforce configurable retention. | S8 and Local Data table, startup cleanup/active grace, J6/J9. |
| FR-16 — Use local access without login. | Launch/offline/privacy everywhere, J1/J7. |
| FR-17 — Require deliberate recovery. | S5b, acknowledgment/restoration/Resume/release-reapply, J5. |
| NFR-1 — Offline complete searching, including AI after setup. | Local runtime/resources; J1–J9; G1 cannot become a cloud dependency. |
| NFR-2 — Fixed-desk connected-room operation. | S5 visibility, J2; actual route must qualify. |
| NFR-3 — Windows team's laptop with dedicated NVIDIA GPU. | Foundation/Responsive & Platform, J2; exact equipment pending. |
| NFR-4 — Local retention-based persistence. | Local Data, J7/J9; partial writes not presented as saved. |
| NFR-5 — Stationary obstacles, people kept clear of the robot's path, visible floor/low-shelf targets. | S4 setup guidance and J2 operating instructions; no autonomous safety claim. |
| NFR-6 — Complete-system performance targets. | Qualification mapping below; no spec/mock establishes measured pass. |

| Metric | UX consequence / verification boundary |
| --- | --- |
| SM-1 | Candidate alerts/boxes and J3/J4; qualification needs five agreed objects × ten presentations, at least seven alerts per object within 3s. No UI-guaranteed detection. |
| SM-C1 | Potential-match wording/human decision; at most one alerted scene among ten distinct 10s dissimilar scenes, measured under frozen conditions. No confidence/identity promise. |
| SM-2 | Release/emergency/actual required loss stops wheels within 0.5s including detection; J2/J5 and both modes/directions must qualify. UI “paused” alone is not timing evidence. |
| SM-3 | No automatic duration cap; 20min full-system movement/video/AI/review/history endurance must be measured without recharge/restart/crash. |
| SM-4 | Live/stale video rules and J2/J5; camera event → display within 0.5s under movement+AI must be measured. Stale-detection threshold must fit SM-2 and actual path behavior. |

Acceptance trials freeze objects/references/placements/lighting/matching settings, avoid rejection-suppression contamination, and record failures. Qualification/report evidence is outside application navigation; this does not add an analytics/admin screen.

## Open Decisions and Handoff Gates

These are explicit limits to completeness: every approved feature has a surface/flow, but the PRD itself leaves the following outcomes/details for agreement. Proposed behavior supports review; it is not silently promoted to approval.

| Gate | Proposed resolution / required decision | Owner / timing |
| --- | --- | --- |
| G1 AI unavailable | [ASSUMPTION] Before Start, block searching with local diagnostic/Retry; during operation, stop+pause and require restoration/acknowledgment/Resume/fresh input. Decide AI failure's exact session/history outcome; no cloud fallback or autonomous manual-only continuation is implied. | Team; agree before implementation, qualify offline. |
| G2 Application interruption | [ASSUMPTION] Never auto-resume after restart; show interrupted-session recovery only from durably known facts. Decide Paused-versus-Ended outcome, interrupted evidence persistence and acknowledgment/restart flow. Architecture must stop on process/command failure independently of UI. | Team; agree before implementation and integration. |
| G3 Stop during unreviewed evidence | Stop must stop movement and end the unsuccessful session, leaving the object Lost. Decide whether/how unreviewed screenshot and event appear in history; proposed label “Not reviewed” is not a confirmed/rejected decision or new object/session state. Do not call Stop a rejection. | Team; agree before implementation. |
| G4 Input/image details | Choose gesture poses, controller mapping/stop gesture, recognition ambiguity policy, supported image formats/limits and keyboard target-selector mechanics. Local guidance must reflect actual mapping; both modes/actions/release and target validation must qualify. | Team UX/architecture; before functional testing. |
| G5 Retention settings | Agree allowed range/units, applying changes to existing registrations, cleanup-failure handling and affected-record confirmation. Proposed R2 applies saved changes immediately; immutable registration time and active grace always remain required. | Team; before settings implementation. |
| G6 Visual and accessibility handoff | Alisa provides branding; neutral tokens/layouts and accessibility behaviors are provisional. Confirm type/density/iconography/semantic colors, contrast, actual laptop scaling/minimum operation size. All S1–S9 are currently spine-only. | Alisa/team; before visual implementation/qualification. |
| G7 Equipment and measured system behavior | Exact laptop/Windows/GPU/webcam/controller, allowed hardware variants, communication arrangement, route and thresholds remain unqualified. Do not alter room-to-room scope or procure extras through UX. | Team with project supervisor; architecture, early integration and acceptance. |

The paired documents define a documentation handoff. They contain no application implementation, coded mocks or evidence that hardware targets passed.
