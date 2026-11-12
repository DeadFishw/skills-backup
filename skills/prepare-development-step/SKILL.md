---
name: prepare-development-step
description: Prepare, refine, validate, or execute one narrow development step in this repository. Use when the user asks to propose the next step, turn a goal into docs/planning/next_step.md, check implementation readiness, or run the complete plan to implementation-worker to independent-planner workflow. Risky plans receive a conditional read-only subagent review before implementation. Approved closeout must archive the reviewed plan and add its linked entry to the history_step.md menu. A direct end-to-end request authorizes the generated plan without an intermediate approval pause; a plan-only request stops after planning. Never bypass unresolved owner decisions or the final planner review.
---

# Prepare and Run Development Step

## Purpose

Turn a development objective into one narrow, source-grounded, testable
`docs/planning/next_step.md`, then either return the plan or drive it through
conditional plan review, implementation, and independent final review according
to the user's requested mode.

This skill owns planning and end-to-end orchestration. It does not replace
`planner-doc-review`, which owns final post-implementation review, the linked
history menu and archive entry, reset, and the focused commit. A direct request
to run the complete workflow authorizes
the resulting in-scope plan; it does not authorize an unresolved product,
privacy, rights, policy, or scope-expansion decision.

## Mode and authority

- Use **plan-only mode** when the user explicitly asks only to propose, refine,
  validate, or review a plan. Produce the planning artifact and stop without
  requesting approval of the plan.
- Use **end-to-end mode** when the user asks to implement, develop, continue a
  goal, or run the complete workflow. Treat that direct instruction as owner
  authorization for the resulting plan and continue without an intermediate
  plan-approval pause.
- Do not infer end-to-end authorization from a plan-only request.
- During the planning phase, modify only the intended planning document. Do not
  edit application code, tests, migrations, dependencies, implementation docs,
  or `docs/planning/history_step.md`; do not stage or commit.
- Do not invoke `planner-doc-review` before implementation evidence exists.
- Stop for an owner decision only when a material product, privacy, rights,
  policy, production, external-authority, or scope choice is unresolved. This is
  a decision gate, not routine approval of the development plan.

## Workflow

### 1. Establish planning authority

1. Read every applicable `AGENTS.md` from the repository root to the target
   subtree.
2. Read completely:
   - `docs/planning/stages.md`;
   - `docs/planning/next_step.md`;
   - `docs/planning/history_step.md`.
3. Read another next-step file only when it exists and the user places that
   planning lane in scope.
4. Capture `git status --short` as a read-only baseline. Preserve every unrelated
   or owner-modified path.
5. Treat `next_step.md` as implementation authority when it is already approved
   or when the user's direct end-to-end instruction authorizes the resulting
   plan. Treat `stages.md` as roadmap context and `history_step.md` as append-only
   evidence.

### 2. Resolve the current planning state

Inspect the top status, appended developer reports, and appended planner reviews
before writing.

- If `next_step.md` is cleared after a planner-approved archive, proceed.
- If it contains a `Proposed` plan, preserve owner decisions and edit only what
  the current request requires. In end-to-end mode, authorize the resulting plan
  after the planning self-review unless a material owner decision remains open.
- If it contains an owner-approved active plan, do not replace or weaken it. Use
  it as the authority for an in-scope end-to-end request.
- If it contains unreviewed implementation evidence, do not create a replacement
  plan. In end-to-end mode, verify the evidence and continue to the independent
  planner-review phase; otherwise report the active gate.
- If its status is `CHANGES_REQUIRED`, do not propose a replacement. In
  end-to-end mode, resume the bounded remediation loop from the latest planner
  findings; otherwise report the active gate.
- If it is blocked on missing evidence, external authority, or an owner decision,
  report that exact blocker and stop.
- If the state is ambiguous, inspect history and Git evidence. Ask the owner only
  when the unresolved choice would materially change scope or policy.

Never duplicate an archive entry or infer that an active plan may be discarded.

### 3. Inspect the implementation surface

