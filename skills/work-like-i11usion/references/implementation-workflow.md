# Implementation Workflow

Use this reference while executing an approved implementation contract.

## Trace the Existing Path

Before editing, determine:

- where input enters;
- where the relevant decision is made;
- how data is transformed;
- which state is read or written;
- how errors are represented;
- which interfaces are externally consumed;
- where tests observe the behavior.

Extend the existing responsible boundary when it already provides the correct ownership point.

## Choose the Smallest Coherent Change

Prefer:

- modifying an existing component;
- extending an established interface;
- explicit control flow;
- small functions with clear inputs and outputs;
- local state with clear ownership;
- project conventions;
- standard-library and existing dependencies.

Judge size at the system boundary. The selected change should satisfy the complete contract, preserve architectural ownership, and leave consistent behavior across affected callers and consumers.

## Establish the Observable Check

Define how the required behavior will be observed before or alongside implementation. Use the narrowest relevant behavioral test where practical. Deterministic commands, fixtures, artifact comparisons, or inspection procedures can cover behavior that resists direct automated testing.

Tests should establish externally meaningful behavior. Test an internal mechanism when the mechanism itself is a durable contract.

## Implement Incrementally

For each logical increment:

1. make the focused change;
2. inspect the local diff;
3. run the narrowest relevant check;
4. confirm that the observed result follows the intended mechanism;
5. confirm that the change set contains task-owned files and dependencies.

Use early focused feedback to resolve basic defects before broader validation.

## Handle Edges and Errors

Consider the cases relevant to the contract, including malformed input, missing values, empty results, duplicate state, unavailable dependencies, timeouts, partial failures, retries, and incompatible stored data.

Use explicit errors with actionable context. Preserve established error types and user-facing conventions when the implementation contract keeps them stable. Recovery and fallback behavior should correspond to a defined product or operational policy.

Add defensive handling where it materially improves safety, correctness, or diagnostics while keeping the primary contract visible.

## Preserve Public Behavior

Keep unmodified public contracts stable, including:

- function signatures;
- schema fields;
- command behavior;
- serialized formats;
- externally visible defaults;
- relevant runtime messages;
- backward compatibility.

When the approved contract changes public behavior, update every affected caller, test, document, and migration within the approved scope.

## Validate Narrowly, Then Broadly

Run checks in increasing order of cost and scope:

1. syntax, type, or static checks relevant to edited files;
2. focused unit tests;
3. affected component or integration tests;
4. relevant broader suites;
5. artifact, CLI, or end-to-end checks required by the contract.

Continue to the broader checks warranted by shared behavior and integration risk. Record each exact command, result, and material output. When an environment is unavailable, use the strongest narrower evidence and keep the unavailable check visible in the report.

## Inspect the Final Diff

Review the complete task-owned diff as another developer would. Confirm:

- every changed file supports an acceptance criterion, preservation requirement, or validation obligation;
- temporary artifacts and debugging output are absent;
- all code paths are live and responsibilities remain singular;
- state ownership and side effects are visible;
- public API changes match the contract;
- comments and documentation match current behavior;
- tests assert meaningful outcomes;
- secrets and machine-specific paths are absent;
- formatting changes remain focused;
- abstractions correspond to current requirements.

Compare the diff with every scope-lock list. Preserve unrelated user changes and verify exact staged paths when version-control actions are part of the request.

## Documentation

Document public behavior, compatibility decisions, constraints, and durable reasoning that future maintainers need. Comments should explain intent or invariants that remain implicit in local code.

Follow repository language and terminology. When repository conventions are silent in an i11usion-owned project, use natural Simplified Chinese prose while retaining established technical terms such as API, RAG, GPU, COG, MCP, model names, and library names in English.

Planning and roadmap state should reflect verified behavior and the planner's recorded decision.

## Deviation Classification

### Incidental Detail

Choose the simplest convention-compatible option. Record it when it affects future maintenance.

### Local Necessary Adjustment

Make the smallest closely connected supporting change and explain its necessity.

### Material Plan Defect

Pause implementation and return the decision to `think-like-i11usion` when the task requires an unapproved public interface, dependency, persistence model, architectural responsibility, migration, security assumption, or substantial scope increase.

### Separate Defect

Record the defect as a follow-up candidate. If it blocks the approved task, establish the narrow connection and return any material scope decision to the planner.

### Conflicting Evidence

Preserve the conflict and request planner resolution when code, tests, documentation, or the plan imply materially different required behavior.

## Bounded Subagents

Use subagents when parallel investigation or validation materially reduces uncertainty or elapsed time. Suitable bounded tasks include tracing an independent path, inspecting tests, checking compatibility in another module, reviewing the diff for scope, running an independent validation, or researching one dependency contract.

Prefer read-mostly assignments. Each writing assignment owns an exclusive, clearly bounded file set. The primary implementation agent reviews every contributed change, validates the integrated result, and confirms delegated test evidence.

## Execution Completion Check

Before handoff, confirm:

- acceptance criteria are satisfied or explicitly blocked;
- preserved behavior remains intact;
- relevant edge and failure paths are deliberate;
- narrow and broader checks match the change risk;
- evidence status reflects actual execution;
- the complete diff is focused and readable;
- documentation is current;
- deviations and limitations are ready for the developer report.
