# Phase 15 — Fixed-desk multi-room readiness

**Status:** Not started · **Depends on:** 14 · **Owner:** Integration/vision team with supervisor

## Goal and entry

Stabilize the actual connected-room operation and freeze T3/T5/T6 qualification conditions. The operator remains at the fixed desk; the production release and full required services are active.

## Work

- [ ] Record the route's rooms/dimensions, floor/obstacle conditions, target locations and fixed desk. Keep people clear and targets visible on the floor/low shelves.
- [ ] Drive the actual robot through more than one room and measure command/video availability, dropouts and recovery. Early stationary probes are not a substitute.
- [ ] Recheck end-to-end stop/video behavior under movement and inference load; resolve network/queue/clock-age problems through the owning phase.
- [ ] Tune only the explicit open model, tracking, input and timing settings; record each change and keep within the adopted requirements.
- [ ] With the supervisor, freeze five objects/reference images, placements, lighting, negative-scene conditions, model/checkpoint and matching/continuity settings for Phase 16.
- [ ] Freeze the serial/camera/browser timing parameters, motor configuration, firmware/build and battery/network arrangement. Record conservative component budgets and physical timing observations.
- [ ] Prepare trial sheets and the available measurement method, including actual event/wheel and camera/display timing rather than UI timestamps alone.

## Acceptance and evidence

The production system supports the fixed-desk connected-room route and deliberate recovery with complete services active. Configuration and trial conditions are reproducible. A wired arrangement, if used under the existing allowance, still satisfies this same scope; an architecture-affecting change requires explicit revision. Do not silently replace a failed route with a same-room test.

**Save:** route/layout, integrated reliability/timing observations, frozen test-object/negative-scene set, configuration manifest and trial protocol.

## Done and handoff

Done when route readiness and the qualification baseline are established. Proceed to [Phase 16](PHASE-16-system-qualification.md). Formal pass/fail remains pending until its complete trial set is executed.
