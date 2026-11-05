# Phase 08 — Local matching and continuity worker

**Status:** Not started · **Depends on:** 02, 04, 05 · **Owner:** Vision/backend team

## Goal and entry

Implement FR-9's reference-image candidates without granting AI ownership of motion or Found status. Follow [AD-8/AD-13](../ARCHITECTURE.md) and [TRD sections 3/5/6](../TRD.md). Development can start on recorded frames after 02/04; completion requires the actual Phase 05 stream.

## Work

- [ ] Run YOLOE visual prompting through the selected local Ultralytics/PyTorch environment in a separate worker process.
- [ ] Prepare a prompt from the stored orientation-normalized reference/ROI; validate it against the original dimensions. Keep object-derived prompt caches session-scoped and clear them when no longer eligible.
- [ ] Consume bounded latest eligible frames with session/generation/reference/frame identifiers and freshness metadata.
- [ ] Return candidate boxes and exact detection-frame references; never modify domain rows or send motor commands.
- [ ] Implement session-level rejected-candidate continuity observations and distinguish them from new matching results. Matching/alerts stop in Paused; continuity-only observations cannot create candidates or authorize movement.
- [ ] Preserve suppression across pause/recovery. Uncertain continuity is not observed exit and does not add an absent-view prerequisite to Resume.
- [ ] Exercise worker crash, missing/corrupt assets, overload and late results. Record candidate checkpoint/association/exit settings for T5; final freeze occurs in Phase 15.

## Acceptance and evidence

Actual camera frames generate locally computed, frame-tagged similarity candidates and boxes; no internet inference is required. Stale/wrong-session outputs can be rejected by the coordinator. A slow/dead worker cannot block safety processing. Demonstrate continuous-view suppression and observed exit/re-entry on development cases without claiming unique identity or a final detection score.

**Save:** worker interface, checkpoint/package hashes, offline runs, initial misses/false alerts, continuity cases and overload/crash traces.

## Done and handoff

Done when the real worker and candidate/continuity contract integrate. Hand off to [Phase 09](PHASE-09-session-and-safety-coordinator.md) and [Phase 10](PHASE-10-review-and-history.md). SM-1/SM-C1 remain pending until frozen-condition system trials.
