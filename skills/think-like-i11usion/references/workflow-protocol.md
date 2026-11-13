# Workflow protocol

This is the shared authority for records and vocabulary used by Think, strict Work, and the coordinator. Ordinary Work needs no planning files or status records.

## Authority and locations

The current user request defines authorized scope; applicable project instructions define execution conventions. An approved contract defines desired behavior; source and tests establish current behavior. Roadmaps and history are context, not new implementation authority.

Use the user's named artifact, then the project's declared active artifact. Preserve existing paths, formats, and vocabulary when tools or project rules depend on them. If none exists and durable planning is authorized, propose `docs/planning/next_step.md` with `docs/planning/history_step.md`; a local task file or existing issue-based contract is also valid. Creating or editing remote issues requires its own authorization. Do not initialize a planning directory just because a skill was loaded.

Recognize `next_step.md`, `next_step2.md`, and `next_step_2.md` as possible existing lanes; do not rename them. Include only explicitly scoped lanes. If two plausible authorities conflict, resolve the ambiguity before acting. Read an active record fully; search relevant history instead of rereading its entirety.

A retained record needs: stable task ID, scope and preservation requirements, acceptance criteria, approval source, validation plan, current state, latest implementation reference, and reports/reviews. Record names and requirements, never credential values.

## Shared states

Use these for new records; state is not a review verdict.

| State | Meaning |
| --- | --- |
| PROPOSED | Plan exists; implementation is not authorized. |
| READY | In-scope implementation is authorized and required plan gates passed. |
| IMPLEMENTING | Authorized implementation is in progress. |
| PENDING_REVIEW | Implementation evidence awaits required review or re-review. |
| CHANGES_REQUIRED | Confirmed blocking findings need correction. |
| BLOCKED | A named decision, evidence source, or required capability is missing. |
| ACCEPTED | Required review passed; authorized closeout may remain. |
| CLOSED | All closeout actions required and authorized for this task are verified. |

Record the prior phase and exact next action with BLOCKED. Resuming uses actual evidence, not status alone. An explicit full-workflow request can authorize the resulting in-scope plan; READY still requires the applicable risk gate. An approved plan's existence alone does not authorize implementation when the current request is review-only.

## Evidence and verdicts

Criterion results: PASS, FAIL, INSUFFICIENT_EVIDENCE.
Check results: PASSED, FAILED, NOT_RUN, UNAVAILABLE, INCONCLUSIVE, VERIFIED_PREEXISTING_FAILURE. Name the environment and exact command or artifact.

The verdict set is shared by plan and implementation review; always label the stage:
- APPROVED: all required criteria for that stage are PASS with sufficient evidence; no blocking findings remain.
- APPROVED_WITH_NOTES: approval with only non-blocking follow-ups.
- CHANGES_REQUIRED: a demonstrated, correctable blocking defect.
- BLOCKED_NEEDS_MORE_INFO: necessary evidence or authority is insufficient.
- REVIEW_UNAVAILABLE: a required independent reviewer cannot be provided.

A plan approval is never implementation approval. Implementation approval moves to ACCEPTED; changes move to CHANGES_REQUIRED; insufficient evidence or reviewer capability moves to BLOCKED. Do not label a waived independent gate as passed.

## Compact reports and updates

A developer report records writer identity, baseline and implementation reference, changed behavior, criterion-to-evidence mapping, exact checks/results, deviations, missing proof, and dirty-work ownership. In strict mode it hands off at PENDING_REVIEW. No repeated full plan or raw log dump is required.

A review records stage, reviewer identity and independence, reviewed references, criterion results, findings and verdict. Bind each record to the exact evidence version. Changed implementation invalidates approval of the changed behavior; obtain the required re-review.

When writing is authorized, append reports after the current record and update only the top state summary. Preserve previous contracts and reports. Avoid duplicate reviews of the same stage and evidence unless requested. Superseding an active plan needs explicit authority and a truthful preserved record.

## Compatibility

Interpret legacy labels without rewriting history:
- Proposed / Planned -> PROPOSED unless a separate approval source is verified.
- Owner-approved / Authorized for implementation -> READY after required gates.
- IMPLEMENTED / Implemented / Implemented - Pending Planner Review / Changes Addressed - Pending Re-review -> PENDING_REVIEW, never automatic acceptance.
- Accepted / Approved / Approved with notes -> the corresponding approval verdict only when a real review of the current evidence exists.
- PLAN_READY / PLAN_CHANGES_REQUIRED -> APPROVED / CHANGES_REQUIRED at the plan stage.
- PLANNER_REVIEW_UNAVAILABLE / PLAN_REVIEW_UNAVAILABLE -> REVIEW_UNAVAILABLE at the stated stage.
- Incomplete / Rejected -> CHANGES_REQUIRED when blocking findings exist.
- Superseded / Replaced / Cancelled are historical dispositions, not successful implementation.
- Cleared / Awaiting planning means no active plan; verify history and required closeout before treating the preceding step as CLOSED.

For a legacy project, keep its required headings and status spelling; record the canonical interpretation in the new report if needed. Preserve stricter project gates, model constraints, and stage/implementation identifiers.

Retired skill names in project instructions are role aliases:
- `prepare-development-step`: Think for a planning-only request; the coordinator for a required or explicitly requested lifecycle.
- `planner-doc-review`: Think for evidence review; the coordinator owns separately authorized closeout.
- `karpathy-guidelines`: Work's implementation discipline; Think's evidence review for review-only work.

This mapping replaces the skill identity, not the project's substantive requirements. Do not reactivate an archived skill to satisfy the alias.
