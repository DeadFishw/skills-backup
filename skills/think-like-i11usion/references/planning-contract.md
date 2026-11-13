# Planning contract

Use for complex planning. Keep the plan in the response unless persistent writing is authorized. For durable files, use [workflow-protocol.md](workflow-protocol.md).

## Investigate the decision

Inspect the smallest relevant evidence set: instructions, active scope, current source and interfaces, affected callers, tests, runtime evidence, and Git changes. Search roadmap or history only to resolve a decision; read an active plan fully before changing it. Treat existing reports as pointers to evidence.

Identify the outcome and consumer, the actual limiting factor, preserved behavior, and the assumption whose failure would invalidate the approach. Use reasonably obtainable evidence to test that assumption. Stop investigating once further information is unlikely to change the decision.

Compare only credible options, including the existing approach, on correctness, complexity, reversibility, operational cost, and compatibility. Prefer extending an existing responsibility. Do not create infrastructure or abstractions for hypothetical future work.

## Produce one complete slice

A useful contract records:
- Outcome, selected approach, and decision rationale.
- Verified current state; material inferences, unknowns, and conflicts.
- Writable scope, preserved interfaces and behavior, and exclusions.
- Affected components and dependencies grounded in inspection.
- Acceptance criteria with stable IDs and direct validation.
- Relevant risks, unresolved owner decisions, and completion boundary.

Use a compact criterion table:

| ID | Starting condition | Observable result | Preservation / failure case | Evidence |
| --- | --- | --- | --- | --- |

For risky work, name the authority for time, identity, policy, persistence, and side effects where relevant. Specify early proof for migrations, rollback, concurrency, sensitive-data boundaries, external-service readiness, and shared-state isolation. These are conditional design concerns, not a mandatory checklist for every plan.

Select a narrow vertical slice that leaves coherent, testable behavior. Split independent outcomes instead of combining several unresolved high-impact changes. State which uncertainty the slice resolves.

Before returning, check that every required outcome has a criterion, likely files exist, scope fits the request, and missing evidence is visible. Planning alone does not approve execution. An explicit end-to-end request can authorize its bounded in-scope plan, subject to unresolved owner decisions and the coordinator's review gates.
