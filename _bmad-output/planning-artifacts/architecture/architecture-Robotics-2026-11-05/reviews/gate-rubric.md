# Architecture rubric gate — 2026-11-05

Verdict: **PASS — R1 and R2 verified closed**. No missing system dimension or unresolved architectural choice prevents beginning software implementation. This is a document gate, not evidence of implemented, hardware-compatible or qualified behavior. The closure check below is limited to the two reported seams; it does not claim a new full-document review after subsequent edits.

## Repair verification

- **R1 closed:** Current TRD section 6.3, line 175, explicitly allows a new generation/ARM handshake after ordinary release/recognition stop in otherwise healthy Searching on neutral-then-fresh hold, without Pause/Resume. Initial Start/fault recovery retain their approved user gates; emergency, expired command and required-path failure explicitly cannot use the ordinary rearm path. Invalidating old generations remains intact. This resolves the ordinary release/reapply ambiguity without weakening fault recovery.
- **R2 closed:** Current TRD section 7, line 208, defines Object/Settings receipt scope with exactly one matching owner FK, nullable object/settings fields and null session for settings receipts. Settings receipts persist with the independent settings action and contain no object data; object expiry still cascades object-owned receipts. Section 9.1, lines 243–252, scopes settings revisions and explicitly checks committed receipts/fingerprints before stale-revision checks, so response-loss retry returns the original result. This supports retention mutation with no registered objects and after object expiry.

The original observations below remain as review history and are no longer open findings.

## Reviewed sources and authority

- `_bmad-output/planning-artifacts/architecture/architecture-Robotics-2026-11-05/ARCHITECTURE-SPINE.md`, complete.
- `docs/TRD.md`, complete (390 lines).
- `docs/PRD.md`, complete approved v1.0 baseline.

Read-only review; no source documents changed. Detailed schema/API contracts are authorized by AD-13. AD-8/AD-14 and the recorded user direction explicitly permit version/model/timing/equipment/electrical/branding gates to remain open. These are not findings, and this review does not invent pinouts, electrical facts, package versions or measured thresholds.

## Findings

### R1 — Clarify ordinary motor stop versus latched protocol stop (closed; originally medium)

**Source:** TRD lines 130, 154–156 and 173–175; PRD FR-5/FR-8.

An ordinary input release/unrecognized gesture/conflicting direction stops movement but may leave the session Searching. The firmware contract then says “Stop/expiry invalidates the armed generation” and permits ARM through an “explicit backend recovery/start sequence.” It does not distinguish an ordinary release STOP from a fault/emergency STOP, or state whether the backend can run that ARM sequence while the same healthy session remains Searching. Two conforming-looking implementations could therefore differ: one permits normal release/reapply; another requires a recovery/start transition for every ordinary release.

**Consequence:** Independent backend and firmware implementers may disagree about the very common stop-and-drive-again path. No new timeout or hardware choice is needed to remove this uncertainty.

**Narrow resolution:** State whether an ordinary stop preserves the current armed generation, or explicitly permit a neutral-validated backend ARM handshake within healthy Searching after ordinary release. Preserve deliberate acknowledgment/Resume for emergency/path-failure latches and preserve stale-command rejection in either design.

This is a local protocol clarification rather than a reason to reject the chosen architecture. Resolve before freezing the software protocol state machine at T6.

### R2 — Specify idempotency storage for the independent settings mutation (closed; originally low)

**Source:** TRD lines 207–208, 242 and 251.

All mutations carry an action ID, while the sole documented receipt table is object-owned with an object FK and retention-cascaded receipts. Retention settings are independent of any object and survive object expiry. The contract does not say whether settings use the same durable action-ID replay semantics, a separate receipt mechanism or only settings-revision/preview guards. An empty installation also has no object to own such a receipt.

**Consequence:** API and persistence implementers could disagree about the result of retrying a successfully committed settings change after response loss, and about the lifetime of its deduplication record.

**Narrow resolution:** Define the settings replay behavior and its ownership/lifetime; for example, an explicit settings-scoped receipt or an explicit revision-based retry contract. Do not fabricate an object owner or retain deleted object data to support it.

No current requirement requires inventing an additional subsystem. Resolve when making the initial API/schema executable.

## Rubric coverage

