# Phase 00 — Project baseline and execution setup

**Status:** Not started · **Depends on:** None · **Owner:** Assign execution/evidence lead

## Goal and entry

Turn the approved documents into an owned work queue before implementation begins. Use the [implementation guide](../IMPLEMENTATION_GUIDE.md), [PRD](../PRD.md), [architecture](../ARCHITECTURE.md) and [TRD](../TRD.md); do not reopen adopted decisions merely because they are not implemented yet.

## Work

- [ ] Record the current document versions and assign named owners to Phases 01–17 and gates T1–T7.
- [ ] Confirm the assessment date/time, expected report/demo format and team availability with the supervisor. Schedule actual milestones and contingency time afterward.
- [ ] Inventory available laptop, webcam, controllers, network and prescribed parts. Preserve uncertainty: the PRD's earlier “not purchased” statement is not a current inventory check.
- [ ] Create the acceptance/evidence index covering every FR, NFR and metric, initially Pending, with owner, test, configuration and evidence fields.
- [ ] Establish source control and the team's normal review process if absent; exclude secrets, runtime records and private images. No remote repository or commit policy is presumed by this plan.
- [ ] Create a blocker/decision register with gate, owner, required evidence and next action. Start the report outline and collect evidence from each later phase.

## Acceptance and evidence

The team can identify who resolves each open gate and where each requirement will be built/tested. Dates are confirmed or explicitly pending; no deadline, electrical value or implementation pass is fabricated. The evidence index separates simulated, bench, integrated and assessed results.

**Save:** source baseline, actual inventory, owner/dependency list, assessment instructions and empty acceptance/evidence register.

## Done and handoff

Done when the baseline and owners are recorded. Open questions may remain at their approved gates. Complete [Phase 01](PHASE-01-hardware-readiness.md) before starting [Phase 02](PHASE-02-laptop-and-vision-spike.md) under the hardware-first execution order in the implementation guide.
