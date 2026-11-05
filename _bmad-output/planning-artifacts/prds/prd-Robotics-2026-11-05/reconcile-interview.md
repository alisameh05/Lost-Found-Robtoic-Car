# Reconciliation — interview and decision log

Reviewed 2026-11-05 against `prd.md` version 1.0-review, `addendum.md`, and the append-only `.memlog.md`. Interview decisions were checked from their logged round summaries; no user decision was inferred from the rejected PDF or research context. This is an artifact-consistency audit, not an independent replay of the chat or performance qualification.

## Verdict

All eight interview-round decision summaries have a clear destination. No conflicting requirement was found. Approval remains pending as intended; deferred design/qualification details have owners and revisit gates.

## Decision disposition

| Logged decision or event | Destination/status |
| --- | --- |
| MCQ interview; clarify assumptions; no code; save approved docs/PRD.md | PRD purpose/approval; draft status; workflow behavior. MCQ format belongs to interview history, not runtime requirements. |
| Round 1: university report/demo, offices/shared spaces, complete laptop/robot system, guided feature-first interview | PRD §§1–2; workflow choice retained in memlog, not product scope. |
| Round 2: all overview features in MVP, similarity plus human decision, floors/low shelves, connected rooms, one operator/laptop/robot/target, no hardware purchased | PRD §§1–2, 4, 6; FR-2/FR-9. |
| Round 3: preselected mode locked during session; held input; local Wi-Fi; stop on command/input/video loss; pause on candidate | FR-4–FR-7, FR-10; PRD §2; NFR-1. |
| Round 4: fixed desk; wired demo allowed; offline AI; Pause stops motion/AI; Resume same search; rejection paused; no duration limit | PRD §2; FR-8/FR-12; NFR-1/NFR-2; addendum operational trade-offs. |
| Round 5: required registration fields; confirm saves/effects Found/end; re-register Found item; sessions and confirmed/rejected evidence; configurable deletion; no login | FR-1, FR-11, FR-13–FR-16. |
| Round 6: seven-day default retention; Windows/NVIDIA GPU; demo 3–6 weeks; prescribed purchases only; stationary furnished-room conditions | PRD §§2, 6, 8; FR-15; NFR-3/NFR-5. |
| Round 7: five objects; seven of ten per-object alerts within three seconds; false-alert countermeasure; 0.5-second stop/video targets; twenty-minute system runtime | PRD §7 SM-1, SM-C1, SM-2–SM-4 plus protocols. Selected targets are explicitly unmeasured. |
| PDF inspection event | Set aside as non-authoritative; provenance retained in prior extract and addendum. Its quantities, servo/sensor, prices do not govern requirements. |
| Round 8: authoritative 16-line hardware list and quantity ranges | PRD §6 table matches all logged names/quantities; technical unresolved details in addendum/§8. |
| Round 8: exclude servo/ultrasonic; acknowledgment/restoration/Resume/fresh input; rejection suppression; registration-based whole-record expiry with active-session exception; Stop saves/ends Lost session that can be retried | PRD §6; FR-12, FR-15, FR-17, FR-2/FR-8; addendum trade-offs. |
| Draft-assembly event | Current PRD has 17 FRs, 6 NFRs, explicit metrics/hardware/non-goals/deferred gates. It makes no implementation or qualification claim. |

## Important interpretation checks

- Wired operation does not waive the fixed-desk, multiple-room requirement; PRD says so in both operating boundary and acceptance protocol.
- No hardware performance or compatibility is inferred from component inclusion.
- The later hardware list replaces the rejected PDF as source authority; no ultrasonic or servo requirement was retained accidentally.
- Mode switching in the original overview is superseded by the explicit lock-through-session interview answer.
- All stored record/history/evidence data expire together from registration, with an active-session exception and no auto-duration limit; the addendum calls out that this can extend retention while active.
- No login means local laptop access, not a claim of user isolation or public sharing.

## Gaps and remaining gates

No substantive interview-decision omission found. The original-overview screenshot-on-alert detail has a narrow unreviewed-candidate lifecycle ambiguity recorded in `reconcile-overview.md`.

The PRD accurately leaves exact assessment date, machine/controller variants, hardware architecture, route/object test set, and mappings/settings for named later gates. These are neither approval of an architecture nor proof that acceptance is achievable. User approval is still required before final status and `docs/PRD.md` publication.
