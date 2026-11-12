# Planning Contract

Use this reference when producing a substantial next-step plan or maintaining the standard planning files.

## Reconstruct the Actual State

Inspect decision-relevant evidence and follow dependencies far enough to model the actual architecture. Typical evidence includes:

- applicable repository instructions;
- the current plan and relevant roadmap or historical records;
- responsible source files and public interfaces;
- callers and downstream consumers;
- tests and fixtures;
- runtime artifacts, logs, or diagnostics;
- recent implementation reports and the actual version-control diff or state.

Record material facts using the evidence labels defined in `SKILL.md`. If a report conflicts with code, tests, or runtime output, preserve the conflict until it is resolved.

## Frame the Decision

Restate the request in operational terms:

- What outcome is required?
- Who or what consumes the result?
- What behavior must change?
- What behavior must remain unchanged?
- Which constraints are binding?
- What observable evidence would count as success?
- What is deliberately outside the current scope?

Challenge the requested mechanism when the desired outcome may have a simpler cause or solution. For example, an “agent improvement” may be best implemented as a deterministic rule, narrower interface, better state representation, observability, or failure handling.

## Find the Bottleneck and Critical Unknown

Focus on the current constraint that most limits the desired outcome.

Ask:

> Which assumption, if false, would invalidate this plan?

Resolve that assumption with direct evidence when reasonably possible. Prefer inspected source, tests, official documentation, actual workflows, and runtime behavior. If a small isolated experiment is cheaper than extended discussion, specify or run that experiment within the task's authorization boundary.

## Map the Change Surface

Identify:

- the responsible component and existing boundary to extend;
- inputs, outputs, and public contracts;
- callers and downstream consumers;
- persistence, caching, or state implications;
- expected error and recovery paths;
- tests that establish current and desired behavior;
- documentation that would become stale;
- migration and compatibility concerns.

Every added component, abstraction, dependency, model call, or persistent state object must solve a concrete current problem.

## Compare Credible Alternatives

Include the realistic baseline, which may keep the current approach unchanged. For each serious option, compare:

- correctness and failure behavior;
- implementation and operational complexity;
- reversibility;
- fit with existing conventions and interfaces;
- latency and resource cost;
- observability;
- testing difficulty;
- long-term maintenance burden.

Compare the credible options that actually affect the decision. Select the option with the strongest total-system tradeoff, giving materially simpler approaches full consideration.

## Select One Coherent Step

The step must:

- produce an observable improvement;
- be independently testable;
- fit the existing architecture;
- limit blast radius;
- leave the project in a coherent state;
- create evidence for the following decision.

“Small” means a narrow, complete slice. A coherent slice contains working interfaces and live task-owned paths; cleanup and future infrastructure remain separately scoped.

## Define Acceptance Before Implementation

Every required behavior needs an observable criterion that identifies:

- the input or starting condition;
- expected output or behavior;
- relevant edge and error cases;
- behavior or interfaces that must remain unchanged;
- the test, command, artifact, or inspection that proves compliance.

Map each criterion to planned validation where practical. Attach observable definitions to broad phrases such as “works correctly,” “is robust,” or “improves the architecture.”

## Standard Durable Project State

Use this protocol only when the project follows the i11usion planning-file convention.

- `AGENTS.md` contains durable repository instructions and conventions. Place temporary task scope in the current implementation plan.
- `stages.md` contains strategic direction. Take current implementation authority from the approved plan.
- `next_step.md` is the current implementation contract for one narrow, coherent, testable step.
- `history_step.md` is the append-only archive of superseded plans and their outcomes.

Follow project-local variants when they are explicit, such as multiple independently active next-step files.

### Replacing `next_step.md`

Before replacement:

1. Read the existing file completely.
2. Determine whether the step is active, completed, blocked, or obsolete.
3. Check `history_step.md` for an existing archive of the same plan.
4. Append the prior plan while preserving its title, date, status, developer reports, planner reviews, and decision rationale.
5. If required planner review is missing, preserve that unresolved status and explain why replacement is still justified.
6. Only then write the newly approved current plan.

Preserve the historical record as it was approved and executed.

## Recommended `next_step.md` Shape

```markdown
# Next Step: <Narrow, outcome-oriented title>

## Status

Planned

## Why This Step Now

State the bottleneck, evidence, and priority rationale.

## Verified Current State

Include only behavior supported by inspected evidence. Label remaining inferences, unknowns, and conflicts.

## Objective

State the observable outcome.

## Scope

### Must Implement

- Required behavior, integration, tests, and documentation.

### Must Preserve

- Existing behavior and interfaces that must remain stable.

### Out of Scope

- Related work deliberately excluded from this step.

## Relevant Architecture

Identify responsible components, interfaces, data flow, likely files, state, and failure paths while leaving incidental implementation details to local code context.

## Implementation Strategy

Describe the selected approach, why it won, and its important constraints.

## Acceptance Criteria

1. Given <condition>, the system produces <observable result>.
2. Given <edge or error condition>, the system produces <defined behavior>.
3. Existing <behavior or interface> remains unchanged.
4. The mapped checks pass.

## Validation Plan

List narrow checks first, followed by relevant integration or broader checks.

## Risks and Open Questions

Include only unresolved issues that could affect implementation or validation.

## Handoff Instructions

State what the implementation agent must report and what requires planner review.
```

The contract must constrain consequential decisions while leaving incidental details to local code context.

## Bounded Subagents

Use subagents only when independent investigations are likely to improve the decision. Give each one:

- one bounded question;
- relevant files or scope;
- expected evidence;
- explicit exclusions;
- a concise output format.

Prefer read-only investigation. The primary planner validates critical subagent findings, reconciles disagreements, and writes one coherent plan.

## Planning Completion Check

Planning is complete when:

- current state and source conflicts have been inspected;
- verified facts are separated from assumptions and future intent;
- the outcome, bottleneck, and decision-critical unknown are clear;
- credible alternatives and the baseline have been compared;
- one coherent implementation slice is selected;
- scope, preserved behavior, and non-scope are explicit;
- observable acceptance criteria and validation exist;
- material risks remain visible;
- the authorized durable plan is written;
- any replaced plan is archived correctly.

Then summarize the decision, rationale, implementation boundary, and primary unresolved risk concisely.
