# Evidence review

Use [workflow-protocol.md](workflow-protocol.md) for record identity, criterion results, verdicts, and historical compatibility.

## Review a plan

Inspect the plan's assumptions against relevant source and constraints. Check whether scope is coherent, alternatives were meaningfully considered, criteria are observable, and risky behavior has direct evidence planned. Return the plan-review verdict and specific blocking findings. Review is advisory; it does not grant execution authority.

## Review implementation

Read the approved baseline and latest relevant developer report, then inspect the actual source, complete task-owned diff, tests, artifacts, and command evidence. For uncommitted work identify the exact patch or file hashes. Verify claimed commits and artifacts exist.

Assess every criterion as PASS, FAIL, or INSUFFICIENT_EVIDENCE. Check preserved behavior, related error paths, scope, and meaningful regression coverage. Passing broad tests cannot replace missing proof of a required behavior. Reuse trustworthy passing evidence for unchanged code; rerun focused checks when needed to resolve a finding.

Separate the original contract from developer-added status. A report cannot approve itself or weaken acceptance criteria. For multiple explicitly scoped plans, produce separate assessments. A missing report is an evidence gap, not permission to invent it.

Unrelated dirty work is non-blocking only if it predates or is outside the task, the implementation does not depend on it, and the contract does not require a clean workspace. Otherwise identify the unresolved ownership or dependency.

Return a compact record: review stage, reviewer identity, plan and implementation references, evidence inspected, criterion table, blocking findings, non-blocking notes, verdict, and next action. Each finding needs location, impact, evidence, and a concrete correction. Distinguish verified defects from suggestions.

Never describe self-review as independent review. When independence is required, a separate reviewer must inspect the evidence; inability to provide one is REVIEW_UNAVAILABLE. A standalone review may be performed by the current agent and must state its actual role.

Return the verdict and stop. Append a record or update status only when authorized. Review-only requests do not authorize implementation, archival, reset, commit, push, merge, or deployment.
