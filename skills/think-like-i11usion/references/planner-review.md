# Planner Review

Use this reference after implementation to review actual evidence against the approved plan.

## Evidence to Inspect

Inspect, as applicable:

- the approved current plan;
- the developer report appended to it;
- the actual diff and relevant source files;
- tests added or changed and what they assert;
- exact command results;
- generated artifacts;
- unresolved warnings or failures;
- commit and push state when those are part of the plan.

Use the developer report as an evidence index and confirm its claims through inspection. Distinguish local, test, branch, staging, and production evidence, and reserve production claims for production evidence.

## Review Method

Assess every acceptance criterion individually as **Pass**, **Fail**, or **Insufficient Evidence**. For each assessment, name the inspected evidence and explain the finding.

Also verify:

- all required behavior is present;
- preserved behavior and public interfaces remain intact;
- the implementation remains within the approved scope;
- applicable project instructions were followed;
- tests assert the required behavior and meaningful edge cases;
- reported commands and outcomes are supported;
- deviations and unresolved warnings are disclosed;
- documentation matches actual behavior.

Keep the approved criteria stable during review. When an approved requirement genuinely changed during implementation, document that change separately before assessing the revised criterion.

If multiple plan documents are independently active, review each against its own criteria and append a separate verdict for each plan.

Append the review after the corresponding developer report when the task authorizes updating the plan. Check for an existing review of the same evidence before appending.

## Verdicts

- **Accepted:** every required criterion is supported by sufficient evidence and the implementation remains within the approved scope.
- **Changes Required:** the implementation is substantially present, but one or more correctable criteria are unmet.
- **Blocked:** necessary evidence is unavailable, authoritative sources conflict, validation remains incomplete, or a fundamental plan assumption is invalid.

Assign **Blocked** when required evidence is missing.

## Recommended Review Shape

```markdown
## Planner Review — <date or review identifier>

### Verdict

Accepted | Changes Required | Blocked

### Evidence Reviewed

- Plan sections examined.
- Diff and files inspected.
- Commands and results verified.
- Artifacts inspected.

### Acceptance-Criteria Assessment

1. Criterion: Pass | Fail | Insufficient Evidence
   - Evidence:
   - Finding:

### Scope Assessment

State whether the implementation remained within scope and preserved required behavior.

### Issues

List concrete defects, omissions, unsupported claims, warnings, or deviations.

### Required Next Action

State the smallest action needed to close the review.
```

## Review Completion Check

Review is complete when:

- actual implementation evidence has been inspected;
- every criterion has an explicit assessment;
- scope and preserved behavior have been checked;
- missing or environment-limited evidence remains visible;
- the verdict is supported by the evidence;
- the authorized review is appended once to the correct plan for the inspected evidence set;
- the smallest required next action is stated.

Then stop.
