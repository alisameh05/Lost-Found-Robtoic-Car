# TRD structure review

This document exists to help the human implementation team build and qualify the Lost and Found application and robot against the approved technical contracts while respecting open decisions and safety gates.

Source: `docs/TRD.md`, draft v1.0, reviewed 2026-11-05. Pass: structure only. Style guide: Microsoft Writing Style Guide. No length target. No source edits made.

Review stage: the findings and metrics below describe the original 8,011-word document. The parent editor subsequently applied a different, compatible heading scaffold: §§9.1–9.4 separate shared payloads, endpoints, events/frames/leases and external integrations; §§10.1–10.6 expose the security topics. That updated document measures 8,044 words and is the source for the dependent prose review. The original findings are retained as recommendations, not a description of the final heading layout.

Chosen model: **Explanation (Conceptual)** for the overall progression from authority and scope through architecture to implementation and verification, with **Reference/Database** organization inside the API and security contracts. The existing top-level sequence supports that purpose. The smallest useful changes improve navigation inside two dense sections; no content cuts or new decisions are recommended.

| Pass | Original Text | Revised Text | Changes |
| --- | --- | --- | --- |
| structure | §9.1 “HTTP and events,” lines 241–279: 1,081 body words covering shared mutations, endpoint groups, state events, binary frames, workspace leases and recovery occurrences under one heading. | **MOVE** the existing content into six level-four subsections, in its current order: “Common actions and payloads” before “Version the API under”; “HTTP endpoints” before the endpoint table; “State events” before “Each JSON state event”; “Video frames” before “Video protocol v1”; “Workspace leases and heartbeats” before “Workspace heartbeats carry”; “Recovery occurrences” before “Every recovery occurrence has.” | Makes the distinct wire contracts directly navigable for frontend, backend and integration implementers without changing sequence or meaning. Preserve every paragraph and table. Word impact: 0 of 1,081 body words removed; these exact Markdown headings add 22 words under the metrics script's counting rule. |
| structure | §10 “Authentication, authorization, isolation and security,” lines 293–309: 568 body words, with seven bold inline topic labels. | **MOVE** each existing topic into a level-three subsection by promoting its existing label to a heading: “Authentication,” “Authorization,” “Multi-tenant isolation,” “Local services,” “Data and input,” “Devices and network,” “Assets and maintenance.” Retain the current order and every sentence; keep the CORS paragraph with “Local services.” | Exposes the existing topic structure in heading navigation and breaks the longest security block into identifiable reference units. Word impact: no content words removed; promoting the seven existing labels adds 7 Markdown heading-marker tokens to the total count. |
| structure | §1 readiness/authority (230 words), §13 open gates (373 words), and §12 verification (616 words). | **PRESERVE** the early readiness summary and the later full gate and verification tables. | The opening already states that software design may proceed while applicable assembly and acceptance gates remain open. Later owner/deadline/evidence tables serve a different implementation task; they are useful reinforcement rather than removable duplication. Word impact: 0 removed from these 1,219 body words. |
| structure | §3 architecture diagram and ownership table (602 words), §7 schema diagram and constraints (631 words), and safety/recovery rules across §§5–6, 8–10 and 12. | **PRESERVE** diagrams, tables and repeated safety constraints where they constrain different components or phases. | Human readers need both an overall model and local contract rules. Moving all stop, expiry, persistence or recovery restrictions into one distant section would weaken component-level comprehension. No cut, merge or new safety decision is proposed. Word impact: 0 removed; the cited sections' exact counts are below. |

Two actionable recommendations and two preservation findings. If both recommendations are accepted exactly as described, the measured total becomes **8,040 words**: **0 words removed (0% reduction)** and **29 added heading/marker tokens (0.36% net growth)**. These deltas were checked with the same word-count function against an in-memory transformation; `docs/TRD.md` was not changed. No length target applies. There is no proposed loss of requirements, safety rules, gate evidence, examples, diagrams or reader context. The only trade-off is six additional nested headings and promotion of seven existing labels.

## Exact source metrics

Command: `python .agents/skills/bmad-review/scripts/word_metrics.py docs/TRD.md`

Result: **8,011 total words**. The script counts whitespace-separated tokens, including Markdown syntax. Section counts cover the body directly beneath each heading and exclude heading text; parent rows do not aggregate their children. Consequently, the section rows need not sum to the total.

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
| 9.1 HTTP and events | 3 | 1,081 |
| 9.2 External integration boundaries | 3 | 183 |
| 10. Authentication, authorization, isolation and security | 2 | 568 |
| 11. Infrastructure, deployment and operations | 2 | 334 |
| 12. Measurable non-functional requirements and verification | 2 | 616 |
| 13. Open gates, owners and exit evidence | 2 | 373 |
| 14. Traceability and technical references | 2 | 0 |
| 14.1 Requirement coverage | 3 | 354 |
| 14.2 Official-source checks | 3 | 174 |

No technical validation, external-source verification, prose copy-edit or implementation readiness approval was performed by this pass.
