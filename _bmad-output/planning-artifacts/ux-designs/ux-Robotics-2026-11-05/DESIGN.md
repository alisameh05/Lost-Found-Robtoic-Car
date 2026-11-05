---
name: Lost and Found
description: Functional visual contract for the Windows robot-search application; branding remains provisional.
status: final
updated: 2026-11-05
visual-approval: deferred
sources:
  - '../../../../docs/PRD.md'
experience: EXPERIENCE.md
colors:
  canvas: '#F5F5F5'
  surface: '#FFFFFF'
  surface-muted: '#E8E8E8'
  ink: '#171717'
  ink-secondary: '#484848'
  border: '#707070'
  action: '#242424'
  on-action: '#FFFFFF'
  focus: '#000000'
  video-matte: '#000000'
  video-label: '#FFFFFF'
typography:
  title:
    fontFamily: 'Segoe UI, system-ui, sans-serif'
    fontSize: 28px
    fontWeight: '600'
    lineHeight: '1.25'
  heading:
    fontFamily: 'Segoe UI, system-ui, sans-serif'
    fontSize: 20px
    fontWeight: '600'
    lineHeight: '1.35'
  body:
    fontFamily: 'Segoe UI, system-ui, sans-serif'
    fontSize: 16px
    fontWeight: '400'
    lineHeight: '1.5'
  label:
    fontFamily: 'Segoe UI, system-ui, sans-serif'
    fontSize: 16px
    fontWeight: '600'
    lineHeight: '1.5'
  caption:
    fontFamily: 'Segoe UI, system-ui, sans-serif'
    fontSize: 14px
    fontWeight: '400'
    lineHeight: '1.5'
rounded:
  sm: 4px
  md: 8px
spacing:
  '1': 4px
  '2': 8px
  '3': 12px
  '4': 16px
  '6': 24px
  '8': 32px
  gutter: 24px
  page-margin: 24px
components:
  navigation:
    background: '{colors.surface}'
    foreground: '{colors.ink}'
  action-button:
    background: '{colors.action}'
    foreground: '{colors.on-action}'
    radius: '{rounded.sm}'
    min-height: 44px
  emergency-stop:
    background: '{colors.ink}'
    foreground: '{colors.surface}'
    min-height: 56px
  field:
    border: '{colors.border}'
    radius: '{rounded.sm}'
    min-height: 44px
  object-row:
    background: '{colors.surface}'
    gap: '{spacing.4}'
  status-indicator:
    foreground: '{colors.ink}'
    background: '{colors.surface-muted}'
  image-selector:
    background: '{colors.surface-muted}'
    border: '{colors.border}'
  readiness-list:
    gap: '{spacing.2}'
  video-panel:
    background: '{colors.video-matte}'
    foreground: '{colors.video-label}'
  target-summary:
    background: '{colors.surface}'
    gap: '{spacing.3}'
  session-controls:
    background: '{colors.surface}'
    gap: '{spacing.3}'
  evidence-review:
    background: '{colors.surface}'
    gap: '{spacing.4}'
  recovery-panel:
    background: '{colors.surface-muted}'
    border: '{colors.ink}'
  history-list:
    gap: '{spacing.3}'
  feedback-panel:
    background: '{colors.surface-muted}'
    foreground: '{colors.ink}'
  confirmation-dialog:
    background: '{colors.surface}'
    radius: '{rounded.md}'
---

# Lost and Found — Visual Design

## Brand & Style

This is a functional visual specification for a fixed-desk operator driving a camera robot. The operator must distinguish live video, captured evidence, object status, session state, and the action that can safely happen next.

**[ASSUMPTION V1] All visual tokens, type choices, spacing, shapes, and layouts outside the PRD's required left/right split are provisional UX proposals.** Alisa will supply branding later. The neutral palette below makes the document usable without claiming an approved aesthetic direction. No logo, illustration style, decorative theme, component framework, dark theme, or visual reference product is selected.

[EXPERIENCE.md](EXPERIENCE.md) owns behavior. These two documents take precedence over any later mockup or imported reference; approved PRD requirements take precedence over either document. All surfaces currently use spine tables alone; no coded mockups are part of this handoff.

Brand handoff must resolve identity, accent/semantic colors, typography, icon style, density, and any dark theme. Replacements must preserve the contrast and operational hierarchy below. A branding change cannot turn a potential match into a confirmed result or conceal stopped/paused state.

## Colors

All frontmatter colors are concrete neutral placeholders, not approved brand choices.

