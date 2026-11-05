# Phase 11 — Retention and crash recovery

**Status:** Not started · **Depends on:** 10 · **Owner:** Backend/data team with frontend settings/recovery

## Goal and entry

Complete FR-15 and durable interruption handling using [AD-6/AD-9](../ARCHITECTURE.md) and [TRD sections 5/8](../TRD.md). Cover actual files, not only feed entries.

## Work

- [ ] Implement default seven-day retention, configurable 1–30 whole days from immutable registration time, with impact preview/revision/confirmation and immediate application to existing records.
- [ ] Block retention-setting changes during Searching/Paused. A new search never extends expiry; independent registration does not change the active target.
- [ ] Schedule runtime expiry, re-evaluate on settings/time/wake/session-end changes, and deny expired non-grace data on all object/media/API paths.
- [ ] Preserve Searching/Paused grace, including review/evidence, until that existing session ends. Then remove eligible data without allowing another search.
- [ ] Implement durable purge operations: hide eligible records, delete every owned image/staging copy, cascade related rows/receipts, then finish the operation. Recover idempotently after interruption.
- [ ] On startup, reconcile storage, end unfinished sessions as Interrupted, preserve committed Found/reviews and purge expired data before exposing history/search. Never fabricate uncommitted evidence or Resume.
- [ ] Handle storage-full/denied/corrupt/cleanup failures visibly; stop/pause active operation and block unsafe new data tasks while preserving safety controls and repair paths.
- [ ] Clear expired browser media and temporary URLs; exclude evidence from persistent browser/Next.js caches and untracked backups.

## Acceptance and evidence

Exercise startup/runtime expiry, shorter/longer settings, grace during Searching/Paused/review, session-end purge and crashes at each staging/purge boundary. Inspect database and filesystem results. Cleanup failure never claims deletion complete; restart never replays motion or changes an unconfirmed Lost record to Found.

**Save:** retention matrix, before/after owned-file/row inventory, crash-recovery outcomes, interrupted-history and cache-clear evidence.

## Done and handoff

Done when complete data lifecycle/recovery works. The stationary application now supports all required business outcomes. Proceed to [Phase 12](PHASE-12-controlled-robot-integration.md) only after its hardware, input and timing entry checks; [Phase 13](PHASE-13-ux-and-visual-handoff.md) can also progress.