Read the smallest relevant set of current source, tests, migrations, architecture
decisions, configuration, and dependency files needed to plan accurately.

Identify:

- existing helpers and public contracts to preserve;
- authoritative data, time, identity, authorization, and failure sources;
- transaction and concurrency boundaries;
- process-global environment variables and external-service dependencies;
- privacy, tenant-isolation, and sensitive-data boundaries;
- representative legacy suites that could expose cross-suite contamination;
- pre-existing workspace noise that the future implementation must preserve.

Do not design from roadmap prose alone. Distinguish source-backed facts, project
decisions, assumptions, and open questions.

### 4. Choose one bounded step

Prefer the smallest vertical slice that produces independently reviewable evidence.

Treat a candidate as likely oversized when it combines multiple high-risk domains,
such as:

- a new migration plus concurrency or rollback behavior;
- a new external service plus environment provisioning;
- privacy or authorization policy plus delivery behavior;
- several independently testable adapters or lifecycle phases;
- a changed-file surface that cannot be reviewed as one coherent contract.

When oversized, select the first dependency-ordered slice and place later slices in
non-goals. Do not create parallel implementation authority or expand scope merely
to complete a roadmap stage.

### 5. Write the plan

Write exactly one plan to `docs/planning/next_step.md` using the repository's
required structure:

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

Set the status according to the request mode:

- plan-only: `Proposed`;
- end-to-end: `Authorized for implementation by direct owner workflow instruction`.

Do not use the end-to-end status while a material owner decision remains open.

Add the following planning controls without duplicating requirements.

#### Normative invariants

List the small set of non-negotiable truths most likely to be lost during
implementation. For each invariant, name its authority. Cover applicable items
such as:

- which component owns time and expiry;
- what constitutes success or failure for returned values and side effects;
- which identity, tenant, authorization, or policy fields must remain bound;
- which transaction owns durable state;
- which data or locator values must never cross a projection, log, or error
  boundary;
- which public behavior must remain unchanged.

Resolve contradictions between prose and authority before implementation. Keep a
material unresolved contradiction in `Open questions` and stop for an owner
decision.

#### Risk and dependency register

For each material risk, record:

- risk or failure mode;
- affected boundary;
- prevention or early detection gate;
- evidence required before broad testing;
- whether an owner decision or external resource is required.

Include external-service readiness, process-global environment restoration, test
ordering, database freshness, and cleanup when applicable. Record variable names
and configuration requirements, never credential values.

#### Acceptance-to-evidence matrix

Map every requirement and acceptance criterion to direct retained evidence. Use a
compact table with these columns:

| ID | Planned behavior | Direct evidence | Negative or edge evidence | Verification phase |
| --- | --- | --- | --- | --- |

Do not rely on the broad suite as the only evidence for a risky behavior. Mark any
item that requires manual, live, or currently unavailable proof.

#### Implementation checkpoints

Define at least these checkpoints when applicable:

1. **Contract checkpoint:** after interfaces and schema shape are drafted, perform
   a bounded read-only review of authority, time, failure-return semantics,
   transaction boundaries, privacy, and environment isolation.
2. **Pre-broad checkpoint:** confirm the acceptance-to-evidence matrix is complete,
   focused suites are green, fixtures restore process-global state, and generated
   infrastructure settings satisfy existing contracts.

These are non-binding implementation reviews. They do not archive, approve, or
replace the final `planner-doc-review` gate.

#### Conditional plan-review subagent

Classify whether the completed plan needs an independent read-only review before
implementation. Require the review when any of these apply:

- migration, schema, durable-state, rollback, transaction, or concurrency work;
- authorization, privacy, tenant isolation, rights, policy, or sensitive data;
- external services, process-global configuration, generated infrastructure, or
  difficult cross-suite isolation;
- changes spanning multiple modules or public contracts;
- non-obvious assumptions, failure semantics, or acceptance-evidence mapping.