| Token | Role and permitted pairings |
| --- | --- |
| `{colors.canvas}` | Application backdrop; pair with `{colors.ink}` or `{colors.ink-secondary}`. |
| `{colors.surface}` | Forms, history, review, controls; the same text pairings apply. |
| `{colors.surface-muted}` | Secondary grouping and persistent feedback; never the only sign of disabled, warning, or failure. |
| `{colors.ink}` | Primary text, status labels, strong outlines. |
| `{colors.ink-secondary}` | Supporting instructions and timestamps; not a substitute for hiding important status. |
| `{colors.border}` | Visible input/container edges on light surfaces. |
| `{colors.action}` / `{colors.on-action}` | Primary actionable control fill/text; use text and placement to distinguish actions. |
| `{colors.focus}` | Keyboard focus outline on light surfaces. On a dark control, use a white inner separation plus black outer ring. |
| `{colors.video-matte}` / `{colors.video-label}` | Video surround and opaque-backed labels. Do not rely on text directly over unpredictable camera imagery. |

Contrast targets: normal text at least 4.5:1; large text at least 3:1; control boundaries, focus indicators and meaningful graphics at least 3:1 against adjacent colors. Verify implemented pairings and any replacements. Never assume a token remains compliant over translucent surfaces or arbitrary video pixels. Evidence/target boxes use a black-and-white double outline with a readable label, so either edge remains visible against mixed imagery.

Statuses use explicit words and an additional shape/icon where useful. Lost/Found, Searching/Paused/Ended, unavailable connections, and Emergency stop do not depend on hue. A later semantic palette must retain this redundancy. Disabled actions retain readable labels and a visible reason; do not reduce an entire blocked control to illegible opacity.

## Typography

**[ASSUMPTION V2]** Use the locally available Windows system sans-serif stack; no font download is needed at runtime. `{typography.title}` names a screen, `{typography.heading}` groups a task, `{typography.body}` carries instructions, `{typography.label}` identifies controls/status, and `{typography.caption}` carries metadata. Do not shrink safety labels or validation below the body role to make them fit.

Use sentence case, familiar action labels, and full object names. Allow names and errors to wrap. Use aligned numerals for elapsed time and timestamps where supported. Display local date/time with enough precision to distinguish registration, session and review events; label what each time means. Full dates remain available when a compact list uses relative time.

Target text enlargement to 200% without loss of content or functionality, using equivalent logical sizing for native Windows or zoom/text controls for a browser surface. Controls expand with text; ellipsis is acceptable for a list preview only when the full value is available in object detail and to assistive technology. No all-caps paragraph instructions or image-baked text.

## Layout & Spacing

**[ASSUMPTION V3]** Use the 4px spacing scale, `{spacing.page-margin}` outer margin and `{spacing.gutter}` between major regions. Apply `{spacing.2}` inside related label/value groups, `{spacing.4}` within task groups, and `{spacing.6}` between groups. Spacing expresses task relationships, not decoration.

| Surface | Composition |
| --- | --- |
| History | Stable heading/navigation, name-search field, Lost/Found scope controls, object rows. Register object remains visible above results. |
| Register object | Name and image selection, reference preview/target selection, validation, then Register/Cancel. Selected target remains visible before save. |
| Object detail | Name/status/registration/expiry, reference and selected region, available search action, then session history. Found evidence stays attached to its original record. |
| Search setup | Target summary, exclusive control choice, required readiness and instructions, then Start. |
| Search workspace | Persistent target/mode/session summary above required split: laptop webcam/gesture feedback **left**, robot live video/AI results **right**. Persistent session controls and Emergency stop occupy a stable separate band. |
| Potential-match review | In-workspace review panel with captured screenshot/box, reference comparison, and Confirm/Reject/Stop; preserve required live/input context and stop access. |
| Recovery | In-workspace panel naming every unresolved cause, acknowledgment and readiness, then Resume eligibility. Review evidence remains accessible if both states coexist. |
| Session detail | Session times/outcome followed by chronological decision entries and their evidence. |
| Retention settings | Current value, registration-based explanation, affected-record preview, Save/Cancel. |
| Connection & control guidance | Task-specific instructions adjacent to readiness; no separate destination required. |

Primary desktop composition assumes enough space for both panels and the control band. Ordinary text, forms, history and settings reflow to a width equivalent to 320 CSS pixels without two-dimensional scrolling; use equivalent logical sizing tests for native Windows. At reduced width or large scaling, reduce secondary chrome and allow panels to resize while preserving left/right order. If the operational layout cannot show live video and essential controls legibly, follow EXPERIENCE.md's paused, readable arrangement for non-driving tasks; never silently collapse driving operation into a single hidden video tab. Any essential spatial-layout exception is limited to the video/image area, not ordinary text or controls.

Reference images and evidence use contain-fit, preserve aspect ratio and original coordinates, and never crop away the selected region. Live video uses the same principle; any letterboxing is matte black. Match boxes track the displayed image transform. Screenshot review is visibly titled **Captured evidence**, with capture/review metadata separate from the live label.

## Elevation & Depth