| Dimension | Result | Evidence / assessment |
| --- | --- | --- |
| Enforceable decision form | Pass | AD-1–AD-14 each contain Binds, Prevents and Rule. They constrain concrete units, ownership and prohibited alternatives; they are not merely aspirational headings. |
| Architecture paradigm and ownership | Pass | One local authoritative FastAPI service; presentation-only Next.js; separate AI worker; backend-owned adapters and writes; independently expiring Uno permission. Dependency diagrams explicitly are not electrical diagrams. |
| Frontend | Pass | TRD 4 specifies surfaces, split workspace, image/ROI interactions, backend authority, pending outcomes, emergency stop, navigation/focus handling and accessibility. Branding and measured usable layout remain T4/T7. |
| Backend and concurrency | Pass | Single owner lock, controlling-browser lease, serialized logical mutations and writes, separate immediate safety revocation, latest-frame queues, session/generation/revision guards and terminal-action arbitration. |
| Domain and state | Pass | Exactly Lost/Found and Searching/Paused/Ended; separate end reasons and review/media lifecycles. Start/reject/confirm/Stop/restart/failure outcomes are explicit. Found is human-confirmed and cannot reopen. |
| Database and integrity | Pass; R2 closed | Logical schema, IDs/types, ownership FKs, global active-session uniqueness, bounds/transaction guards, migration refusal and durable transaction settings are defined. Settings receipt ownership and retry behavior were verified in the repair check. |
| Files/evidence | Pass | Durable image preparation, generated managed paths, checksums, journal, transactions, cross-store crash recovery and distinct missing/corrupt-media handling. No false assertion that SQLite makes file operations atomic. |
| API/events | Pass | Versioned REST groups, structured error classes, ordered snapshots/events, replay IDs, revisions, frame envelopes, independent video delivery and protected control lease. Exact executable DTOs can be derived without choosing an architectural alternative. |
| Device integrations | Pass | Webcam/controller/serial/camera/AI boundaries specify observations, generations, freshness and failure rules. Selected profile/protocol numbers are named T1–T6 gates, not guessed defaults. |
| Motion safety | Pass; R1 closed | Priority revocation, neutral/reapply, independent device expiry, stale/queued-command rejection, capture/display freshness and full physical 0.5-second budget are all explicit. Ordinary stop/rearm semantics were verified in the repair check. |
| Candidate review/suppression | Pass | Immutable frame/box evidence, pause before review, atomic decision, Not reviewed on Stop/interruption, human confirmation and continuity-only tracking distinguish matching from tracking while Paused. Tracking settings are a permitted T5 gate. |
| Retention | Pass | Registration-based formula; 1–30/default seven; preview/revision guard; no settings changes during active sessions; Searching/Paused grace until end; startup purge; read/action denial before delayed deletion; journaled physical cleanup and repair blocking. |
| Authentication | Pass / explicit platform boundary | No application login or accounts. Automatic per-launch capability is service protection; Windows account supplies local access context. |
| Authorization | Pass | Backend enforces state/mode/lease/revision/readiness/expiry and human review ownership; disabled buttons are not authority. Local protection remains required for emergency stop. |
| Multi-tenancy | Explicitly not applicable | Single operator/robot/installation. Same Windows account shares records. Cross-record FKs preserve integrity without adding tenants or account roles. |
| Security | Pass | Loopback listeners, exact origin/Host validation, capability protection, bounded inputs/decoding, safe media resolution/reparse handling, no static media root, protected configuration, asset hashes and local log boundaries. |
| Offline operation | Pass | Production Node and Python services, local assets/models/fonts/scripts, no cloud fallback or runtime hosted dependency; complete offline qualification is required. Local Wi-Fi availability is kept distinct from internet access. |
| Infrastructure/deployment | Pass | Prescribed hardware plus existing laptop/network; local production build/launcher; owner lock; Windows data root; schema/assets verification; disarmed startup/shutdown/upgrades; no unrequested cloud platform. |
| Operations/recovery | Pass | Startup reconciliation ends unfinished sessions Interrupted without undoing Found; missing dependencies actionable; service restarts never Resume; local readiness/diagnostics and release manifests. |
| Verification and performance | Pass | All SM/NFR targets map to whole-system tests. Stop includes actual failure detection and mechanical motion; live view includes rendering; false-positive scenes and five-object trial counts retained. No measurements or passing results are fabricated. |
| Procurement/electrical/route | Properly gated | T2 requires supervisor-reviewed exact variant/power/wiring/programming plan before procurement/assembly/energizing. T3/T6 preserve fixed-desk connected-room scope and timing; failures require explicit revision. |
| Traceability and scope | Pass | FR-1–FR-17, NFR-1–NFR-6 and all SMs are mapped; manual navigation, no automatic session duration, both controls, no autonomous obstacle functions or extra purchasing authority. |

## Gate conclusion

No fundamental contradiction with PRD scope/state/retention/offline/acceptance rules was found in the original review. ADs form an enforceable system spine and TRD covers all relevant system dimensions, with single-operator authentication/tenancy explicitly addressed rather than omitted. R1 and R2 are now closed by verified contract changes. Qualification and applicable assembly permissions remain pending at T1–T7.
