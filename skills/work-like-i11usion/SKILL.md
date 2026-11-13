---
name: work-like-i11usion
description: Implement, debug, or refactor for a concrete development request using the merged karpathy-guidelines principles. Use ordinary execution by default; use strict execution for a relevant approved contract, an explicit strict request, or a project requirement.
---

# Work Like i11usion

Execute authorized implementation. Planning-only and review-only requests belong to Think. A complex unresolved design decision needs planning, not speculative implementation.

## Select the mode

- **Ordinary (default):** direct, sufficiently clear work. Understand -> implement -> validate -> inspect diff -> report. Relevant verification is enough to report completion.
- **Strict:** the current request executes a relevant approved contract, explicitly requests strict execution, or project rules require it. Read the shared [workflow protocol](../think-like-i11usion/references/workflow-protocol.md). Execute the contract -> validate -> developer report -> required planner review. Leave acceptance pending until that review occurs.
- A plan file's mere presence does not make unrelated work strict. For legacy skill names in project instructions, use the protocol's compatibility mapping. A required full lifecycle belongs to the coordinator; Work remains its executor.

## Implementation discipline

1. **Think before coding.** Read applicable instructions, relevant source and tests, and Git state. Establish the observable outcome, preserved behavior, and material assumptions. Resolve ambiguity that would change scope or correctness; decide routine details using existing conventions.
2. **Simplicity first.** Prefer existing implementations and dependencies. Add only behavior needed for the request; introduce an abstraction, option, or dependency only for a concrete requirement.
3. **Surgical changes.** Keep every changed line connected to the outcome. Preserve public interfaces and behavior unless the authorized change requires otherwise. Protect unrelated uncommitted work, including overlapping hunks. Clean up only fallout from this change.
4. **Goal-driven verification.** Reproduce a bug when practical; define the smallest meaningful check for the requested behavior. Cover relevant error and boundary cases. Run focused checks, then affected integration or broader checks when risk requires them. Reuse valid unchanged evidence; do not automatically repeat a successful full suite.
5. Inspect the complete task-owned diff, scope, regressions, and temporary artifacts. Report what changed, why, what ran, results, and remaining limits. Clearly separate measured evidence from assumptions and unavailable checks.

Stop for an unapproved material change to scope, public contracts, persistence, security, or external effects. Otherwise continue within the request without routine approval pauses.

Ordinary work needs no planning-file updates or extra reviewer. Strict work follows the protocol's compact developer report and hands off for review; never self-certify independent approval. Commit, push, merge, and deploy require authorization for the specific action; implementation permission alone does not grant it.
