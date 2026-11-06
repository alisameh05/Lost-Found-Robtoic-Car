# Phase 07 — Gesture and controller input

**Status:** Not started · **Depends on:** 03 · **Owner:** Input/backend team with frontend guidance

## Goal and entry

Implement the adopted held-input mappings and fresh/neutral sample semantics for FR-4/FR-5/FR-17. Follow [AD-10](../ARCHITECTURE.md) and [TRD section 6.1](../TRD.md). Keep physical motor outputs disabled; record actual device availability under T3.

## Work

- [ ] Capture the selected laptop webcam through the backend and derive pointing direction from MediaPipe hand landmarks.
- [ ] Verify mirrored displayed coordinates: one extended index finger up/down/left/right means forward/backward/left/right. Closed fist, no hand, multiple hands or ambiguity means ordinary stop.
- [ ] Select and record recognition, ambiguity and neutral/reapply thresholds from local tests; no guessed confidence value becomes an approved default.
- [ ] Implement Pygame polling/hotplug for the actual PS4 DualShock 4 profile: held D-pad direction moves, release/conflict stops, Circle triggers emergency stop.
- [ ] Emit timestamped samples with device identity/generation, validity, direction/neutral and disconnection causes. Do not silently substitute another controller.
- [ ] Keep polling independent of browser foreground behavior; the coordinator will separately enforce visible/focused workspace eligibility.
- [ ] Build local mapping/readiness guidance. A missing inactive webcam/controller must not block the selected mode; selected gesture webcam failure must be observable.

## Acceptance and evidence

Every approved direction, release, conflict and invalid gesture is correctly represented without motor movement. Disconnects invalidate old samples. The PS4 DualShock 4 uses a verified profile rather than guessed button numbers. A held pre-failure input cannot masquerade as neutral then a new hold. Unavailable required hardware prevents completion, although simulator work can continue.

**Save:** device/profile inventory, mirrored-direction checks, threshold rationale/results, input/disconnect traces and guidance captures.

## Done and handoff

Done when T4's initial input configuration and mappings pass on the required devices. Supply samples/emergency signals to [Phase 09](PHASE-09-session-and-safety-coordinator.md). Measure physical release-to-stop later in Phases 12/16.
