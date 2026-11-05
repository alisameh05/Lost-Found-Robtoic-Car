# Phase 04 — Registration and persistent records

**Status:** Not started · **Depends on:** 03 · **Owner:** Backend/data and frontend team

## Goal and entry

Implement FR-1 and the data foundation for FR-11–FR-15 using [TRD sections 7–9](../TRD.md). All writes belong to the backend. The full review workflow and retention scheduler arrive in Phases 10/11.

## Work

- [ ] Implement versioned SQLite migrations, explicit transactions, foreign keys and the schema/ownership constraints for objects, sessions, matches, media, receipts, settings and storage operations.
- [ ] Establish the managed local media/staging root and generated paths. Reject arbitrary client file/delete paths and keep runtime data outside source/build directories.
- [ ] Build name/image/ROI registration: JPEG/PNG, at most 10 MiB encoded and 20 MP decoded, orientation normalization and backend repeat validation.
- [ ] Support rectangular drag selection and keyboard position/size fields in normalized source pixels. Replacing the image clears selection.
- [ ] Prepare/flush/check images and coordinate media metadata with registration. Implement operation reconciliation primitives so interrupted saves do not become complete records.
- [ ] Create the initial Lost/Found list, name search and object detail/reference view. Preserve duplicate names as separate IDs and immutable registration times.
- [ ] Add storage integrity/readiness results for later Start guards and boundary/duplicate-submission tests.

## Acceptance and evidence

Invalid, oversized, corrupt or missing inputs cannot complete registration. Valid registration creates one independent Lost record and one usable reference copy; retry cannot duplicate it. Unexpired committed records survive restart. ROI coordinates agree across orientation, scaling, mouse and keyboard. Database failures are visible rather than an invented empty history.

**Save:** migration/schema baseline, sample validated records, image/ROI boundary results, restart and interrupted-registration evidence.

## Done and handoff

Done when registration and storage primitives pass. Supply reference records to [Phase 08](PHASE-08-local-matching-worker.md) and data interfaces to [Phase 09](PHASE-09-session-and-safety-coordinator.md). Do not mark full history or retention complete yet.