Skip the review for a localized low-risk step with clear authority, one coherent
boundary, and direct focused proof. Record the skip reason; do not spawn a
reviewer merely to restate the plan.

When review is required:

1. Spawn one fresh read-only plan-review subagent after the main-agent planning
   self-review and before any implementation writer.
2. Give it the complete plan, applicable instructions, relevant inspected source
   and test context, and dirty-worktree baseline.
3. Require it to check scope, authority, invariants, contradictions, acceptance
   coverage, negative evidence, ordering, environment isolation, and test gates.
4. Require exactly one result: `PLAN_READY` or `PLAN_CHANGES_REQUIRED`, followed
   by blocking findings and optional non-blocking notes with precise plan or source
   locations.
5. Keep it advisory and read-only. It must not edit files, implement code, invoke
   `planner-doc-review`, append a formal planner result, approve completion, or
   act as the final implementation reviewer.
6. Have the main agent verify every finding against source, incorporate valid
   plan-aligned corrections, and rerun the planning self-review. Continue without
   a user approval pause unless a finding exposes a material owner decision.

#### Delegation and final-review handoff

Add a subsection under `Implementation notes` that defines this mandatory
authorized execution contract:

1. **Authorization gate:** in end-to-end mode, the direct workflow request
   authorizes the self-reviewed, in-scope plan without a separate approval pause.
   Stop only for a material unresolved owner decision or a change that expands
   beyond the user's request.
2. **Conditional plan reviewer:** before implementation, apply the plan-review
   trigger above. When required, use one fresh read-only subagent and resolve its
   source-backed findings without turning the review into a user approval gate.
3. **Single implementation writer:** after authorization and any required plan
   review, the main agent delegates the step to exactly one bounded
   implementation subagent. Give that worker
   the authorized plan, applicable instructions, writable file scope, non-goals,
   dirty-worktree baseline, required validation commands, and developer-report
   format. The worker may implement the authorized step, run its checks, and append
   a developer implementation report to the planning document. It must not
   archive or reset planning docs, stage or commit files, invoke
   `planner-doc-review`, or claim final completion.
4. **Non-overlapping agents:** any additional subagent is read-only and has a
   distinct evidence-gathering or specialist-review scope. No second agent may
   edit the implementation writer's files. If subagent delegation is unavailable,
   report the blocker instead of silently changing the role contract.
5. **Main-agent verification:** after the worker returns, the main agent remains
   accountable for requirements and decisions. It must inspect the actual diff,
   changed-file set, developer report, and test outputs; map the evidence back to
   the acceptance-to-evidence matrix; and rerun the highest-signal focused checks
   when feasible. A worker summary alone is not completion evidence.
6. **Independent planner review:** once implementation evidence is ready, the main
   agent delegates a fresh independent planner subagent that did not implement the
   change or perform the pre-implementation plan review. That reviewer must use
   `planner-doc-review` against the authorized plan and actual workspace evidence.
   The implementation worker and plan reviewer may not perform final review.
7. **Bounded remediation loop:** for `CHANGES_REQUIRED`, return the exact blocking
   findings to the same implementation worker, permit only plan-aligned fixes,
   rerun affected proof, append a new developer report, and request a fresh
   independent planner review. For `BLOCKED_NEEDS_MORE_INFO`, gather the missing
   evidence or request the required owner decision. Never weaken the authorized plan
   to obtain approval.
8. **Closeout authority:** only an `APPROVED` or `APPROVED_WITH_NOTES` result may
   trigger `planner-doc-review`. Closeout must add exactly one linked row to the
   `history_step.md` Step History Menu, add the matching unique anchor immediately
   before the append-only archive entry, reset the reviewed plan, and create the
   focused commit. Verify that the new link resolves to exactly one archive entry
   and that neither the menu row, anchor, nor archive is duplicated. Do not mark
   the goal complete before that commit succeeds. Preserve unrelated dirty files
   with explicit staging pathspecs.

#### Validation ladder

Derive exact commands from the repository. Require this order when the relevant
test layers exist:

