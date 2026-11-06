# Phase 06 — Command firmware and expiry stopping

**Status:** Not started · **Depends on:** 01, 03 · **Owner:** Firmware/backend integration team

## Goal and entry

Implement the HC-05/Uno command path and independent command expiry before driving. Follow [TRD section 6.3](../TRD.md) and the reviewed T2 electrical plan. Use isolated/disabled motor power and observable output-state tests; physical wheel-stop qualification comes later.

## Work

- [ ] Establish the actual paired Windows serial connection and record device/firmware identity, protocol version and serial configuration.
- [ ] Implement a bounded nonblocking parser, framing/integrity/range checks, boot/control generations, increasing sequences and device-issued expiring challenges.
- [ ] Default motor outputs disabled on boot/reset. Ensure incomplete, invalid, oversized, replayed or expired packets cannot renew motion permission.
- [ ] Implement priority STOP and expiry; return boot/challenge/accepted-sequence/logical-output status without claiming sensed wheel telemetry.
- [ ] After T2 clears the sensor wiring, define bounded HC-SR04 distance/validity telemetry for the advisory warning. Invalid/missing readings are unknown, and sensor telemetry cannot command or inhibit motion.
- [ ] Distinguish ordinary release stopping from faults: a healthy Searching session may rearm for neutral then a new hold; emergency/expiry/path failures require the approved recovery gates.
- [ ] Kill the serial sender, break the link, stall an incomplete frame and deliver old/queued packets. Measure command-to-output/expiry behavior with motors isolated.
- [ ] With outputs disabled, probe serial reliability at route locations from the fixed desk and record T3 gaps.

## Acceptance and evidence

Fresh valid commands affect only the intended logical outputs. Boot/reset/loss/expiry forces disabled outputs without depending on browser or Python survival. A delayed packet never rearms a stopped old generation. Proximity telemetry, if carried on this link, remains advisory and cannot change motor outputs. Bench timing informs the T6 budget but is not an SM-2 wheel-stop pass.

**Save:** versioned firmware/protocol specification, exact tested parameters, parser/expiry/replay results, output timing and stationary serial coverage probes.

## Done and handoff

Done when the real serial protocol and disabled-output tests pass. Supply the adapter to [Phase 09](PHASE-09-session-and-safety-coordinator.md). No unrestricted wheel movement is introduced in this phase.
