# Planning and Plan Review

Use this reference while creating, refining, or validating the active implementation plan.

## Establish Planning Authority

Read completely:

- every applicable repository instruction from the repository root to the target subtree;
- the project roadmap or stage document;
- the active plan;
- the planning history;
- each additional active-plan lane explicitly in scope.

Capture the initial Git branch, HEAD, merge base when relevant, index state, and dirty path list. For every dirty path that could enter the task scope, retain its pre-task diff or another exact baseline that supports later hunk ownership. Record which paths predate the task and preserve them.

Inspect the active plan from top to physical end. The current status, developer reports, and planner reviews determine the next lifecycle phase. Search history before replacing, superseding, or archiving anything.

## Inspect the Implementation Surface

Read the smallest relevant set of source, tests, migrations, architecture decisions, configuration, dependency files, artifacts, and runtime evidence required to plan accurately.

Identify:

- existing ownership boundaries and helpers;
- public contracts and behavior to preserve;
- authoritative data, time, identity, authorization, and failure sources;
- transaction, concurrency, retry, and rollback boundaries;
- sensitive-data, tenant-isolation, and privacy boundaries;
- process-global state and external-service dependencies;
- focused tests and representative legacy suites;
- workspace noise that implementation must preserve.

Classify important claims as source-backed fact, project decision, assumption, conflict, or open question.

## Select One Bounded Step

Choose the smallest dependency-ordered vertical slice that produces independently reviewable evidence and leaves the repository coherent.

A candidate usually needs splitting when it combines several high-risk domains, such as migration plus concurrency, external-service provisioning plus product behavior, policy plus delivery, multiple independent adapters, or a changed-file surface that cannot be reviewed as one contract.

Place later slices in non-goals. A roadmap stage remains context rather than implementation authority.

## Write the Plan

Follow the repository's required plan shape. Under the default convention, include:

- Title
- Status
- Summary
- Current state
- Goal
- Required functionality
- Non-goals / out of scope
- Acceptance criteria
- Testing requirements
- Likely affected files
- Implementation notes
- Definition of done
- Open questions
- Role ledger and plan-review record

Use `Proposed` in plan-only mode. In end-to-end mode, use a status such as `Authorized for implementation by direct workflow instruction` after the plan passes its self-review and any required risk review. Keep material owner decisions open and pause before implementation.

## Normative Invariants

List the small set of truths most likely to be lost during implementation and name each authority. Cover the applicable questions:

- Which component owns time, expiry, identity, authorization, and policy?
- What values and side effects constitute success or failure?
- Which tenant, principal, request, or policy bindings remain intact?
- Which transaction owns durable state and publication?
- Which data, locators, credentials, or identifiers may cross projections, logs, errors, and trust boundaries?
- Which public behavior remains stable?

Resolve material contradictions before implementation. Put unresolved owner decisions in `Open questions` with the exact decision needed.

## Risk and Dependency Register

For each material risk, record:

| Risk or failure mode | Boundary | Prevention or early gate | Evidence before broad testing | Owner or external dependency |
| --- | --- | --- | --- | --- |

Include external-service readiness, process-global restoration, test ordering, database freshness, cleanup, and generated configuration when relevant. Record configuration names and requirements while keeping credential values private.

## Acceptance-to-Evidence Matrix

Map every requirement and acceptance criterion to retained proof:

| ID | Planned behavior | Direct evidence | Edge or failure evidence | Verification phase |
| --- | --- | --- | --- | --- |

Use direct focused proof for risky behavior. Mark evidence that must be manual, live, production-specific, or currently unavailable.

## Implementation Checkpoints

Add checkpoints where risk warrants them:

1. **Contract checkpoint:** after interface and schema shape are drafted, review authority, time, identity, failure returns, transaction ownership, privacy, and environment isolation.
2. **Pre-broad checkpoint:** confirm focused checks, matrix coverage, fixture cleanup, process-global restoration, and infrastructure readiness before broad suites.

These checkpoints guide implementation and leave final acceptance to the independent final reviewer.

## Validation Ladder

Derive exact commands from the repository. Use available layers in this order:

1. focused tests for the changed boundary;
2. cross-suite isolation in one process, with the new suite first and representative legacy suites after it;
3. repository-wide fail-fast validation;
4. a complete fresh repository-wide suite after fail-fast is clean;
5. static, formatting, privacy, dependency, resource-cleanup, diff, and scope checks.

When database, broker, object storage, or another service matters, define disposable infrastructure, readiness checks, valid generated settings, and cleanup before implementation. Plans should name unavailable proof explicitly.

## Planning Self-Review

Confirm:

- one coherent step and one active authority;
- specific, testable requirements;
- evidence for every acceptance criterion;
- explicit preservation and non-goals;
- likely files grounded in inspected source;
- risk-first implementation ordering;
- focused and isolation checks before broad regression;
- correct mode and status;
- recorded plan-review trigger decision;
- one writer, coordinator verification, fresh final reviewer, remediation loop, and closeout contract;
- durable identities or session references for every assigned role;
- explicit owner gates;
- a planning-only diff during the planning phase.

Inspect the exact planning diff and run the narrow Markdown or diff check available for that file.

## Conditional Independent Plan Review

Require one fresh read-only reviewer when the step involves any of:

- migration, schema, durable state, rollback, transactions, or concurrency;
- authorization, privacy, tenant isolation, rights, policy, or sensitive data;
- external services, process-global configuration, generated infrastructure, or difficult isolation;
- multiple modules or public contracts;
- non-obvious authority, assumptions, failure semantics, or evidence mapping.

A localized low-risk step with clear authority, one boundary, and direct focused proof may skip this review. Append a durable `PLAN_REVIEW_SKIPPED` record with the trigger assessment, rationale, coordinator identity, and timestamp.

Give the reviewer the complete plan, applicable instructions, relevant source and test context, and dirty-worktree baseline. Require this output:

```text
PLAN_READY | PLAN_CHANGES_REQUIRED

Reviewer identity: <agent id, nickname, or session reference>
Reviewed at: <timestamp and timezone>
Trigger reason: <risk requiring review>

Blocking findings:
- Location:
- Finding:
- Required plan change:
- Evidence:

Non-blocking notes:
- Note:
```

The reviewer checks scope, authority, invariants, contradictions, acceptance coverage, edge evidence, implementation ordering, environment isolation, and validation gates. The reviewer remains advisory and read-only.

Append the result to the plan as a durable `Plan Review Record`, including reviewer identity, timestamp, trigger reason, verdict, findings, and coordinator disposition. If the required reviewer is unavailable, append `PLAN_REVIEW_UNAVAILABLE` and keep implementation blocked.

The coordinator verifies every finding against source, incorporates plan-aligned corrections, records the disposition, and repeats the planning self-review. Continue by mode when blocking findings are resolved; request owner input when a finding exposes a material owner decision.
