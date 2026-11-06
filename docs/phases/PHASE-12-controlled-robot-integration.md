# Phase 12 — Controlled physical integration

**Status:** Not started · **Depends on:** 09, 10, 11 · **Owner:** Integration/hardware team

## Goal and entry

Introduce physical wheel movement through the complete guarded application. Confirm T2 clearance, actual firmware/parts, T4 mappings, usable operational controls and initial exact T6 parameters before enabling motor power. Use the reviewed hardware arrangement and keep people clear of the path.

## Work

- [ ] Inspect the assembled power/wiring/programming arrangement against Phase 01 and confirm reset/disabled-output behavior before energizing motors.
- [ ] Start with a securely restrained setup/wheels clear of the floor under the reviewed procedure. Verify motor direction, logical stop and physical stopping before floor operation.
- [ ] Check the approved left/right motor-pair arrangement for startup current and module heating using the supervisor-approved procedure. Begin with the selected low indoor speed; PWM settings alone do not establish current compatibility. Record the result before floor progression.
- [ ] Start real app sessions only with AI/storage, selected input, acquired/displayed video, command path and workspace ready. Do not bypass a required service to make the robot move.
- [ ] Measure release/emergency/required-path-loss stopping in the controlled setup; include stale queued commands, application termination and frozen video. A failed stopping case blocks floor progression until fixed.
- [ ] Progress to the agreed clear floor test area with stationary obstacles and available emergency controls. Exercise held directions and release in gesture and PS4 DualShock 4 sessions.
- [ ] Calibrate and exercise the HC-SR04 warning threshold/clear condition. Confirm the silent warning never stops, pauses or steers the robot and never labels missing/invalid sensor data as clear.
- [ ] Integrate actual candidate stop/review, rejection/Resume/suppression and confirmation/end/history. Test the PS4 profile and gesture mode with live input/video/inference load.
- [ ] Verify fault recovery requires acknowledgment/restoration/Resume/neutral-reapply; ordinary input release can continue within healthy Searching on a new hold.

## Acceptance and evidence

The complete app drives only when permitted and does not move in Paused/Ended, review, saving failure or fault recovery. Measured controlled physical stopping meets SM-2 under the tested configuration; record every case and limitation. This initial result is not final route/release/endurance qualification.

**Save:** assembly inspection, actual build/configuration, direction and wheel-stop timing, integrated workflow/failure results and issues.

## Done and handoff

Done when controlled physical integration is repeatable with no unresolved stopping/readiness blocker. Combine with [Phase 13](PHASE-13-ux-and-visual-handoff.md) for [Phase 14](PHASE-14-offline-release.md). Revisit the relevant earlier phase if any hardware or software assumption fails.
