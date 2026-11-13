---
name: plan-review-implement-review
description: Coordinate planning, risk-based plan review, implementation, verification, independent final review, and closeout only for an explicit full-lifecycle request or project mandate. Replaces prepare-development-step lifecycle and planner-doc-review closeout roles.
---

# Plan Review Implement Review

Be the sole end-to-end coordinator. Reuse Think for planning and evidence review, Work for implementation, and the [shared protocol](../think-like-i11usion/references/workflow-protocol.md) for authority, records, states, and verdicts. Load their guidance only for the phase being performed.

1. Establish the requested endpoint and actual current state. A plan-only or review-only request stops at that endpoint, even in a project with a full workflow. Do not interpret an old report as authority to start the next phase.
2. Plan one bounded step using [Think](../think-like-i11usion/SKILL.md). Apply [lifecycle.md](references/lifecycle.md) for the risk decision and role separation. Record why a low-risk plan needs no independent plan review.
3. Execute the authorized contract using [Work](../work-like-i11usion/SKILL.md) in strict mode. Keep one active implementation owner at a time.
4. Verify actual diff and evidence. Obtain independent final review using Think; required final review cannot be silently skipped or reported as passed.
5. Correct confirmed blocking findings within scope, verify again, and obtain re-review of the changed evidence.
6. For accepted work, apply [closeout.md](references/closeout.md) only to authorized closeout actions. Preserve history and unrelated work.

Commit, push, merge, and deploy are separate actions, each needing explicit user authorization or an applicable project policy that authorizes that specific action. A lifecycle request alone authorizes neither publication nor a commit. When authorized policy requires a commit, keep closeout pending until it succeeds.

Persist a compact role/evidence ledger when the workflow has a durable record. Cross-session writer replacement is allowed after a verified handoff and exclusive ownership transfer; see lifecycle.md. If independence is unavailable, record REVIEW_UNAVAILABLE and the remaining gate. Follow the actual authorization boundary; never substitute self-review for independent approval.

Stop at the requested endpoint, a material owner decision, or a required unavailable gate. Never start another roadmap step automatically.
