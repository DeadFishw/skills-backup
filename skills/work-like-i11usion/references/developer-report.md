# Developer Report and Planner Handoff

Use this reference after implementation and validation.

The developer report records what changed, what was checked, the observed results, scope compliance, and remaining limits. Planner review determines acceptance of the overall step.

Append the report after the approved content in each task-owned active plan. Preserve the approved criteria and earlier reports and reviews. For scope supplied only by the current user instruction, place the same structured report in the final handoff. If several active plans apply independently, append a separate report to each plan with its own acceptance evidence.

## Status Selection

- **Implemented - Pending Planner Review:** approved behavior and required validation are supported by the available evidence.
- **Partially Implemented - Pending Decision:** useful implementation exists and a decision is required to continue.
- **Blocked:** current evidence, environment, or authority blocks implementation or required validation.
- **Changes Addressed - Pending Re-review:** a prior planner review identified issues and the new evidence addresses them.

## Report Template

```markdown
## Developer Report - <date or execution identifier>

### Status

Implemented - Pending Planner Review |
Partially Implemented - Pending Decision |
Blocked |
Changes Addressed - Pending Re-review

### Summary

Describe the implemented behavior and its role in the system.

### Files Changed

- `path/to/file`: explain the relevant change.
- `path/to/test`: explain the behavior validated.

### Acceptance-Criteria Evidence

1. Criterion:
   - Implementation:
   - Evidence:
   - Result: Pass | Fail | Inconclusive

### Checks Run

- `<exact command>`
  - Result:
  - Relevant output:

### Scope Verification

State how the diff maps to the approved scope. Identify and justify supporting changes.

### Deviations From Plan

Describe each material or maintenance-relevant deviation. Write `None` when the implementation followed the plan exactly.

### Risks and Limitations

Describe unresolved behavior, unavailable validation, compatibility risk, and operational limitations.

### Artifacts

List generated artifacts and their locations when applicable.

### Version-Control State

- Commit: `<hash or absent>`
- Push: `<remote and branch status or pending>`
```

Use exact commands, paths, commit hashes, branches, and observed results. Distinguish task-owned failures from verified pre-existing failures and name the environment that supplied each result.

## Handoff Completion

The handoff is ready when:

- every acceptance criterion has implementation and evidence status;
- changed files and supporting changes are accounted for;
- command results and environment limits are explicit;
- deviations, risks, artifacts, and version-control state are recorded;
- the report is stored in the active plan or included in the instruction-only handoff;
- the status remains pending planner review or reflects the concrete blocker;
- `think-like-i11usion` is asked to inspect the plan, diff, tests, commands, and artifacts.

When implementation changes after review, append a new report tied to the issues addressed and retain the earlier evidence as history.
