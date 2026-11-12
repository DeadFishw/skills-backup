---
name: work-like-i11usion
description: Implement an approved software or agent plan with strict scope control, small readable changes, deliberate edge handling, narrow-first validation, evidence-based reporting, and planner-review handoff. Use when `next_step.md`, another named implementation contract, or a precise current user instruction authorizes changes to code, tests, documentation, configuration, or project artifacts; planning-only and underspecified tasks route to `think-like-i11usion`.
---

# Work Like i11usion

## Outcome

Execute the approved behavior as the smallest maintainable change that satisfies its acceptance criteria. Favor simple code, explicit behavior, local reasoning, deliberate error handling, focused tests, and inspected evidence.

Finish with a developer report labeled pending planner review. Planner acceptance determines completion of the overall step.

Use this question to filter every change:

> Is this change necessary to satisfy the current plan, preserve required behavior, or validate the implementation?

Keep task-owned changes that pass this test within the current diff.

## Preconditions and Authority

Implementation begins with sufficiently specific scope from one of these sources:

- the user's latest precise implementation instruction;
- the approved `next_step.md`;
- another explicitly named implementation contract.

Read the applicable sources before editing:

1. the user's latest instruction;
2. repository and directory instructions such as `AGENTS.md`;
3. the active implementation contract;
4. relevant architecture and product documentation;
5. target source files, callers, and consumers;
6. relevant tests, fixtures, and runtime artifacts;
7. current version-control state;
8. prior reports and planner reviews for the same step.

Interpret project state consistently:

- The latest user instruction may amend current scope; record the amendment.
- `AGENTS.md` defines how work is performed.
- The current implementation contract defines what is implemented now.
- Source code and tests define current behavior.
- `stages.md` supplies strategic direction.
- `history_step.md` supplies prior rationale and outcomes.

When scope remains underspecified, or authoritative sources conflict on required behavior, pause implementation and return the decision to `think-like-i11usion`.

## Scope Lock

Extract four working lists from the approved scope:

- **Required Changes:** behavior and artifacts to add, remove, or modify.
- **Required Preservation:** interfaces, workflows, compatibility behavior, and invariants that remain stable.
- **Deliberate Non-Scope:** adjacent work reserved for another step.
- **Validation Obligations:** tests, commands, artifacts, and inspections required for handoff.

Use these lists throughout implementation and final diff review. A supporting refactor belongs in the task when it is necessary for the required behavior or its validation, remains local, and is explained in the developer report.

Preserve unrelated dirty work. When staging or committing is authorized, use exact pathspecs and inspect the staged path list before creating the commit.

## Execute the Plan

Read [references/implementation-workflow.md](references/implementation-workflow.md) before changing project files.

The execution loop is:

1. Trace the existing path from input through decisions, state, outputs, errors, consumers, and tests.
2. Extend the existing responsible boundary with the smallest coherent change.
3. Define the narrow observable check for the required behavior.
4. Implement in logical increments, inspecting the local diff and running the narrow check after each meaningful change.
5. Handle relevant edge and failure cases explicitly.
6. Preserve approved public behavior and update affected callers, tests, documentation, and migrations when the contract changes it.
7. Validate from narrow checks to affected broader checks according to risk and change surface.
8. Inspect the complete final diff against every acceptance criterion, preservation requirement, and deliberate non-scope item.
9. Update documentation for public behavior and durable non-obvious decisions.

## Implementation Quality

Prefer code that a reviewer can understand locally:

- small functions with one clear responsibility;
- explicit inputs, outputs, and control flow;
- descriptive names and shallow branching;
- deterministic behavior where practical;
- existing project patterns and ownership boundaries;
- standard-library or existing dependencies;
- state with clear ownership;
- errors close to their source with actionable context.

Introduce an abstraction when multiple real uses establish a shared contract or when the approved architecture requires it. A new dependency requires a concrete current benefit beyond existing facilities.

Tests should assert observable behavior and meaningful edge cases. Internal details belong in tests when they are themselves part of the contract.

## Evidence Discipline

Record exact commands and classify each result accurately:

- **Passed**
- **Failed**
- **Not run**
- **Unavailable**
- **Inconclusive**
- **Pre-existing failure**

Match each claim to its evidence environment: local, test, branch, staging, or production. Reserve production claims for production evidence. Verify a pre-existing failure and report it separately from task-owned regressions.

## Plan Deviations

Resolve incidental details with the simplest convention-compatible choice. Keep local necessary adjustments focused and explain them in the developer report.

A change to public interfaces, dependencies, persistence, architectural responsibility, migrations, security assumptions, or substantial scope returns to `think-like-i11usion` for approval. Record unrelated defects as follow-up candidates. Conflicting implementation evidence also returns to the planner for resolution.

## Developer Report and Review Handoff

Read [references/developer-report.md](references/developer-report.md) before reporting completed implementation work.

Produce one evidence-based developer report for each applicable implementation contract. Append it to the task-owned active plan when present; for instruction-only scope, include the same structured report in the final handoff. Use the status that reflects the observed state:

- **Implemented - Pending Planner Review**
- **Partially Implemented - Pending Decision**
- **Blocked**
- **Changes Addressed - Pending Re-review**

`think-like-i11usion` reviews the actual implementation evidence and records the planner verdict. Preserve earlier reports and reviews as history when work is revised.

## Completion

Implementation handoff is ready when:

- every approved behavior is implemented or a concrete blocker is established;
- relevant validation has run as far as the environment permits;
- exact results and evidence limits are recorded;
- the complete diff has been inspected for scope, correctness, readability, compatibility, and secrets;
- necessary documentation is current;
- the developer report is appended to the correct plan or included in the instruction-only handoff;
- planner review is requested.

Describe the work as pending planner review, then stop implementation.
