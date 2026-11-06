# Phase 01 — Hardware review and preparation

**Status:** Not started · **Depends on:** 00 · **Owner:** Hardware/firmware team with supervisor

## Goal and entry

Resolve TRD **T2 before wiring or energizing**. The owner-confirmed purchased inventory in [PRD section 6](../PRD.md) is authoritative; the supplied components PDF and photos are product references, not wiring instructions. No electrical configuration is approved yet.

## Work

- [ ] Identify exact chassis/motor, Uno, HC-05, ESP32-CAM and L298N variants and obtain their actual specifications.
- [ ] Reconcile the purchased inventory: two-layer MDF 4WD chassis; four assumed-identical 3–12 V, 450 RPM dual-shaft motors; L298 module; Uno; ESP32-CAM OV2640/CH340; HC-05; HC-SR04/holder; three active 1200 mAh 18650 cells plus three spares; 3-cell holder; 3S 10 A BMS; TG-008 two-bay charger plus one single-bay charger; 7805 marked 5 V/100 mA; and 3-pin rocker switch. Record the single-bay charger's model/output and other uncertain labels rather than guessing.
- [ ] Select the left motor pair for one L298 channel and the right pair for the other. Before wiring/powering that arrangement, verify the combined startup/stall current and thermal limits of each channel and the actual module. A running-current figure alone does not close this check.
- [ ] Implement the selected removable-cell charging procedure after compatibility review: disconnect power and remove all cells from the holder; charge two using the TG-008 and one using the single-bay charger only if their actual specifications permit independent charging of these cells at compatible currents. Neither charger connects to the assembled 3S pack. Verify cell chemistry/discharge/charge ratings, identify matched active/spare cell sets and review holder cell-junction access for the 3S BMS before use.
- [ ] Compare the pictured 7805 5 V/100 mA regulator with all board loads. If it is inadequate, obtain supervisor approval for a suitable power-component change before procurement; do not treat it as the originally planned DC-DC regulator.
- [ ] Record the listed resistor inventory, including the extra 0.22 Ω and 1 Ω parts, as unassigned. Do not include them in wiring until their actual values and a reviewed use are established.
- [ ] Mount the HC-SR04 facing forward and resolve its pin/power/telemetry arrangement. Calibrate separate warning and clear distances at the selected indoor speed to prevent flicker. Keep the warning silent and visual only; invalid readings are unavailable. It never stops, pauses or steers the robot.
- [ ] Produce the power, grounding, logic-level, motor-disable/reset and wiring plan with the supervisor. Use the breadboard for suitable signal circuits; route battery/motor current through connections rated for the actual current. Use the stock resistors only where a calculated, reviewed circuit needs them. Record connector/pin assignments only after review.
- [ ] Confirm the Uno's USB-B cable compatibility and that the ESP32-CAM's CH340 programming hardware/base is actually present and compatible; a listing title alone does not prove the base is included. Verify both programming methods. Escalate missing equipment instead of silently adding a purchase.
- [ ] Inspect received components against the owner-confirmed inventory. No further purchase or replacement is authorized unless the supervisor approves it.
- [ ] After T2 is cleared, assemble the chassis and connect the approved wiring/power arrangement. Keep motor power disconnected and motor outputs disabled; inspect the assembly against the reviewed plan.
- [ ] Prepare a bench arrangement with motor power/output disabled for camera and protocol development. Document the sequence for later controlled integration and how to stop/isolate the system.

## Acceptance and evidence

Supervisor-reviewed specifications and power/wiring/programming plan resolve T2 for the exact components used; the physical assembly matches and has been inspected against that plan, with motor power/output disabled. Battery charging, regulator-load, motor/driver-current and logic/wiring compatibility remain blockers until evidence closes them. Any incompatibility is escalated for an approved change; no bench success establishes endurance or room coverage.

**Save:** variant/specification inventory, compatibility checks, reviewed wiring/power plan, programming method, assembly inspection and open conflicts.

## Done and handoff

Done when the reviewed hardware plan is cleared, available parts match it, and the physical assembly has been inspected while motor power/output remains disabled. Photo identification alone does not close T2. Hand off assembled motor-disabled equipment to [Phase 05](PHASE-05-camera-and-video-freshness.md) and [Phase 06](PHASE-06-firmware-and-command-expiry.md). Revisit this phase if the actual variants change.
