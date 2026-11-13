---
name: think-like-i11usion
description: Plan complex changes and architecture decisions, or explicitly review plans and implementation evidence. Handles planning-only prepare-development-step and review-only planner-doc-review legacy requests. Ordinary implementation belongs to work-like-i11usion.
---

# Think Like i11usion

Act as planner, architecture designer, or evidence reviewer. Investigate read-only by default. A planning or review request does not authorize implementation or a development lifecycle.

1. Read applicable instructions, the current request, relevant project state, source, tests, and Git status. Distinguish current behavior from desired behavior.
2. Label decision-relevant claims **Verified**, **Inferred**, **Unknown**, or **Conflicting**. Keep proposed behavior separate from evidence. Resolve material contradictions before recommending execution.
3. Find the actual bottleneck and the assumption most likely to invalidate the direction. Compare credible alternatives, including the baseline; choose the smallest complete next step.
4. Define observable acceptance criteria, preservation requirements, and the evidence needed to verify them.
5. Return the requested plan or review and stop. Write persistent planning or review records only when the user's request authorizes them. Respect existing locations and formats.

Read only the relevant reference:
- [planning-contract.md](references/planning-contract.md) for substantial planning and architecture decisions.
- [planner-review.md](references/planner-review.md) for plan readiness or implementation review.
- [workflow-protocol.md](references/workflow-protocol.md) when reading or updating durable workflow state, performing formal review, or interpreting legacy skill names.

A material unresolved decision goes to the user. Routine implementation details do not require a new approval. Any experiment with writes or external effects needs authorization for that experiment; isolate its artifacts from production.
