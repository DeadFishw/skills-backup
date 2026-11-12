# Implementation and Evidence

Use this reference after the plan is authorized and any required plan review is resolved.

## Delegate One Writer

Give exactly one implementation writer:

- the complete authorized plan;
- applicable repository instructions;
- exclusive writable files or subtree;
- required behavior, preservation rules, and non-goals;
- initial branch, HEAD, index, and dirty-worktree baseline;
- exact validation ladder and evidence expectations;
- developer-report format;
- recorded writer identity or session reference;
- material decision and scope stop conditions.

The writer may edit the authorized files, add or update tests and documentation within scope, run checks, and append a developer report to the active plan. The writer leaves final planner review, history archive, plan reset, staging, commit, push, release, and completion claims to the coordinator.

Additional agents have disjoint read-only assignments. The recorded writer owns every task file through implementation and remediation. Shared schemas, migrations, public contracts, transaction state machines, and final integration retain that single editing owner.

## Writer Execution Contract

The writer should:

1. trace the existing behavior and ownership boundary;
2. implement the smallest coherent plan-aligned change;
3. establish focused direct evidence for each required behavior;
4. reach authority, privacy, transaction, concurrency, environment, and failure risks early;
5. inspect the local diff after meaningful increments;
6. run the planned validation ladder in order;
7. preserve unrelated work and process-global state;
8. update public documentation and durable decisions supported by the implementation;
9. inspect the final task-owned diff;
10. append the developer report at the physical end of the active plan.

Incidental details use the simplest repository-compatible choice. A local supporting change belongs in scope when required for an acceptance criterion and is recorded in the report. Material public-interface, dependency, persistence, architecture, migration, security, policy, or scope changes return to the coordinator.

## Evidence Status

Classify each check accurately:

- Passed
- Failed
- Not run
- Unavailable
- Inconclusive
- Verified pre-existing failure

Name the environment that produced the evidence: local, isolated test, branch, staging, or production. Reserve production claims for production evidence. Keep source outages, unavailable infrastructure, cleanup failures, and known baseline failures visible.

## Developer Report

Append a report using the repository format or this default:

```markdown
---

## Developer Implementation Report - <timestamp and timezone>

**Status:** <IMPLEMENTED | PARTIAL | BLOCKED>
**Writer identity:** <agent id, nickname, or session reference>
**Implementation reference:** <workspace, branch, patch, or commit>
**Baseline:** <branch, HEAD, merge base when relevant>

### What changed

- <file or behavior change>

### Acceptance-criteria evidence

| Criterion | Implementation | Direct evidence | Result |
| --- | --- | --- | --- |

### Tests and validation

- `<exact command>`: <result and relevant output>

### Proof artifacts

- <artifact path or None>

### Deviations from plan

- <deviation or None>

### Risks and missing evidence

- <risk, unavailable check, or None>

### Dirty workspace and scope

- <task-owned paths, unrelated preserved paths, index state>

### Version-control state

- Commit: <hash or absent>
- Push: <remote status or pending>
```

Preserve previous reports and planner reviews. A remediation appends a new report tied to the blocking review findings.

## Coordinator Verification

After the writer returns, the coordinator directly inspects:

- the active plan from title through the latest report;
- actual changed files and complete task-owned diff;
- pre-task diffs for task-touched paths that were already dirty;
- branch, HEAD, merge base, and index state when relevant;
- each implementation claim at its source;
- focused tests and what they assert;
- acceptance-to-evidence matrix coverage;
- edge, error, regression, isolation, and live-proof gaps;
- artifacts and their exact contents or existence;
- unrelated dirty files and scope boundaries;
- documentation, dependency, and generated-file changes;
- reported unavailable or pre-existing failures.

For a task-touched file that was dirty at baseline, separate the pre-task owner diff from the task delta and determine whether their hunks overlap. Preserve the baseline evidence for closeout. Treat an inseparable overlap as a staging blocker rather than assigning the whole path to the task.

Rerun the highest-signal focused checks when feasible. Use broader evidence according to the plan's validation ladder. A green broad suite cannot substitute for missing direct proof of a risky requirement.

## Prepare the Final Review Package

Give the final reviewer:

- the planning baseline and unchanged acceptance criteria;
- every developer report relevant to the current implementation reference;
- actual diff and changed-file set;
- exact test commands, results, and environment;
- artifacts and manual/live evidence;
- deviations, risks, skipped or unavailable checks;
- dirty-worktree and scope assessment;
- durable role ledger showing distinct plan reviewer, writer, and final reviewer assignments;
- coordinator verification findings;
- any prior final-review findings and remediation evidence.

List missing or unverifiable evidence explicitly.

## Bounded Remediation

For `CHANGES_REQUIRED`:

1. verify each blocking finding against source and plan authority;
2. send only confirmed blocking findings and required proof to the same writer;
3. retain the authorized scope and acceptance criteria;
4. permit the narrow code, test, documentation, or artifact changes required by those findings;
5. rerun affected focused and preservation checks;
6. append a remediation report;
7. request a fresh independent final review.

Confirm that remediation returns to the writer identity recorded in the latest developer report. If that writer is unavailable, keep the lifecycle blocked. A different writer begins only through a separately authorized superseding workflow that preserves the current plan, reports, reviews, and blocker as history.

For `BLOCKED_NEEDS_MORE_INFO`, gather the named evidence or request the material owner decision. Resume at final review after the blocker is resolved.
