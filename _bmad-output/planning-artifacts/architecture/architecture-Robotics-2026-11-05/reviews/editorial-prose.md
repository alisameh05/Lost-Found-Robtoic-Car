# TRD prose review

This document exists to help the human implementation team build and qualify the Lost and Found application and robot against the approved technical contracts while respecting open decisions and safety gates.

Source: updated `docs/TRD.md`, draft v1.0, reviewed 2026-11-05 after the parent editor's heading changes. Pass: prose only. Style guide: Microsoft Writing Style Guide. No length target. No source edits made.

The voice is intentionally contractual: direct imperatives, precise state names and identifiers, short table cells, component-specific prohibitions, and explicit distinctions between required behavior and measured qualification. Preserve that tone and terminology. Slashes and abbreviations are often functional technical shorthand; do not expand them throughout merely for stylistic preference.

Structure context: the preceding review recommended heading scaffolding within the API/security sections and preservation of safety repetition, diagrams, gates and verification tables. The parent editor added headings without deleting technical passages. No passage was tagged CUT or MERGE, so none was excluded from this pass. Frontmatter, code blocks and structural markup were excluded from copy-editing.

| Pass | Original Text | Revised Text | Changes |
| --- | --- | --- | --- |
| prose | §4: “Stop permission is revoked immediately even when persistence remains pending.” | “Motion permission is revoked immediately even when persistence remains pending.” | Corrects the permission being revoked. As written, the sentence appears to revoke permission to stop. The neighboring text and motion-gate contract already establish that motion is revoked while saving can remain pending; no behavior changes. |
| prose | §9.1, Registration payload: “`action_id`, `name`, reference image bytes, and `roi` with integer `x`, `y`, `width`, `height` in orientation-normalized source pixels. Never display coordinates.” | Consider: “`action_id`, `name`, reference image bytes, and `roi` with integer `x`, `y`, `width`, `height` in orientation-normalized source pixels. Never use display coordinates in this payload.”? | Disambiguates “display” as a coordinate space rather than an instruction never to show coordinates to a user. The preceding sentence already requires source-pixel payload coordinates. This is phrased as a consideration because the original final sentence could be read as a separate UI prohibition; confirm the intended reading rather than adding a new UI rule. |
| prose | §12, NFR-1 / FR-16: “All normal searching/history works with internet disconnected after setup; no normal reference/video/evidence upload” | “All normal search and history operations work with internet disconnected after setup; no normal reference/video/evidence upload” | Clarifies the compound subject and its verb while retaining the offline and upload requirements. |

Three recommendations: two direct copy-edits and one coordinate-wording clarification to confirm. No other high-impact prose issue was found. None changes thresholds, state transitions, gates, requirements or technical decisions. No technical validation, external-source verification or implementation readiness approval was performed by this pass.

## Exact source metrics

Command: `python .agents/skills/bmad-review/scripts/word_metrics.py docs/TRD.md`

Result: **8,044 total words** in the updated source. The script counts whitespace-separated tokens, including Markdown syntax. Section counts cover the body directly beneath each heading and exclude heading text; parent rows do not aggregate their children. These metrics are for the source reviewed, not an edited result.

| Heading | Level | Exact body words |
| --- | ---: | ---: |
| (preamble) | 0 | 30 |
| Lost and Found — Technical Requirements Document | 1 | 0 |
| 1. Purpose, authority and readiness | 2 | 230 |
| 2. Operating scope and technology stack | 2 | 423 |
| 3. System architecture and responsibilities | 2 | 602 |
| 4. Frontend contract | 2 | 425 |
| 5. Domain states, transitions and failure outcomes | 2 | 553 |
| 6. Inputs, video freshness and motion safety | 2 | 0 |
| 6.1 Input mappings | 3 | 157 |
| 6.2 Live video | 3 | 281 |
| 6.3 Command permission and stopping | 3 | 344 |
| 7. Database schema and relationships | 2 | 631 |
| 8. Evidence consistency and retention | 2 | 0 |
| 8.1 Consistent saves | 3 | 179 |
| 8.2 Retention algorithm | 3 | 333 |
| 9. API, event and integration contracts | 2 | 0 |
| 9.1 HTTP actions and shared payloads | 3 | 328 |
| 9.2 Endpoints | 3 | 387 |
| 9.3 Events, frames and control leases | 3 | 366 |
| 9.4 External integration boundaries | 3 | 183 |
| 10. Authentication, authorization, isolation and security | 2 | 0 |
| 10.1 User access and authorization | 3 | 94 |
| 10.2 Multi-tenant isolation | 3 | 50 |
| 10.3 Local service protection | 3 | 215 |
| 10.4 Data and input protection | 3 | 71 |
| 10.5 Devices and network | 3 | 65 |
| 10.6 Assets and maintenance | 3 | 63 |
| 11. Infrastructure, deployment and operations | 2 | 334 |
| 12. Measurable non-functional requirements and verification | 2 | 616 |
| 13. Open gates, owners and exit evidence | 2 | 373 |
| 14. Traceability and technical references | 2 | 0 |
| 14.1 Requirement coverage | 3 | 354 |
| 14.2 Official-source checks | 3 | 174 |
