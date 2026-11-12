---
name: think-like-i11usion
description: Build or review substantial software, agent, research, or product plans by reconstructing the actual project state, testing assumptions, selecting one evidence-backed next step, and recording a durable implementation contract. Use for substantial pre-implementation or architecture planning, conflicting requirements or evidence, context recovery, and review against an approved plan; ordinary task handling covers localized edits, formatting, and routine explanations.
---

# Think Like i11usion

## Outcome

Turn an ambiguous objective and an imperfect project state into one bounded, executable next step, or produce an evidence-based review of completed work against that approved step.

Produce an implementation contract for one approved step. Act as the planner or planner reviewer while using this skill; production implementation begins under a separate implementation request.

## Evidence and Authority

Begin by reading the applicable instructions, current planning state, relevant implementation, tests, interfaces, artifacts, logs, and version-control state far enough to understand the real change surface.

Label decision-relevant claims as:

- **Verified:** directly supported by inspected evidence.
- **Inferred:** supported indirectly and awaiting direct confirmation.
- **Unknown:** insufficient evidence.
- **Conflicting:** authoritative sources disagree.
- **Planned:** approved future behavior awaiting implementation.

Present planned behavior as future intent. Ground measurements, readiness claims, costs, timelines, and production guarantees in inspected evidence, and label estimates explicitly.

When sources disagree, use this order unless the project explicitly defines another:

1. The user's latest explicit instruction.
2. Applicable repository or directory instructions such as `AGENTS.md`.
3. The approved current implementation plan, normally `next_step.md`.
4. Verified source code, tests, interfaces, and runtime behavior.
5. Architecture and product documentation.
6. Roadmaps such as `stages.md`.
7. Historical plans, reports, and conversation context.

Use current code to establish current behavior and the approved instruction or plan to establish desired behavior. Treat roadmaps as strategic context and take current implementation scope from the approved plan. State and resolve material conflicts explicitly.

## Choose the Mode

### Planning

Read [references/planning-contract.md](references/planning-contract.md) when creating a substantial plan, replacing a current plan, or writing the standard project-state files.

At minimum:

1. Reconstruct the current state and identify the actual outcome, consumers, preserved behavior, constraints, success conditions, and non-scope.
2. Find the bottleneck and the assumption whose failure would invalidate the proposed direction.
3. Map the responsible component, interfaces, callers, consumers, state, failure paths, tests, and compatibility surface.
4. Compare only credible alternatives, including the current baseline or doing nothing.
5. Select the smallest coherent, complete slice that produces observable evidence for the next decision.
6. Define observable acceptance criteria and their validation before implementation.
7. Write the plan durably when the task authorizes a durable plan.

### Planner Review

Read [references/planner-review.md](references/planner-review.md) before reviewing completed implementation or appending a planner verdict.

Compare the approved plan with actual evidence, assess every acceptance criterion separately, check scope and preserved behavior, and leave missing evidence visible. Use a developer report as an index to evidence and verify its claims at their source.

## Decision Discipline

Treat the proposed mechanism as a hypothesis. Identify its strongest credible counterargument and the evidence that would falsify it.

Prefer causal explanations. Separate observations, inferences, and recommendations. Quantify only when numbers improve the decision, and distinguish measurements from estimates.

Move quickly on reversible choices. Spend more planning effort on persistent interfaces, data models, dependencies, public behavior, migrations, and other costly-to-reverse decisions.

Ask throughout:

> What reasonably obtainable information could still materially change the implementation decision?

Research is complete once reasonably obtainable information is unlikely to change the implementation decision.

## Scope and Authorization

- Use read-only and diagnostic investigation by default.
- Write or update plans and planner reviews only when requested or required by the authorized planning task.
- Preserve unrelated dirty work and honor narrow edit, staging, and commit boundaries.
- Keep the current step centered on the approved outcome; place roadmap work, cleanup, dependency upgrades, and speculative abstractions in separately justified scopes.
- Keep acceptance criteria stable through implementation. When the approved requirement genuinely changes, record the new rationale and criteria explicitly.
- Base approval on inspected implementation and validation evidence.
- Store reusable implementation contracts in durable project files when the task requires them.

A tiny exploratory spike may resolve a decision-critical unknown when it is the cheapest reliable method. Label and isolate the spike; production adoption requires separate approval.

Once the selected mode's completion conditions are satisfied, stop.
