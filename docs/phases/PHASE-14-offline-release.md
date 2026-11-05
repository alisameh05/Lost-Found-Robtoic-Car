# Phase 14 — Offline production release

**Status:** Not started · **Depends on:** 12, 13 · **Owner:** Integration/release team

## Goal and entry

Create the actual release that will be qualified and demonstrated. Follow [AD-4/AD-12](../ARCHITECTURE.md) and [TRD sections 10/11](../TRD.md). This is a local Windows release, with both the Next.js Node server and FastAPI.

## Work

- [ ] Build the production frontend, pin the supported Node/Python/package environment, and include all required local models/fonts/assets and schema/firmware versions.
- [ ] Finish the Windows launcher: ownership lock, startup reconciliation/purge, component diagnostics, browser opening, orderly stop-first shutdown and failure reporting.
- [ ] Keep one backend worker and no release reload. Missing/corrupt dependencies or assets leave the app disarmed with an actionable reason.
- [ ] Configure exact loopback ports/origins, protected bootstrap/tickets and local device endpoints. Check that no public listener, hosted script/font or cloud inference is required.
- [ ] Install/reproduce the release in a clean documented location on the supported laptop; keep data in the Windows-user local root, outside the build/source tree.
- [ ] Disconnect internet and cold-start; exercise registration, actual video/input, local matching, review/history and restart. Local Wi-Fi remains available.
- [ ] Verify upgrades/migration/recovery without silently recreating records or leaving untracked retention-bypassing copies.
- [ ] Generate the release manifest with all relevant versions, hashes, device profiles and timing/model configuration; record setup and operation instructions.

## Acceptance and evidence

The production launcher starts both local services offline after setup, with no development server or account/login gate. Normal operations need no internet downloads. Process failure/shutdown cannot auto-resume motion. The release is reproducible from its manifest, with actual firmware/model/configuration identity.

**Save:** release package/manifest, installation/run instructions, cold-start/offline test results and migration/shutdown checks.

## Done and handoff

Done when T1's release lock and offline deployment checks pass. Use this release for [Phase 15](PHASE-15-multi-room-readiness.md), not a different development configuration.
