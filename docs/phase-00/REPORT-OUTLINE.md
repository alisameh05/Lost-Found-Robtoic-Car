# Report and evidence handoff

This outline is a starting structure, not a confirmed assessment format. The assessment coordinator must reconcile it with supervisor instructions before Phase 17. No measured result is implied by an empty section.

## Report outline

1. **Executive summary and scope** — approved problem, PRD version, users and operating boundary.
2. **Requirements and acceptance** — FR/NFR/metric traceability; deviations approved through upstream revisions only.
3. **Architecture and decisions** — adopted AD-1–AD-15, local service boundaries, device and data flow, safety invariants.
4. **Equipment and safety** — actual inspected inventory, exact variants, T2/T3 decisions, wiring/power review and limits; distinguish reported purchases from inspected items.
5. **Implementation** — phases completed, release identifiers, configuration and dependency/model manifests.
6. **Methods** — each trial procedure, environment, room layout/route, object/scene set, timing/instrumentation and test level.
7. **Results** — all passes, failures, misses, late alerts, interruptions and retests linked to the acceptance index; distinguish simulated, bench, integrated and assessed evidence.
8. **Limitations and unresolved gates** — known faults, unqualified conditions, remaining blockers and dependent work.
9. **Demonstration** — confirmed assessment format, setup, scripted steps, safety roles and recovery plan.
10. **Appendices** — sanitized inventory, configuration/release manifests, trial records, diagrams, approvals and evidence index.

## Evidence conventions

- Suggested sanitized repository locations: `evidence/phase-XX/` for phase handoffs and `evidence/qualification/` for complete-system results. Keep private media, credentials, runtime records and unsanitized images/video in approved local storage outside Git.
- Name evidence `YYYY-MM-DD_<phase-or-requirement>_<trial-id>_<short-description>.<ext>` after actual capture. Do not use a date or test status that was not observed.
- Each record includes requirement/trial IDs, release/configuration, conditions, checks, results including failures, evidence reference and remaining issues.
- Mark the evidence level as planned, simulated, bench, integrated or assessed as applicable. Evidence level does not change the separate result status.
- Sanitize personal/private information before a tracked artifact is created. Never put network credentials, access tokens, private reference images or unredacted object names in ordinary logs or commits.
- The acceptance index is [ACCEPTANCE-INDEX.md](ACCEPTANCE-INDEX.md). Add evidence links only after the cited artifact exists and has been reviewed.

## Phase handoff locations

| Handoff | Suggested location | Required record |
| --- | --- | --- |
| Phase 00 baseline | `docs/phase-00/` | Source, ownership, inventory/schedule, 29-entry index, blockers, report outline, review disposition |
| Phase 01–15 work | `evidence/phase-XX/` | Sanitized phase-specific design, configuration, tests and handoff evidence |
| Phase 16 qualification | `evidence/qualification/` | Complete-system trial records, failures, final configurations and requirement links |
| Phase 17 assessment | `evidence/phase-17/` | Confirmed assessment instructions, report/demo artifact, rehearsal record and release archive reference |

These paths are conventions proposed for organization. Their creation does not establish evidence, qualification or assessment approval.
