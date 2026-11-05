# Adversarial consistency gate — independently implemented seams

Reviewed: the run's `ARCHITECTURE-SPINE.md` and `docs/TRD.md`, 2026-11-05. Read-only review of the design; only this review artifact was written. No implementation, hardware, timing or package qualification was performed.

Current verdict after scoped repair verification: **PASS — S1–S3 closed at the documentation level**. The original findings below are retained as review history and are superseded by the closure assessment. This is not implementation, schema-generation, hardware or timing qualification.

## Repair verification — 2026-11-05

Scope: reread only the repaired ordinary-rearm, action-receipt, shared application-contract and WebSocket-protection provisions in current `docs/TRD.md`. No new broad review or source-document edits were performed.

- **S1 closed:** Section 6.3 (`docs/TRD.md:175`) now expressly permits a new generation/ARM handshake after ordinary release/recognition stop during otherwise healthy Searching, requiring neutral then fresh hold without Pause/Resume. It expressly excludes emergency, command expiry and required-path failure from that path. This reconciles firmware generation invalidation with ordinary held controls while preserving fault recovery and stale-packet rejection. Exact protocol/timing qualification remains T6.
- **S2 closed:** The receipt schema (`docs/TRD.md:208–209`) now has constrained Object/Settings scope, exactly one matching owner, and no session for Settings receipts. Settings receipts survive object expiry without storing object data. Section 9.1 (`:245`) checks existing matching receipts before stale revisions and identifies settings as the retention revision scope. This represents an idempotent retention write even when no objects exist.
- **S3 closed:** Section 9.1 (`docs/TRD.md:245–279`) defines action names, resource revision scopes, required payload fields, explicit acquire/release/takeover, returned lease/control-generation identity, runtime request deduplication, snapshot/event fields, occurrence-based failure IDs, heartbeats and frame acknowledgment fields. FastAPI owns REST/OpenAPI plus event/frame schemas and generated frontend types, with an explicit freeze before separate implementation (`:255`). The binary frame envelope is structurally specified (`:275`); numeric limits remain T6. Section 10 (`:301`) supplies a browser-compatible protected handshake using an authorized HTTP-issued scoped single-use ticket offered in subprotocols while selecting only `laf.v1`, keeping secrets out of URLs and negotiated protocol output. These provisions resolve the independent-unit disagreement and identify where generated schemas become authoritative; they do not claim those schemas already exist.

No concrete new contradiction was found in these repairs. The remaining original no-finding observations and authorized T1–T7 deferrals are unchanged. The review gate passes for these three structural seams; implementation must still generate/freeze the owned schemas and perform the stated checks and qualification.

## Original findings — closed by the repairs above

### S1 — P2: ordinary input release has no defined firmware rearm path

Evidence: `docs/TRD.md:130`, `:153–159`, `:173–175`; spine AD-5/AD-10.

The domain contract permits ordinary release/ambiguity to stop movement while remaining Searching. A later fresh held direction should therefore work during that session. The firmware contract invalidates its armed generation on **Stop/expiry**, then permits ARM only through an explicit backend **recovery/start** sequence with neutral input. Ordinary input release is neither a new session Start nor a latched-failure recovery, and the TRD does not specify another rearm transition.

Two compliant units diverge: firmware invalidates the generation whenever the backend sends STOP for a released D-pad; the backend preserves the Searching session and, after the next fresh press, sends a renewed movement command in the existing generation. Firmware must reject it. A backend that instead starts a recovery sequence may introduce an acknowledgment/Resume requirement after every release, changing the ordinary held-control behavior.

Resolve this structurally: distinguish a non-latching neutral output command from a stop that invalidates permission, or expressly define a neutral-to-ARM handshake for ordinary release while Searching. Specify how that path differs from emergency/path-loss recovery and how a previous queued hold cannot rearm it. Exact encoding, deadlines and packet sizes can remain T6.

### S2 — P2: mandatory durable action receipts cannot represent retention-settings writes

Evidence: `docs/TRD.md:207–208`, `:222`, `:230`, `:242`, `:251`; spine AD-7/AD-13 and identity/concurrency convention.

Mutations carry action IDs, durable receipts are the retry mechanism, and the required `action_receipts` schema has an owner `object_id` FK. Retention settings are a singleton independent of objects and survive their expiry. A successful retention change can legitimately happen with no objects at all. The schema offers no owner for its receipt and no independent settings receipt mechanism.

Two compliant units diverge: the frontend retries a lost successful PUT using the original action ID and expected settings revision; the backend either cannot store its receipt, rejects the retry as a stale revision, or attaches it to an arbitrary object whose later purge destroys the settings action's receipt. A separate implementation may silently omit durable idempotency for settings. These disagree on the promised retry behavior and lifecycle.

