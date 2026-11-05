# Editorial review — structure and prose

Reviewed 2026-11-05 using bmad-review as required by bmad-ux doc_standards. Audience: human architecture and development consumers. Reference/Database model; Microsoft Writing Style Guide. Structure ran before prose. Reviewers proposed changes; parent applied the accepted edits.

Initial exact word counts from word_metrics.py: DESIGN.md 1,949; EXPERIENCE.md 6,459; total 8,408. No length target or cuts; proposed reduction 0 words (0%). Contextual repetition of movement/review/recovery rules and the canonical spine sections were preserved for distinct lookup tasks.

| Pass | Finding | Disposition |
| --- | --- | --- |
| Structure | Foundation mentions three unresolved product outcomes without a direct jump to the gate table. | Added an anchor to Open Decisions and Handoff Gates. |
| Prose | “Emergency stop is immediate and unconfirmed” can confuse user confirmation with physical stop verification. | Changed to “acts immediately without a confirmation dialog.” |
| Prose | J9 “confirms/save” has incorrect verb agreement. | Changed to “confirms and saves.” |
| Prose | G3 shorthand conflates movement, session outcome and object status. | Explicitly names stop movement, end unsuccessful session, object Lost. |
| Prose | G7 “doctor” obscures the academic role. | Changed role label to project supervisor. |

No application code, coded mockups or runtime verification was performed.
