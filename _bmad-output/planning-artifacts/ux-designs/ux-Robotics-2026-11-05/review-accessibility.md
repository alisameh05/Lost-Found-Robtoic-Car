# Accessibility Review — Lost and Found

Reviewed: 2026-11-05. Scope: the draft documentation pair, not an implemented application. Locations below refer to the pre-repair drafts. Approved behavior was checked against the PRD extraction; visual tokens and accessibility proposals remain provisional.

## Overall judgment

The documents provide a useful accessibility foundation: meaningful names and states, keyboard navigation, non-color status, deliberate recovery, minimal motion, persistent errors, and honest limits to visually steered robot access. Three contract details need clarification before handoff: modal focus versus emergency-stop access, measurable scaling/reflow expectations, and a pointer alternative to dragging the target region. This review does not establish WCAG conformance, safe physical stopping, or successful Narrator/device testing.

## Findings

### High — Modal focus containment conflicts with emergency-stop access

Locations: EXPERIENCE.md §Information Architecture, IA2 (line 43); §Component Patterns, Confirmation dialog (line 97); §Accessibility Floor (lines 167–169). DESIGN.md §Elevation & Depth and §Components, Confirmation dialog.

The draft requires confirmation dialogs to trap focus while also requiring Emergency stop to remain operable whenever a session exists. The active-session leave choice could be implemented as such a dialog. A visible emergency control outside a modal focus scope is insufficient: a true modal makes outside content unavailable to keyboard and assistive technology. [W3C modal-dialog pattern](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/).

Fix: explicitly make operational help, review, recovery, and the Stay/Stop-and-leave choice modeless inline workspace regions. Keep Emergency stop in the shared keyboard traversal and assistive-technology reading order. Reserve focus-trapped Confirmation dialogs for dirty-form discard and retention consequences when no session is active. Apply the same rule to both spines. An alternative is to include an emergency action inside every operational modal, but that adds unnecessary duplicated control rules.

### Medium — Scaling and reflow need measurable acceptance conditions and a usable stopped fallback

Locations: EXPERIENCE.md §Accessibility Floor (lines 170–172); §Responsive & Platform (lines 176–180); DESIGN.md §Typography and §Layout & Spacing.

The draft asks implementations to respect scaling, then leaves the operational minimum to qualification. It does not define a measurable floor for ordinary forms/history/settings, and its small-window fallback requests Pause without explicitly keeping the paused application usable for review, recovery and ending the session. Merely blocking operation can leave a magnifier/text-enlargement user unable to complete non-driving actions.

Fix: specify text enlargement to 200% without content/function loss, and ordinary vertical-reading screens at a width equivalent to 320 CSS pixels without two-dimensional scrolling where applicable. For native Windows, use equivalent logical sizing/accessibility tests rather than implying browser zoom is available. Scope any essential two-dimensional-layout exception to robot video/image manipulation, not navigation, controls or ordinary text. When driving is paused because the split view is unusable, provide a readable non-driving arrangement for evidence, recovery, Emergency stop and Stop session; restoring size never resumes automatically. Test actual Windows scaling, text enlargement, keyboard focus and Narrator before release. These are design targets, not verified capabilities. [WCAG resize text](https://www.w3.org/TR/WCAG22/#resize-text), [WCAG reflow](https://www.w3.org/TR/WCAG22/#reflow).

### Medium — Region selection must support a single pointer without dragging

Locations: EXPERIENCE.md §Component Patterns, Image selector (line 88); §Interaction Primitives, Pointer, keyboard and selection (line 156); DESIGN.md §Components, Image selector.

The draft explicitly provides dragging plus a keyboard alternative. Keyboard access alone does not settle the separate need to complete a drag-based action with a single pointer without dragging. The described labeled region controls can satisfy this, but their pointer operation is not explicit. [WCAG dragging movements](https://www.w3.org/TR/WCAG22/#dragging-movements).

Fix: state that the labeled position/size controls work with both keyboard and ordinary clicks/taps, with no press-and-drag requirement; alternatively offer click-first-corner/click-opposite-corner selection. Include preview, reset, acceptance, bounds validation and textual selected-region state in either method. Keep this a provisional interaction proposal under G4, not an approved image-limit decision.

## Coverage and evidence

| Area | Result |
| --- | --- |
| Keyboard and focus | Standard traversal/activation, heading focus, return focus and review focus are specified. Operational modal conflict is recorded above. No third keyboard driving mode is introduced. |
| Assistive technology | Names, roles, selected/locked/invalid/pending states and meaningful status announcements are required. Frame/freshness spam is explicitly prohibited. Actual Windows Narrator testing remains pending. |
| Image selection | Bounded, nonzero selected region, replacement reset, preview and keyboard/text representation are covered. Single-pointer non-drag clarification is recorded above. |
| Contrast | Calculated provisional solid-token pairs: ink/surface 17.93:1; secondary ink/canvas 8.39:1; secondary ink/muted surface 7.46:1; border/muted surface 4.04:1; action/on-action 15.52:1; focus/canvas 19.26:1; video label/matte 21:1. These checks do not prove arbitrary video overlays, forced colors, implemented focus rings or replacement branding. |
| Status and errors | Object/session/connection distinctions are textual; errors retain valid input and identify recovery. Safety and unsaved-decision messages persist. |
| Motion and time | Reduced motion, no flashing, no decision timeout and no automatic review dismissal are specified. Stop must precede animations/persistence. |
| Hold and recovery | Input neutralization, fresh hold after Resume, no queued motion, inactive-mode exclusion and no reconnection-driven movement are covered. Physical stop latency requires hardware measurement. |
| Scope limits | Controller is an alternative to gesture input, not proof of universal motor/vision access. The documents do not claim that narration makes live visual steering safe. |

## Remaining verification boundary

After the contract fixes, implementation still needs keyboard-only registration/review/history/settings tests; Narrator role/state/focus checks; actual laptop scaling and stopped-layout tests; pointer non-drag selection; implemented contrast and forced-color checks; and hardware stop/recovery qualification. No code, browser/native UI, controller or robot was operated in this review.

## Resolution check — 2026-11-05

Narrowly re-read the repaired clauses in both spines. All three documentation findings are closed:

- **Modal/emergency-stop conflict:** EXPERIENCE.md IA2, Confirmation dialog and Accessibility Floor now explicitly use modeless operational leave/help/review/recovery panels and restrict focus-trapped dialogs to no-active-session tasks. DESIGN.md Elevation & Depth and Confirmation dialog match. Emergency stop remains reachable in the operational keyboard order.
- **Scaling/reflow:** DESIGN.md Typography/Layout and EXPERIENCE.md Accessibility Floor now state 200% text enlargement and ordinary reading/form reflow at 320 CSS-pixel-equivalent width, with native Windows logical-size testing. EXPERIENCE.md Responsive & Platform specifies a readable modeless paused arrangement for evidence/review/recovery/emergency/end actions. The essential two-dimensional exception is confined to the spatial video/image area, preserving its left/right relationship; it does not exempt ordinary text or controls.
- **Single-pointer region selection:** Both spines now explicitly make labeled position/size controls usable with keyboard and ordinary single-pointer clicks without dragging. EXPERIENCE.md preserves preview, reset, explicit acceptance, bounded values and textual selection state.

No unresolved conflict was found within this closure check. This closes the written-contract findings only; the implementation and hardware verification boundary above remains unchanged. No broader second review was performed.
