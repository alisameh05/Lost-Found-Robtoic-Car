# Phase 16 — Whole-system qualification

**Status:** Not started · **Depends on:** 15 · **Owner:** Integration/evidence lead with component owners

## Goal and entry

Produce defensible acceptance results for every approved requirement on the frozen production system. Use [PRD section 7](../PRD.md) and [TRD section 12](../TRD.md). Earlier component/simulator tests support diagnosis but do not establish a whole-system pass.

## Work and acceptance

- [ ] **SM-1:** Run five agreed objects × ten clearly visible presentations. Each object needs at least seven alerts within three seconds. Record all fifty trials, including misses/late alerts; do not pass from an overall average alone.
- [ ] **SM-C1:** Run ten separate ten-second scenes without a visually similar target. At most one scene may contain any alert; count an alerted scene once. Use fresh presentations/sessions so suppression does not contaminate counts.
- [ ] **SM-2:** Measure actual event → wheels stopped, including detection, within 0.5 seconds. Cover each direction/release in both modes, emergency stop in both modes including the applicable UI/Circle paths, selected-input disconnect, command loss and disconnected/frozen/stale displayed video.
- [ ] **SM-3:** Run the complete system for twenty minutes without recharge, restart or crash while exercising movement, video, AI, review and history. Record battery/setup and every interruption.
- [ ] **SM-4:** Record an observable camera event and laptop display together; event → display must be within 0.5 seconds with movement/control and AI active.
- [ ] Execute the entire FR-1–FR-17 checklist: images/ROI, one target/session/mode lock, controls/recovery, review/suppression, human-only Found, unsuccessful-session reuse, new registration after Found, full history and actual retention deletion.
- [ ] Complete NFR-1–NFR-6, including internet-disconnected full operation, recorded Windows/NVIDIA equipment and fixed-desk searching in more than one room under the stated conditions.
- [ ] Inject browser/backend/worker loss, focus/visibility loss, expired leases, late frames/results, queued/replayed serial commands, multiple-client conflicts and repeated terminal actions. Verify no automatic restart or duplicate outcome.
- [ ] Test denied/full/corrupt storage, crash/restart/save-response-loss, expiry during active/Paused/review states, shortened/lengthened retention, purge interruption and cache clearing.
- [ ] Check loopback listeners, Host/origin/capability/ticket rejection, no login, media ownership/path protections, secrets/log handling and the approved UI/accessibility criteria.

## Evidence and failure handling

**Save:** release/configuration hashes, trial conditions, measurement method, raw results, relevant recordings/logs, requirement index and issue references. Keep passes, failures and unexecuted checks distinct. The tested release/configuration must match the evidence.

A failed target is a blocker, not a reason to delete the requirement. Repair through the owning phase and repeat affected tests; changes to model/reference/route/configuration require the affected qualification baseline and trials to be renewed. Any proposed scope/target revision needs explicit approval.

## Done and handoff

Done when all approved functional and non-functional acceptance criteria pass on the recorded complete system and no unresolved qualification blocker remains. Hand the passing release/evidence index to [Phase 17](PHASE-17-report-and-demonstration.md).
