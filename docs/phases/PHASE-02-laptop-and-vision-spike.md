# Phase 02 — Laptop environment and vision feasibility

**Status:** Not started · **Depends on:** 00 · **Owner:** Backend/vision team

## Goal and entry

Expose compatibility and reference-matching risks before building the full application. Implement the early checkpoints of TRD **T1/T3/T5** on the intended Windows laptop. Hardware may still be in preparation; clearly labeled sample images/video can support the initial spike.

## Work

- [ ] Record the actual laptop/Windows, GPU/driver, webcam, browser, existing Bluetooth/Wi-Fi capability and access to PS4/PS5 devices.
- [ ] Select a supported, mutually compatible Node/Next.js/React/TypeScript and Python/FastAPI/vision/input package combination using current primary documentation. Record versions and installation steps; do not assume the newest package fits every dependency.
- [ ] Run local MediaPipe hand-landmark and webcam smoke checks; verify controller enumeration and serial-library availability where devices are available.
- [ ] Exercise YOLOE visual prompting from a selected reference region against sample frames using the intended local PyTorch/GPU runtime. Record candidate boxes, misses and resource/timing observations.
- [ ] Download required models/assets during setup, record hashes/notices and rerun the spike with internet disconnected.
- [ ] Record feasible checkpoint/configuration candidates and failures. Leave the final five objects, thresholds and qualification freeze to Phases 08/15.

## Acceptance and evidence

A reproducible candidate environment runs local reference prompting and landmarks on the intended laptop offline after setup. Exact versions and known gaps are recorded. Sample-image success does not pass SM-1/SM-C1, actual-camera latency or the twenty-minute system target. Unavailable equipment is a T3 blocker, not assumed support.

**Save:** machine inventory, initial dependency/model manifest, setup steps, offline smoke results and vision observations.

## Done and handoff

Done when the basic selected stack is feasible and reproducible, or a blocking incompatibility has been explicitly resolved. Start [Phase 03](PHASE-03-application-foundation.md). Carry the candidate environment into [Phase 08](PHASE-08-local-matching-worker.md); finalize release compatibility in Phase 14.
