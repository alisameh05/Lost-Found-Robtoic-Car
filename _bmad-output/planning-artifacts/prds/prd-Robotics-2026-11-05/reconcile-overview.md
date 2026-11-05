# Reconciliation — original overview

Reviewed 2026-11-05 against `prd.md` version 1.0-review and `addendum.md`. Source: user-pasted Lost and Found overview, extracted earlier from the attachment; existing source extract used. This is a requirements/source review, not implementation or feasibility verification.

## Verdict

The draft preserves the concept and explicit scope exclusions. Most changes are deliberate interview refinements. One evidence-lifecycle detail is less explicit than the overview and merits a small clarification.

## Coverage

| Source intent | Destination | Disposition |
| --- | --- | --- |
| Four-wheel camera robot plus laptop application; manually locate belongings | PRD §§1–2, 4.2, 6 | Captured. |
| Gesture primary control, PS4/PS5 fallback; five movement actions | FR-4/FR-5; addendum operational trade-offs | Both modes/actions retained. Primary/fallback preference need not establish automatic switching. |
| Split-screen laptop webcam/robot feed; AI bounding boxes | FR-3/FR-9 | Captured. |
| Upload reference and select target region | FR-1/FR-2 | Captured. |
| Start search; manual driving with AI checking robot frames | FR-8/FR-9 | Captured as capability without binding frame-processing implementation. |
| Notification, bounding box, screenshot, confirm/reject, Found only on human confirmation | FR-9–FR-13 | Core behavior captured; see screenshot-lifecycle clarification below. |
| Feed with name/reference/status/registration time/evidence/confirmation time; searchable history | FR-11/FR-13 | Captured and expanded to sessions/rejections by interview. |
| Pause/resume/stop, connection status, emergency stop, timeout-based stop | FR-3, FR-6–FR-8, FR-17, SM-2 | Captured with explicit failure/recovery and timing targets selected during interview. |
| Wireless preference, Arduino/HC-05/L298N, example ESP32-CAM | PRD §6 component list; NFR-2; addendum hardware | User's later hardware list governs; wired demonstration allowance is explicit. Compatibility is not asserted. |
| Candidate Python/OpenCV/MediaPipe/YOLOE/Pygame/Arduino IDE/local storage | Addendum software proposals | Captured as proposals, preserving PRD capability focus. |
| No retrieval/autonomous navigation/ultrasonic detection/GPS/mapping | PRD §6; addendum | Captured; servo functions also excluded by interview. |

## Intentional changes established by interview

- The overview allowed switching control modes during searching. The later decision locks mode selection until session end (FR-4).
- Potential-match review now stops movement and pauses matching. Rejection leaves the session paused until Resume; confirmation ends it (FR-10–FR-12).
- The feed is local history, not a public social service (FR-13/FR-16). This makes the overview's social-feed comparison a presentation analogy.
- Windows/offline runtime, fixed-desk connected-room search, held movement input, registration-based seven-day default retention, and new registration after Found are interview additions.
- No separate model training is made a user requirement: software mechanisms remain proposed in the addendum, while similarity/human confirmation remain explicit.

## Clarification

**Evidence for an unreviewed candidate:** the overview explicitly says to capture and save a screenshot when a potential match is detected. FR-10 provides screenshot review, FR-11 saves confirmed evidence, and FR-13 persists confirmed/rejected matches. The case where the operator presses Stop during review without confirming/rejecting does not explicitly establish whether that candidate screenshot persists. State capture at alert time and the intended retention of an unreviewed candidate, or record any deliberate narrowing. This is a small evidence-lifecycle gap, not a change to the matching or confirmation rules.

No other substantive source gap found. Source intent is preserved without importing the rejected workspace hardware PDF.
