# Proactive mechanical coverage — UX draft

Checked 2026-11-05 against approved `docs/PRD.md` v1.0 and the existing PRD extraction. This is the bmad-ux Finalize Pass 1 check, not optional independent UX/accessibility review and not implementation or hardware qualification.

## Flow and surface coverage

- FR-1 through FR-17 and NFR-1 through NFR-6 are present in the Requirement Coverage table with governing surfaces/rules/journeys. SM-1, SM-C1, SM-2, SM-3 and SM-4 have separate qualification mappings.
- Ten named illustrative journeys J1–J10 contain numbered steps, an explicit climax, and a failure branch. The PRD has no formal UJ identifiers or named personas to inherit.
- All ten IA surfaces/regions (S1, S2, S3, S4, S5, S5a, S5b, S7, S8, S9) have entry/exit/Back behavior and at least one named journey. S9 is local contextual guidance rather than an additional primary destination; the numbering intentionally preserves S5a/S5b as workspace regions.
- Each surface has a per-surface loading/empty/error/denial/recovery row. Shared focus, offline and keyboard rules are specified once and apply to all surfaces. Device/file permission states are distinguished from nonexistent account permissions.
- Source invariants retained: release stops movement without necessarily pausing matching; Pause disables both; mode/target lock includes Paused; human confirmation alone establishes Found; rejected continuously visible candidate suppression is session-scoped; Ended never resumes; active/Paused retention grace ends at session end.

## Token, component and source checks

- Python/YAML parse of DESIGN.md frontmatter passed. All 11 color values are concrete six-digit hex strings.
- Every `{colors.*}`, `{typography.*}`, `{rounded.*}`, `{spacing.*}` and `{components.*}` reference used in either spine resolves against DESIGN.md frontmatter. No unresolved token references.
- Sixteen named components have matching rows in DESIGN.md.Components and EXPERIENCE.md.Component Patterns. No name differences between these inventories.
- DESIGN.md body follows the eight canonical sections in order. EXPERIENCE.md includes all required spine sections plus platform, local-data, coverage and explicit-gate sections.
- Both source references `../../../../docs/PRD.md` resolve to the approved source. Paired-spine Markdown links resolve. The accessibility reference is the primary W3C WCAG 2.2 source provided by the parent; the standard is a proposed target, not claimed compliance.

## Visual reference coverage

No imports, mockups or wireframes were supplied or generated for this documentation-only run. All surfaces are explicitly spine-only. Neutral visual tokens remain provisional because branding is deferred; there is no external reference artifact to orphan or reconcile. The extraction/reconciliation artifacts remain working evidence rather than visual specifications.

## Deliberately unresolved upstream decisions

EXPERIENCE.md G1–G3 retain the PRD's required pre-implementation agreements for AI unavailability, application interruption, and Stop during unreviewed evidence. They include labeled proposals without claiming approval. G4–G7 retain mapping/image/retention/branding/equipment and qualification work. These are visible handoff limits, not missing approved-feature surfaces or evidence of implementation readiness.

The user's selected full UX rubric and accessibility review subsequently ran. All four findings were repaired and their originating reviewers verified closure; see the paired review files and validation-report.md. Structure/prose polish also ran. Final YAML, token/source links, component parity and coverage checks passed after the edits. These are documentation checks, not runtime or hardware qualification.
