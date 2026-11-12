---
name: plan-review-implement-review
description: "Run one Git repository development step through a gated plan-review-implement-review lifecycle: reconstruct durable planning state, write or refine one bounded plan, conditionally obtain independent plan review, delegate one implementation writer, verify workspace evidence, obtain independent final review, remediate with the same writer, and close approved work through archive/reset and a focused commit. Use only when the user explicitly requests this lifecycle or repository instructions mandate it in a project with durable active-plan and history artifacts plus commit-based closeout; plan-only requests stop after planning and risk-based plan review, while ordinary direct edits use their normal workflow."
---

# Plan Review Implement Review

## Outcome

Move one bounded repository step through a durable, auditable state machine:

```text
plan -> risk-based plan review -> implement -> verify -> independent final review
     -> bounded remediation when required -> approval-gated closeout
```

Completion means the approved plan, implementation evidence, planner verdict, archive/reset state, and focused commit agree. Push, merge, release, deployment, and other external mutations require their own authorization.

## Discover the Project Contract

Read every applicable repository instruction before selecting files or roles. Use the project's named planning artifacts. When the project follows the default convention, use:

- roadmap: `docs/planning/stages.md`;
- active plan: `docs/planning/next_step.md`;
- history: `docs/planning/history_step.md`.

Include another active-plan lane only when the user or repository instructions place it in scope. Treat roadmap documents as strategic context, the approved active plan as implementation authority, and history as durable evidence.

Verify that the repository already defines, or the owner explicitly authorizes, equivalent durable active-plan, history, and focused-commit closeout artifacts. Repositories governed only through issues, pull-request descriptions, ephemeral chat, or a no-autonomous-commit policy use their ordinary workflow unless the owner first establishes an equivalent contract.

Capture `git status --short` before planning. Preserve every unrelated or owner-modified path throughout the lifecycle.

## Select the Mode

### Plan-only

Use when the user asks only to propose, refine, validate, or review a plan. Create or update the planning artifact, perform the planning self-review, run the risk-based plan review when triggered, report the result, and stop.

### End-to-end

After this skill's lifecycle trigger is satisfied, use end-to-end mode when the user asks to implement, develop, continue one reviewed step, or run the complete workflow. A generic direct-edit request does not activate this mode. The explicit lifecycle request or repository mandate authorizes the resulting self-reviewed in-scope plan and its repository-local implementation, so routine intermediate plan approval is unnecessary.

Pause for the owner when a material product, privacy, rights, policy, production, external-authority, irreversible migration, or scope choice remains unresolved. The end-to-end request supplies workflow authorization and does not supply missing domain authority.

## Resolve the Current State

Inspect the active plan's top status, appended developer reports, appended planner reviews, history, and Git evidence before writing.

| Observed state | Continue with |
| --- | --- |
| Cleared after approved archive | Create one new bounded plan. |
| Proposed plan | Refine it; stop in plan-only mode or authorize it in end-to-end mode after planning gates pass. |
| Owner-approved active plan | Preserve it and continue with its authorized scope. |
| Implementation report awaiting final review | Verify the workspace evidence and begin independent final review. |
| `PLAN_CHANGES_REQUIRED` | Revise the plan, rerun planning checks, then continue by mode. |
| `CHANGES_REQUIRED` | Return confirmed blocking findings to the same implementation writer. |
| Missing evidence or material owner decision | Gather the evidence or request the decision. |
| Approved but partially closed | Resume idempotent closeout from the first incomplete gate. |
| Archived and reset with no verified focused commit containing the reviewed paths | Resume partial closeout and verify completed gates. |
| Archived, reset, and included in a verified focused commit | Treat the step as closed and begin another step only under a new request. |

Preserve active, reviewed, and historical records. A new plan begins only after the previous lane is cleared or explicitly superseded by owner authority with truthful history.

## Role Contract

- **Coordinator:** owns planning, authority decisions, task decomposition, evidence reconciliation, final changed-file inspection, closeout, and user reporting.
- **Conditional plan reviewer:** a fresh read-only agent used for risky plans. It returns `PLAN_READY` or `PLAN_CHANGES_REQUIRED` and never implements or performs final review.
- **Implementation writer:** exactly one bounded writing agent identity for the entire step, including remediation. It owns the authorized write set, executes validation, and appends developer reports. It leaves final review, archive/reset, staging, commit, and completion claims to the coordinator.
- **Final planner reviewer:** a fresh independent read-only agent that neither implemented the change nor reviewed the plan. It assesses the authorized plan against actual workspace evidence.

