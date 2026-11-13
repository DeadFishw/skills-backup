# Authorized closeout

Use after an implementation-stage approval under the [shared protocol](../../think-like-i11usion/references/workflow-protocol.md). Approval establishes acceptance; it does not grant additional mutation permissions.

1. Determine which actions the current request or applicable project policy authorizes and requires: record review, archive/reset, commit, push, merge, deploy. Check each separately. For a plan-only or review-only endpoint, return the result and stop.
2. Bind acceptance to the reviewed implementation reference. Inspect current changes against that reference. A substantive implementation change requires re-review.
3. If archival is authorized, search for this task ID and implementation reference in history before appending. Preserve the full contract and reports exactly once. Use the existing history format; when it has navigation, create one unique anchor and matching menu entry and verify resolution. Do not rewrite earlier history.
4. Reset only the reviewed lane, after verifying its archive. Use the project's cleared format. Never create the next plan automatically. Update a roadmap only when separately within scope and supported by accepted evidence.
5. If a commit is authorized, inspect the final diff. Stage exact task paths that were clean at baseline; use selective hunks for paths containing owner changes. An inseparable overlap blocks staging. Inspect the staged diff before committing and verify its paths and content afterward.
6. Publish or deploy only when that specific action is authorized, using the reviewed artifact and reporting the observed result.

When no archive/reset or commit is required and authorized, closeout can finish with an accepted handoff and verified workspace state. Do not create a permanent completion blocker merely because commit permission was not granted. If the project's explicit completion contract requires a still-pending action, keep that action visible and report ACCEPTED rather than CLOSED.

After partial failure, preserve the verified steps, record the first incomplete action, and resume there. Do not duplicate archives, resets, or commits. An external failure or unavailable check remains visible even if implementation was accepted.
