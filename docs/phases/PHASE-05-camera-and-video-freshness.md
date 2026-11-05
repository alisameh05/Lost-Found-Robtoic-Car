# Phase 05 — Camera streaming and video freshness

**Status:** Not started · **Depends on:** 01, 03 · **Owner:** Camera firmware, backend and frontend team

## Goal and entry

Build the actual ESP32-CAM → local Wi-Fi → backend → browser path required by FR-3/FR-7. Follow [TRD sections 6.2/9](../TRD.md). Use cleared camera power/programming arrangements and disabled motor outputs.

## Work

- [ ] Program the selected camera variant and join the approved existing protected network; record firmware/endpoint configuration without exposing secrets.
- [ ] Preserve camera boot/stream epoch, acquisition sequence/timestamp and a bounded clock-age/uncertainty exchange. Receipt time or pixel similarity alone is insufficient freshness proof.
- [ ] Ingest/decode through bounded latest-frame queues and carry metadata through backend delivery. Do not accumulate stale frames under load.
- [ ] Implement the TRD binary frame channel and browser decode/draw acknowledgments. Keep robot and webcam source IDs distinct.
- [ ] Show live, initializing, disconnected, stale/frozen and captured-evidence states correctly. Never overlay a candidate box on a different frame.
- [ ] Disconnect/freeze the source, repeat old metadata, restart the camera and stop browser display acknowledgments while its connection stays open; expose each loss to the safety interface.
- [ ] With motors disabled, probe video availability at route locations from the intended fixed desk; record gaps for T3/T6.

## Acceptance and evidence

Actual camera frames display with preserved identity and conservative capture/display freshness information. Lost/uncertain freshness cannot remain labeled Live. Camera epoch changes invalidate prior timing estimates. Initial scene-to-display measurements identify latency risks; final SM-4 requires the complete release with movement and AI active.

**Save:** camera firmware/configuration IDs, frame-schema examples, freshness fault results, initial timing traces and stationary route probes.

## Done and handoff

Done when the real path and its failure signals work. Hand off frames to [Phase 08](PHASE-08-local-matching-worker.md) and readiness/freshness to [Phase 09](PHASE-09-session-and-safety-coordinator.md). Do not claim multi-room moving operation or SM-4 yet.
