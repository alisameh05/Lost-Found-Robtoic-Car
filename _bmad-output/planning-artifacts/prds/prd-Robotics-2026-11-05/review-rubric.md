# PRD Quality Review — Lost and Found

## Overall verdict

The draft is adequate for user review and substantially reflects the interview: a complete, manually operated university robot system with explicit human confirmation, hardware constraints, and measurable demonstration targets. It appropriately separates selected targets from measured capability and gives unresolved equipment/design details owners and revisit gates. Two behavioral gaps should be resolved or explicitly assigned before the document is treated as an implementation-ready baseline: expiry during a running application and search-session behavior when AI or the application is interrupted.

## Decision-readiness — strong

Sections 2, 4, and 6 state the chosen operating boundary rather than balancing incompatible options: fixed-desk control across connected rooms, one target/session, both control modes, offline runtime, and doctor-prescribed procurement. The wired allowance does not silently remove multi-room requirements. Section 8 makes coverage, latency, and endurance qualification explicit and requires an authorized revision if targets are unmet.

The user can approve a product baseline without pretending the exact laptop specifications, hardware variants, test objects, or assessment date are known. Their named team/doctor gates are proportionate to this academic prototype.

## Substance over theater — strong

The vision is specific to reference-image robot searching and human-reviewed visual similarity. The draft avoids invented market sizing, monetization, elaborate personas, generic security promises, and novelty claims. Hardware, retention, controller exclusivity, and recovery rules are present because the interview established them. The supporting addendum preserves technical suggestions without pretending they are validated architecture.

## Strategic coherence — strong

The complete-system MVP serves one coherent search loop: register, navigate, detect, review, and retain evidence. Success metrics evaluate detection, false alerts, stop behavior, video delay, and endurance rather than irrelevant adoption measures. SM-C1 explicitly counterbalances SM-1, and the visual-similarity boundary is consistently distinguished from unique-belonging recognition.

The all-features MVP is demanding for the stated delivery window, but it is the user's explicit choice. The document honestly treats feasibility as an integration gate rather than silently reducing scope.

## Done-ness clarity — adequate

All seventeen FRs have observable acceptance statements. Section 7 defines object/trial counts, timing origins, negative-scene duration, end-to-end measurement, and coverage on the actual route. It explicitly prevents isolated component results or successful-trial selection from being passed off as complete-system qualification.

### Findings

- **[medium] Runtime retention trigger remains ambiguous** (§4.4 FR-15) — The requirement says expiry removes data, but acceptance only guarantees an inactive expired record is removed "by the next startup." If the application remains open, an implementation could retain expired inactive records indefinitely while still satisfying that acceptance wording. *Fix:* specify the running-application purge trigger as well as startup behavior, or explicitly defer the purge cadence/trigger with an owner and preimplementation gate. Preserve the user's active-session exception and registration-based age; do not introduce a background service or an unapproved numeric purge SLA.

- **[medium] AI/application interruption has no session-state contract** (§4.3 FR-8–FR-10; §4.4 FR-13; §4.5 FR-17) — Connection/input/video failure and recovery are clear, but the draft does not state what happens when AI matching becomes unavailable while control/video remain healthy, or when the application closes/restarts during an active session. "Every session" persists, but its interrupted outcome and whether it may resume are unspecified. *Fix:* obtain a product decision or add an explicit team-owned preimplementation decision covering visible AI-unavailable state, session/history outcome on application interruption, and deliberate restart/recovery. Do not assume automatic movement resumption; existing command-loss and fresh-input rules must continue to apply.

## Scope honesty — adequate

The rejected PDF is explicitly excluded as procurement authority, the authoritative list is preserved with quantity ranges, and sensor/servo functions remain out of scope. Candidate software choices live in the addendum. Section 8 declares unresolved design and equipment details rather than smuggling them in as facts. The addendum also records the real retention trade-off: recent evidence can expire with an older registration, while an indefinitely active session can delay deletion.

The two findings above concern additional operational decisions, not a reason to reopen the user's explicit MVP choices. They can be resolved by targeted decisions or honest owned gates; no unverified performance should be presented as accepted.

## Downstream usability — adequate

The glossary distinguishes object status from session state, and globally stable FR-1–FR-17, NFR-1–NFR-6, SM-1–SM-4, and SM-C1 provide usable extraction anchors. Each feature subsection has behavioral acceptance criteria. Architecture can clearly identify the prescribed hardware and the design work left to do.

The walkthrough is labeled illustrative instead of claiming an elicited real user session. For a single-operator academic capability specification, a named persona/UJ catalog would add little; its omission is proportionate. The operating gaps above should be pinned before stories assume interruption behavior.

## Shape fit — strong

The capability-spec structure fits a single-operator hardware/software demonstration. It includes product vision, scope, business/state rules, functional acceptance, NFRs, procurement constraints, and qualification gates without importing commercial-launch ceremony. The small addendum appropriately carries implementation proposals and trade-offs. No code implementation or performance qualification is claimed.

## Mechanical notes

- Requirement and metric IDs are unique and contiguous within their respective main sequences; SM-C1 is a separately named counter-metric.
- Requirement/metric cross-references resolve. No inline assumption tags require an assumptions-index round trip; unconfirmed details are explicitly listed in section 8.
- The sole illustrative walkthrough is intentionally not represented as an observed or named-persona user journey.
- Draft frontmatter correctly remains `status: draft` pending user approval.

## Finding counts

Critical: 0. High: 0. Medium: 2. Low: 0.

## Resolution check — 2026-11-05

Re-read the revised FR-15 and section 8 against the two original findings; the findings above remain as review history.

- Runtime retention ambiguity: **resolved**. FR-15 now requires expiry removal while the application is open, preserves the active-session exception, and removes closed-application expiries at startup before display or new searches.
- AI/application interruption contract: **explicitly deferred with a gate**. Section 8 assigns the team to agree AI-unavailability, application-interruption, and unreviewed screenshot/history outcomes before implementation while preserving stop/recovery and human-confirmation requirements. This is an honest remaining product/design decision, not an invented outcome or a completed implementation contract.

The revised draft is suitable for user approval as a requirements baseline with stated gates. **No critical or high issues remain.** The original two medium findings have been resolved or converted into the explicit, owned preimplementation gate; no further rubric change is required for this approval round.