Additional agents may gather disjoint read-only evidence. Each writing assignment has an exclusive file set. If the required role separation cannot be provided, report that workflow blocker rather than collapsing independent roles.

Record a durable role ledger in the active plan: coordinator identity or session reference, conditional plan reviewer identity or skip status, implementation writer identity, final reviewer identity, and each phase timestamp. On resume, route remediation to the recorded writer. If that writer is unavailable, keep the current lifecycle blocked. A different writer requires a separately authorized superseding workflow that preserves the current plan and reports as history.

## Lifecycle

### 1. Plan

Read [references/planning-and-plan-review.md](references/planning-and-plan-review.md). Reconstruct current behavior, choose one dependency-ordered vertical slice, write the durable plan, map acceptance criteria to evidence, and classify whether independent plan review is required.

### 2. Review the Plan When Risk Requires It

Use one fresh read-only reviewer for work involving durable state, migrations, concurrency, authorization, privacy, external services, process-global configuration, multiple public contracts, or non-obvious failure semantics. Resolve source-backed findings in the plan before implementation. A localized low-risk plan may skip this review with a recorded rationale.

### 3. Implement with One Writer

Read [references/implementation-and-evidence.md](references/implementation-and-evidence.md). Give the writer the authorized plan, applicable instructions, exclusive write scope, non-goals, dirty-worktree baseline, validation ladder, developer-report format, and stop conditions.

### 4. Verify Directly

After the writer returns, inspect the actual diff, changed-file set, plan report, artifacts, and test outputs. Map evidence back to every requirement and acceptance criterion. Rerun the highest-signal focused checks when feasible. Worker narrative is an index to evidence.

### 5. Obtain Independent Final Review

Read [references/final-review-and-closeout.md](references/final-review-and-closeout.md). Give the fresh reviewer the planning baseline, latest developer report, actual diff, validation evidence, dirty-worktree notes, deviations, and missing evidence. Require one verdict:

- `APPROVED`
- `APPROVED_WITH_NOTES`
- `CHANGES_REQUIRED`
- `BLOCKED_NEEDS_MORE_INFO`
- `PLANNER_REVIEW_UNAVAILABLE`

### 6. Remediate Through the Same Writer

For `CHANGES_REQUIRED`, verify the findings, return the confirmed blocking items to the original writer, permit plan-aligned changes, rerun affected evidence, append a new developer report, and request a fresh independent review. Keep the approved plan stable through remediation.

For `BLOCKED_NEEDS_MORE_INFO`, gather the missing evidence or request the required owner decision before another review.

### 7. Close Approved Work

Only `APPROVED` or `APPROVED_WITH_NOTES` opens closeout. The coordinator appends the review, updates status, archives the full reviewed plan, verifies any history-menu link and unique anchor, resets the active plan, inspects the final diff, isolates task-owned hunks from the initial dirty baseline, stages the verified task-owned delta, and creates one focused commit.

Closeout remains incomplete until the commit succeeds. Preserve unrelated dirty files and keep push or release actions outside this workflow unless separately authorized.

## Invariants

- One active planning lane contains one coherent implementation step.
- Roadmap proximity never expands current implementation scope.
- Material owner decisions remain explicit gates.
- Risk review reaches authority, privacy, transaction, concurrency, environment, and failure semantics before broad testing.
- Every acceptance criterion maps to retained evidence and relevant edge evidence.
- Plan review, implementation, and final review use distinct roles.
- Final review evaluates actual source, diff, tests, artifacts, and environment limits.
- Remediation preserves the approved contract and historical reports.
- Approved history is archived exactly once; menu rows, anchors, and archive entries are idempotent.
- Baseline-aware hunk ownership, selective staging for overlapping dirty files, and staged-diff inspection protect unrelated work.

## Success Conditions

Plan-only mode succeeds when one source-grounded plan is ready, its risk-review decision is recorded, required plan findings are resolved, and implementation has not begun.

End-to-end mode succeeds when the authorized plan passes required plan review, one writer implements it, the coordinator verifies actual evidence, a fresh independent reviewer approves it, closeout archives and resets the plan safely, and the focused commit succeeds.
