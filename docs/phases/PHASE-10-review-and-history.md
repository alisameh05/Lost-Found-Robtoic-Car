# Phase 10 — Match review, evidence and full history

**Status:** Not started · **Depends on:** 09 · **Owner:** Backend/data and frontend team

## Goal and entry

Complete FR-10–FR-14 using [TRD sections 5/7/8/9](../TRD.md). Captured evidence is distinct from live video. Human confirmation alone establishes Found.

## Work

- [ ] Complete the modeless review panel with the exact detection screenshot/box, reference comparison and Confirm/Reject/Stop actions, retaining emergency-stop access.
- [ ] Prepare durable evidence through the storage journal before committing review outcomes; track generated files across failures/crashes.
- [ ] Atomically commit Confirmed/time + Found/time + Ended session and receipt; a repeated action returns its committed result without a duplicate outcome.
- [ ] Commit rejection/time/evidence while retaining Lost and Paused. Resume is separate and preserves suppression context from Phase 08.
- [ ] Stop an unresolved review as Ended/Lost with saved Not reviewed evidence, never as a fabricated rejection. Serialize Confirm/Stop races so only one terminal outcome wins.
- [ ] Complete object/session histories, name search, ordered review entries and read-only evidence inspection. Show missing/corrupt media explicitly.
- [ ] Allow another search of an unsuccessful Lost record. A Found belonging must create a separate registration; do not reopen its old record.

## Acceptance and evidence

Committed outcomes/evidence survive restart and response loss. Inject file/transaction failure: movement remains disabled and unsaved actions are not shown as successful. Held input cannot continue during review or saving. Confirm/Reject/Stop, racing requests and retries produce one consistent historical result.

**Save:** end-to-end review cases, crash/response-loss/retry results, history screenshots and data/media consistency checks.

## Done and handoff

Done when full review/history works on unexpired records. Continue [Phase 11](PHASE-11-retention-and-crash-recovery.md), including startup reconciliation and expiry during these same workflows.
