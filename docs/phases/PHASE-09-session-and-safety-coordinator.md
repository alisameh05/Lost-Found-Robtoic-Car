# Phase 09 — Session and safety orchestration

**Status:** Not started · **Depends on:** 04, 05, 06, 07, 08 · **Owner:** Backend/integration team

## Goal and entry

Integrate FR-2–FR-8/FR-17 while motor power remains disabled. The backend is the single authority, using [TRD sections 3/5/6/9](../TRD.md). Do not create a production manual-only mode to bypass unavailable AI.

## Work

- [ ] Implement Searching/Paused/Ended, one active session including Paused, immutable target/mode, and atomic Start guards for an eligible Lost record.
- [ ] Require healthy storage/AI, selected input, command path, fresh acquired/displayed video and operational workspace before Start/Resume or movement permission.
- [ ] Implement the controlling-browser lease, generations, ordered snapshots/events and failure occurrence IDs. Reconnect/snapshot recovery never implicitly starts/resumes.
- [ ] Implement held input and ordinary stop/rearm, plus immediate stop/Pause, emergency stop, AI/storage/path loss, hidden tab/focus loss and browser/backend interruption behavior.
- [ ] Enforce restoration, acknowledgment of current failures, explicit Resume and neutral/reapply before post-fault motion. Pending review also prevents Resume.
- [ ] Route candidate alerts through immediate permission revocation before any review/media work. Ignore wrong-generation/Paused/Ended candidate results.
- [ ] Keep disk/inference/render work off the stopping path. Measure bench/capture/display/command components and record initial exact T6 timing configuration with a reserved mechanical-stop budget.

## Acceptance and evidence

Deterministic transition tests and integrated motor-disabled traces show no dual session, mixed-mode command, automatic recovery or stale rearm. Backend/worker/UI/storage stalls cannot prevent command expiry. Emergency stop revokes permission despite stale ordinary revisions or an absent/expired control lease, with valid local request protection retained.

**Save:** transition/readiness matrix, lease/failure/epoch tests, integrated traces and initial timing-budget/configuration record. Physical SM-2 remains pending.

## Done and handoff

Done when the actual adapters and worker participate in the guarded stationary flow. Continue [Phase 10](PHASE-10-review-and-history.md). No floor driving occurs yet; Phase 12 also requires completed evidence and retention/restart behavior.
