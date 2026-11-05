# Phase 13 — UX completion and visual handoff

**Status:** Not started · **Depends on:** 03, 10, 11 · **Owner:** Frontend team with Alisa

## Goal and entry

Complete the actual screens and resolve the visual portion of T7 using [TRD section 4](../TRD.md) and the UX documents linked in the [guide](../IMPLEMENTATION_GUIDE.md). Can overlap Phase 12; functional emergency controls and readable video must already exist before driving.

## Work

- [ ] Obtain Alisa's branding/type/color/icon/density decisions before treating provisional visual tokens as approved. Select no new UI framework by implication.
- [ ] Complete History, registration/ROI, object/session details, setup/readiness, workspace, evidence review, recovery, retention settings and connection/control guidance.
- [ ] Preserve the left webcam/gesture panel and right robot-video/AI panel; distinguish Live, Not live and Captured evidence and separate object status from session state.
- [ ] Keep emergency stop reachable during help, review, pending saves and recovery. Verify navigation/focus/visibility behavior and explicit return without automatic Resume.
- [ ] Implement loading, empty, denied, missing media, stale revision and save/cleanup failure states without losing valid input or inventing success.
- [ ] Verify the adopted keyboard ROI selector. Agree the remaining proposed accessibility goals under T7, then test keyboard/focus/status announcements, contrast, scaling/reflow and text enlargement as approved.
- [ ] Record actual laptop scaling/minimum usable operational layout; an unusable layout must revoke motion, not hide required controls/video.

## Acceptance and evidence

Every required task is operable on the intended Windows/browser setup. Controller mode does not require an inactive webcam. UI state matches backend facts; visual polish cannot alter human confirmation, retention or recovery behavior. Provisional accessibility goals are not reported as approved/passed before T7 review.

**Save:** visual approval decisions, screen/state inventory, keyboard/ROI/scaling/contrast checks and operational-layout results.

## Done and handoff

Done when the functional UX and applicable visual/accessibility decisions are approved and checked, or any remaining visual item is explicitly accepted as a documented pending handoff. Do not silently choose branding. Proceed to [Phase 14](PHASE-14-offline-release.md) only when its required UI is usable.
