# Lifecycle and roles

Read the [shared protocol](../../think-like-i11usion/references/workflow-protocol.md) for state, record, and verdict semantics. Use the project's existing contract; missing conventional folders are not a blocker when an authorized equivalent record exists.

## Resume from evidence

Inspect the active contract, latest reports/reviews, Git HEAD, index and relevant dirty hunks. Preserve a baseline sufficient to distinguish task edits from owner changes. Continue from the first incomplete authorized phase: planning, implementation, review, remediation, or closeout. Do not replace active unreviewed work or duplicate a partial closeout.

## Plan risk decision

The coordinator self-checks each plan. Require independent plan review when an unresolved high-impact risk remains: destructive migration or rollback, changed authorization/privacy policy, a new external effect, uncertain concurrency/failure semantics, or a similarly consequential untested assumption. Existing patterns or multiple files alone do not require another reviewer. Honor stricter project rules.

Record either the review with evidence and findings, or SKIPPED with the concrete risk assessment and reason. Resolve confirmed blockers before implementation. Missing required plan review is REVIEW_UNAVAILABLE and keeps implementation blocked unless the user expressly changes that gate within applicable policy. A planning-only request still stops after the requested planning/review work.

## Assign roles

- Coordinator: scope, authority, planning, evidence reconciliation and authorized closeout.
- Plan reviewer, when required: fresh read-only review of the plan and relevant source.
- Implementation owner: one active writer; use Work in strict mode. Give the approved contract, applicable instructions, exact writable scope, baseline, checks, report destination and stop conditions.
- Final reviewer: fresh read-only reviewer who did not author the plan, perform its independent plan review, or implement/remediate the change.

A separate subagent, external reviewer, or equivalent independently evidenced session can fill a reviewer role. A new role label in the same context is not independence. Record identities, evidence references, and phase outcomes. Honor project-specific delegation/model requirements; otherwise the coordinator may implement when no separate writer is required, while final review remains independent.

## Transfer a writer safely

Prefer continuity, but an unavailable former agent does not permanently block work. Preserve the contract, baseline, current diff/hashes, latest report, checks, unresolved findings, decisions, and next action. Confirm the previous writer has stopped, or isolate the successor in a separate checkout with an explicit integration owner. Record old/new identities and the transfer. The successor verifies the workspace against the handoff before editing. Preserve original scope, project role/model constraints, and exclusive write ownership; record a blocker only for a genuinely missing authority, unsafe overlap, or missing essential evidence.

## Verify and review

The coordinator checks the actual task diff, report claims and criterion evidence; reruns focused checks when needed. Give the final reviewer the approved baseline, exact implementation reference, reports, diff, validation artifacts, ownership notes, deviations and missing proof. Use Think's review procedure and the protocol's verdicts.

For CHANGES_REQUIRED, verify findings and route narrow corrections to the active implementation owner. Keep criteria stable. Fresh final review must cover the corrected evidence before acceptance; reuse reliable evidence for unchanged behavior.

If a required independent reviewer cannot be provided, state the limitation and gate. Already-authorized work before that gate may proceed; acceptance and approval-dependent closeout remain pending. If the user changes a gate, record it as a waiver/changed contract, not an independent pass; do not silently override a mandatory project policy.