Define a settings-owned receipt or a constrained owner/discriminator model, including result revision and replay semantics independent of object expiry. Preserve the deliberate object-linked purge rule for object/session actions. Also state that a matching committed receipt is checked before ordinary stale-revision rejection; conflicting reuse still fails. No runtime benchmark or hardware gate resolves this schema issue.

### S3 — P2: controlling-client acquisition and shared control payloads have no common structural contract

Evidence: `docs/TRD.md:95`, `:111`, `:143`, `:204`, `:242–258`, `:276`, `:280`; spine AD-13.

The required control lease, explicit acquisition/transfer, failure IDs, recovery acknowledgment, revision checks and snapshot recovery are sound invariants. The endpoint table and logical database schema do not define their shared message shapes. In particular, there is no specified acquisition request/response or event message, no lease identity/generation field in the ordinary action envelope, and no structural snapshot/failure/acknowledgment schema. `pause_causes` is named without a representation despite actions requiring named failure IDs. T6 expressly owns serial/video encoding and timing, but no equivalent ownership step is identified for these application contracts.

Two compliant units diverge: the UI opens `/events` and sends an explicit `acquire-control` message expecting a lease in its snapshot; the backend expects an acquisition REST call or an acquisition field in the heartbeat and rejects that message. Both obey the stated explicit-acquisition rule, yet cannot establish the first protected control action. Likewise, one unit can treat `expected_revision` on acknowledgment as the durable session revision while another requires a recovery-context revision and failure occurrence IDs. Versioned but unspecified typed payloads do not settle that difference.

Add one authoritative application-contract source (a compact schema or named versioned contract artifact is sufficient) for control acquisition/transfer/release, lease/session generations, action discriminants and revision scope, snapshot fields, failure occurrences/acknowledgments, and ordered event payloads. Reference it from the TRD so frontend, backend and worker implementations share it. It need not freeze T4–T6 numeric thresholds or every internal table/storage encoding. Until then, identify this as required contract derivation rather than claim the endpoint/schema seed already supports independent implementation.

## Seams challenged without an additional finding

- **Terminal revisions and retries:** First valid terminal commit wins, a committed Found is preserved, and immediate emergency revocation is separated from disk/revision handling. This is coherent. Implementations must preserve the specified expired/missing response after grace ends rather than reconstruct a purged action; that is an explicit policy, not an idempotency defect. S2 addresses the genuinely unrepresentable settings owner.
- **Video capture age and display acknowledgment:** The conservative source-age bound, camera epoch invalidation, bounded latest-frame delivery, frame-specific boxes and displayed-frame acknowledgment can coexist. A backend can conservatively age an acknowledged frame using its mapped capture time and its own clock; unrelated clock subtraction is expressly forbidden. Exact uncertainty budgets, acknowledgment fields/encoding and clock exchange are deliberately T6. No claim is made that the example firmware already satisfies them.
- **Retention grace and terminal evidence:** Grace covers only the existing Searching/Paused session and disappears at Ended, including a successful Confirm or Stop. Immediate post-terminal inaccessibility of already expired evidence is therefore intentional. Startup ending interrupted sessions before purge is also explicit. The filesystem journal/preparation ordering and reconciliation avoid asserting an impossible SQLite/filesystem atomic transaction. Durable file/SQLite settings and platform validation remain required; no silent success is permitted for missing/corrupt evidence.
- **Firmware boot/challenge freshness:** Device-issued expiring challenges, device-monotonic deadlines, boot generations, strictly increasing sequences and nonblocking expiry are a feasible structural basis for rejecting delayed packets. Numeric challenge windows, baud rates, framing and the measured physical budget remain T6. S1 concerns the missing ordinary release transition, not those authorized deferrals.
- **Next/FastAPI bootstrap:** A direct cross-origin loopback bootstrap can carry the exact frontend Origin, validate Host and return a no-store in-memory capability without a login. Browser-compatible WebSocket capability delivery must be selected without a URL token or secret logging, but no unavoidable contradiction follows from that requirement: a handshake subprotocol is one possible mechanism. Bootstrap need not rely on a same-origin request that omits Origin. Initial navigation to Node is not itself a control/bootstrap action. This gate does not demand a new login, public hosting or framework default.
- **Remaining logical schema:** Object/session/candidate/media ownership and the non-cascading purge journal are consistent. Exactly-one-reference and cross-table bounds may be enforced by the expressly required serialized transactional guards. The review does not mistake an initial logical schema for already executed migrations. S3 concerns the external shared contract, not arbitrary internal representation choices.

## Authorized open gates and scope

Exact versions/model hashes, numeric recognition/continuity thresholds, clock/lease/watchdog budgets, electrical wiring/power compatibility, prescribed-board programming access, laptop/controllers/network/route, measured stop/video/endurance behavior and branding remain T1–T7. Alisa explicitly authorized documentation completion with those gates open and authorized high-level design plus detailed API/schema derivation. They are not findings, and this report neither invents their values nor treats them as qualified. Resolving S1–S3 completes structural contracts while leaving those decisions at their approved gates.