1. Run the narrow focused tests for the changed boundary.
2. Run a cross-suite isolation regression in one test process: the new suite first,
   followed by representative legacy suites. Verify restoration of mutated
   environment and other process-global state.
3. Run the repository-wide suite fail-fast with `--maxfail=1` or the repository's
   equivalent. Diagnose the first failure in full test order before changing
   production behavior.
4. Run the complete fresh repository-wide suite only after the fail-fast run is
   clean.
5. Run applicable static, formatting, privacy, diff, dependency, resource-cleanup,
   and scope checks.

Require fresh disposable infrastructure where the plan depends on database,
broker, object-storage, or similar services. Define readiness checks and valid
generated settings before the broad run. If a check cannot run, require the
implementation report to state the exact reason and missing evidence.

### 6. Perform a planning self-review

Before finishing, verify that:

- every requirement is specific and testable;
- every acceptance criterion has mapped evidence;
- non-goals exclude adjacent roadmap work;
- likely affected files match the inspected repository;
- the implementation ordering reaches risk early;
- focused and cross-suite checks precede broad regression;
- the plan status matches plan-only or end-to-end mode;
- the conditional plan-review trigger was classified with a recorded reason;
- the downstream handoff names one implementation writer, direct main-agent
  evidence inspection, a distinct final planner reviewer, and the bounded
  remediation and closeout rules, including the linked history menu entry;
- owner decisions are explicit and unresolved decisions remain open;
- the plan does not authorize policy, privacy, rights, or production behavior the
  owner has not approved;
- no file other than the intended planning document was changed.

Use `git diff --check -- docs/planning/next_step.md` and inspect the exact planning
diff when available.

### 7. Run conditional plan review

Apply the trigger criteria in `Conditional plan-review subagent` in both request
modes.

- If skipped, record the concrete low-risk reason and continue.
- If required, dispatch one fresh read-only reviewer and wait for its result.
- For `PLAN_CHANGES_REQUIRED`, verify each finding, revise only the plan, and rerun
  the planning self-review before continuing.
- Do not dispatch the implementation writer while a confirmed blocking plan
  finding or material owner decision remains unresolved.
- Do not reuse this reviewer for final post-implementation review.

### 8. Continue or stop by mode

Report:

- the proposed step title and scope;
- whether the step was narrowed or split;
- the highest-risk invariants and early gates;
- any open question requiring an owner decision;
- confirmation that the implementation-worker and independent-review handoff is
  encoded in the plan;
- whether conditional plan review ran or was skipped, its result, and the reason;
- the exact planning file changed;
- the selected request mode.

- In plan-only mode, stop after reporting the proposed plan. Do not ask for routine
  approval unless the user asked to approve it.
- In end-to-end mode, do not pause for plan approval. Dispatch the implementation
  worker immediately after any required plan review is resolved.
- If a material owner decision remains unresolved, report only that decision gate
  and do not dispatch implementation.

### 9. Execute the authorized handoff

In end-to-end mode:

1. Dispatch exactly one bounded implementation writer using the scope and stop
   conditions recorded in the plan.
2. Wait for the worker, then directly inspect the actual diff, changed-file set,
   developer report, and test evidence.
3. Dispatch a fresh independent planner subagent that neither implemented the
   change nor reviewed the plan, and require it to use `planner-doc-review`.
4. For `CHANGES_REQUIRED`, return only the confirmed blocking findings to the same
   worker, rerun affected evidence, and request a fresh independent review.
5. Complete only after planner approval, linked history-menu/archive update,
   reset, and the focused commit succeed. Report blockers without weakening the
   plan or staging unrelated work.

## Success criteria

In plan-only mode, this skill succeeds when one source-grounded `Proposed` plan is
ready, any required read-only plan review was resolved, and no implementation
action occurred. In end-to-end mode, it succeeds only when any required plan
review was resolved and the authorized plan passed the worker, direct
verification, independent final planner review, linked history-menu/archive
update, reset, and focused-commit gates.