**[ASSUMPTION V4]** Establish hierarchy with spacing, headings, borders and surface changes. Use no decorative shadows or perspective effects. A single confirmation dialog may sit above a surface with a restrained scrim only when no session is active. During Searching or Paused, leave choices, help, review and recovery stay in modeless workspace panels, with Emergency stop visible and operable. Safety and recovery remain persistent rather than disappearing as transient notices.

## Shapes

**[ASSUMPTION V5]** Use `{rounded.sm}` on fields/buttons and `{rounded.md}` on grouped panels/dialogs. The emergency action has a strong rectangular outline and a distinct text label, not a shape that resembles an ordinary navigation item. Candidate boxes are image annotations, not tappable buttons. Icons always accompany text for critical states; no custom icon language is assumed.

## Components

Names match EXPERIENCE.md.Component Patterns. Subcontrols inherit these component rules; the table is the visual inventory.

| Component | Visual specification |
| --- | --- |
| Navigation | Persistent History/Register object/Retention settings labels; active destination has weight plus an indicator. Search workspace uses explicit return actions and an active-session summary rather than burying controls in navigation. |
| Action button | Minimum 44px height, `{rounded.sm}`, visible label; primary uses `{colors.action}`/`{colors.on-action}`, secondary uses outlined light surface. Focus double ring; pressed border/shape change; disabled label plus nearby reason. Pending label describes the operation. |
| Emergency stop | Minimum 56px height; strong contrasting fill, thick outline, full “Emergency stop” text; stable position in operational control band. “Stop session” remains a separately labeled ordinary action. No hover-only appearance. |
| Field | Persistent label above a bordered input; hint/error below. Required status appears in text. Focus ring; invalid outline plus explicit message. Search, object name and retention value use this pattern. |
| Object row | Reference thumbnail, full/wrapped name, Lost/Found label, registration time, and expiry context. Selected/keyboard-focus appearance distinct from status; no status-only colored thumbnail. |
| Status indicator | Explicit status/device name plus availability or state. Session and object indicators are separately labeled. Optional icon reinforces text; pending and unavailable are not rendered as the same word. |
| Image selector | Image-picker action, aspect-preserving preview, contrasting target boundary/handles, visible target confirmation, and labeled position/size controls usable by keyboard or single-pointer clicks without dragging. No image/invalid image messages occupy the preview area. |
| Readiness list | Aligned required-path labels, available/unavailable text, actionable reason/help. A selected mode stands out by selection control and label; inactive mode is clearly noncontrolling. |
| Video panel | Opaque title/status strip, aspect-preserving frame, freshness information, optional matching overlay. Lost/frozen live video has an unmistakable “Not live” cover/label; never an unchanged “Live” badge. |
| Target summary | Reference-region thumbnail, object name, object status and mode/session labels; compact enough to remain visible alongside controls. |
| Session controls | Stable ordered Start/Pause/Resume/Stop session area with current eligibility reasons; active target/mode lock is visible. Do not move the control band when review or recovery appears. |
| Evidence review | Explicit captured-evidence heading, screenshot/box, reference comparison and metadata; Confirm/Reject/Stop session grouped with clear spacing. Confirmation is not styled as a detector-generated result. |
| Recovery panel | Strong outline, plain-language cause list, stopped/paused statement, acknowledgment and restored-path status. No dismiss-only treatment. Multiple causes fit without hiding the control band. |
| History list | Chronological session/decision rows with labeled times/outcomes and evidence thumbnails. Confirmed/rejected are textual; expandable evidence preserves aspect ratio. |
| Feedback panel | Inline title, concise explanation, and one relevant recovery action where available. Loading text and reserved content area, empty explanation, or persistent error share anatomy; critical messages do not auto-expire. |
| Confirmation dialog | No-active-session tasks only; one level, descriptive heading, consequence and explicit action/cancel labels. Default focus on the least destructive action. Operational choices use modeless workspace panels instead. |

## Do's and Don'ts

| Do | Don't |
| --- | --- |
| Keep live robot video, session state and emergency action visible together. | Replace operation with a full-screen animation, alert or unrelated destination. |
| Differentiate Lost/Found, session state, and connection status in text. | Call a paused session “Ended” or a stopped command proof of physical wheel feedback. |
| Label screenshot evidence separately from live video. | Reuse a frozen screenshot beneath a “Live” label. |
| Preserve the reference and target region without distortion. | Crop imagery for decorative composition. |
| Show potential-match language until explicit confirmation saves. | Use a Found badge or celebratory success appearance for AI similarity alone. |
| Keep provisional branding visible as a handoff decision. | Treat these neutral tokens as Alisa's aesthetic approval. |
| Use visible focus, plain status labels, and scalable text. | Make color, hover, animation, sound or gesture the sole access path. |
