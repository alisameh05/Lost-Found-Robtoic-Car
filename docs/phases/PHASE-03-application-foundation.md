# Phase 03 — Application foundation and shared contracts

**Status:** Not started · **Depends on:** 02 · **Owner:** Frontend/backend team

## Goal and entry

Create the shared application structure before separate units diverge. Follow [AD-1/AD-2/AD-4/AD-12/AD-13](../ARCHITECTURE.md) and [TRD sections 3, 9–11](../TRD.md). Keep motors disabled throughout development.

## Work

- [ ] Scaffold Next.js/React/TypeScript with a local Node server and FastAPI with one authoritative backend worker. Keep AI and device adapters behind explicit interfaces.
- [ ] Define the TRD REST payloads/OpenAPI, event/frame schemas, revision scopes, failure occurrence IDs and controlling-client lease protocol; generate shared frontend types.
- [ ] Implement an initial Windows launcher and process health reporting. Build the single-owner guard for the data directory/devices; refuse a second backend owner.
- [ ] Bind both services to loopback; configure exact Host/origin allowlists, automatic capability bootstrap and protected WebSocket tickets without a login gate.
- [ ] Add clearly labeled device/storage/worker simulators for development. No simulator bypass may arm physical hardware or appear as a qualified real path.
- [ ] Create functional screen shells and the required left/right workspace, persistent emergency stop, stopped/pending/error states and readiness display. Keep branding provisional.
- [ ] Establish local diagnostics with identifiers/faults rather than secrets or raw media.

## Acceptance and evidence

The launcher opens the local interface; service/initialization/readiness are distinct. A second backend cannot take ownership. Unexpected origins/hosts or missing capabilities cannot mutate state or establish control channels. Shared schema examples agree between frontend/backend. No application account, cloud dependency or duplicate Next.js state owner is introduced.

**Save:** initial reproducible build, schema versions/examples, loopback/protection/owner-lock checks and screen-shell captures.

## Done and handoff

Done when the shared interfaces and protected local foundation are usable. Begin [04](PHASE-04-registration-and-persistence.md), [05](PHASE-05-camera-and-video-freshness.md), [06](PHASE-06-firmware-and-command-expiry.md) and [07](PHASE-07-gesture-and-controller-input.md) according to their own hardware entry gates.
