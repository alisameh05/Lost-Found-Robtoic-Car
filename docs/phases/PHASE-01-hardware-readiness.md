# Phase 01 — Hardware review and preparation

**Status:** Not started · **Depends on:** 00 · **Owner:** Hardware/firmware team with supervisor

## Goal and entry

Resolve TRD **T2 before relevant procurement, assembly or energizing**. The prescribed list in [PRD section 6](../PRD.md) is authoritative; the workspace components PDF is not. This checklist contains no approved wiring or battery configuration.

## Work

- [ ] Identify exact chassis/motor, Uno, HC-05, ESP32-CAM and L298N variants and obtain their actual specifications.
- [ ] Check the four motors' required current, including startup/stall conditions, against the selected driver and thermal/power arrangement. Do not assume one driver safely supports every 4WD kit.
- [ ] Resolve cell count/configuration, holder, charger, BMS, regulator and switch compatibility within the prescribed quantities.
- [ ] Produce the power, grounding, logic-level, motor-disable/reset and wiring plan with the supervisor. Record connector/pin assignments only after review.
- [ ] Confirm how both boards will be programmed with the actual variants and allowed equipment, including connector/cable compatibility. Escalate any missing programming-access component instead of silently adding a purchase.
- [ ] Confirm the exact prescribed variants through the authorized procurement process; inspect received components before assembly.
- [ ] Prepare a bench arrangement with motor power/output disabled for camera and protocol development. Document the sequence for later controlled integration and how to stop/isolate the system.

## Acceptance and evidence

Supervisor-reviewed specifications and power/wiring/programming plan resolve T2 for the exact components used. Any incompatibility is a recorded blocker. Extra parts or scope changes require explicit authorization; no bench success establishes endurance or room coverage.

**Save:** variant/specification inventory, compatibility checks, reviewed wiring/power plan, programming method, assembly inspection and open conflicts.

## Done and handoff

Done when the relevant hardware plan is cleared and available parts match it. Hand off motor-disabled equipment to [Phase 05](PHASE-05-camera-and-video-freshness.md) and [Phase 06](PHASE-06-firmware-and-command-expiry.md). Revisit this phase if the actual variants change.
