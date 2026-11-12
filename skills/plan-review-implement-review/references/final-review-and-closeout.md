# Final Review and Closeout

Use this reference after coordinator verification has assembled the implementation evidence.

## Independent Final Reviewer

Use one fresh read-only reviewer that neither implemented the change nor performed the conditional plan review. Give it the complete review package and require criterion-by-criterion assessment against the authorized plan.

Verify the role ledger before dispatch and record the final reviewer agent id, nickname, or session reference. The final reviewer identity must differ from the implementation writer and any conditional plan reviewer.

The reviewer inspects actual evidence where access permits and evaluates:

- alignment with goals, requirements, invariants, and non-goals;
- completeness against every acceptance criterion;
- architecture, security, privacy, reliability, compatibility, and maintainability;
- focused, edge, error, regression, isolation, and live-proof coverage;
- implementation deviations and missing evidence;
- dirty-worktree and changed-file scope;
- truthfulness of developer and coordinator reports.

## Verdicts

- **APPROVED:** the implementation satisfies the plan with sufficient evidence.
- **APPROVED_WITH_NOTES:** the implementation satisfies the plan; recorded caveats or follow-ups remain outside the completion gate.
- **CHANGES_REQUIRED:** one or more correctable blocking findings prevent acceptance.
- **BLOCKED_NEEDS_MORE_INFO:** evidence, authority, environment, or planning consistency is insufficient for a verdict.
- **PLANNER_REVIEW_UNAVAILABLE:** the required independent reviewer cannot be provided in the current environment.

## Review Request

Use this structure:

```text
Independent planner review requested.

Planning document and baseline:
<path, status, goals, requirements, invariants, non-goals, acceptance criteria>

Developer reports:
<latest report and relevant remediation reports>

Verified implementation evidence:
<diff, changed files, source inspection, commands, results, artifacts>

Acceptance-to-evidence assessment:
<criterion-by-criterion mapping and gaps>

Dirty workspace and scope:
<baseline paths, task-owned paths, index state, unrelated preserved work>

Role ledger:
<coordinator, plan reviewer or skip, implementation writer, proposed final reviewer>

Deviations, risks, and missing evidence:
<details>

Return exactly one verdict:
APPROVED | APPROVED_WITH_NOTES | CHANGES_REQUIRED | BLOCKED_NEEDS_MORE_INFO | PLANNER_REVIEW_UNAVAILABLE

For each finding include severity, location, finding, required action, rationale, and supporting evidence.
```

## Review Record

The coordinator appends the returned review after the latest developer report using the repository format or this default:

```markdown
---

## Planner Implementation Review - <timestamp and timezone>

**Planning document reviewed:** `<path>`
**Developer report reviewed:** `<heading or implementation reference>`
**Implementation reference:** `<workspace, branch, patch, or commit>`
**Planner result:** `<verdict>`
**Reviewed by:** <final reviewer agent id, nickname, or session reference>
**Role separation:** <writer identity; plan reviewer identity or skip; final reviewer identity>

### Summary

<summary>

### Alignment with plan

<assessment>

### Verified evidence

- <evidence>

### Acceptance-criteria assessment

| Criterion | Result | Evidence | Finding |
| --- | --- | --- | --- |

### Findings

#### Blocking

- <finding or None>

#### Non-blocking

- <finding or None>

#### Informational

- <finding or None>

### Test and validation assessment

<assessment>

### Dirty workspace and scope assessment

<assessment>

### Required developer actions

- <action or None>

### Final decision

<decision>
```

Append one review per active planning lane. Preserve the planning baseline, developer reports, and prior reviews.

## Status Mapping

Update the active plan's top status after appending the review:

- `APPROVED`: `Implemented and planner-reviewed - APPROVED (<timestamp>)`
- `APPROVED_WITH_NOTES`: `Implemented and planner-reviewed - APPROVED_WITH_NOTES (<timestamp>)`
- `CHANGES_REQUIRED`: `Changes required after planner review (<timestamp>)`
- `BLOCKED_NEEDS_MORE_INFO`: `Blocked pending planner-review evidence (<timestamp>)`
- `PLANNER_REVIEW_UNAVAILABLE`: `Planner review unavailable; pending independent approval (<timestamp>)`

Change only the top status body. Keep the appended audit trail intact.

## Verdict Handling

### Changes Required

Append the review, update status, and return confirmed blocking findings to the same writer. Keep archive, reset, staging, and commit closed until a fresh review approves the remediation.

### Blocked or Review Unavailable

Append the blocked or unavailable result, update status, and state the evidence or role needed to resume. Keep completion pending.

### Approved or Approved With Notes

Append the review and update status, then perform the closeout gates below.

## Approval-Gated Closeout

1. **Capture the reviewed artifact.** Read the full active plan after the final review and status update. Determine the step title, final verdict, timestamp convention, and archive identity.

2. **Check idempotency.** Search history and Git for the step title, implementation reference, menu row, anchor, archive body, reset state, and focused closeout commit. Resume an existing partial closeout instead of duplicating it.

3. **Archive the full record.** Append the reviewed plan, including developer reports and planner reviews, to the history file using the project's archive format. Preserve existing archived bodies.

4. **Maintain navigation when the project uses it.** Add exactly one history-menu row and one matching unique anchor. Derive a stable identifier from the stage/step or title. Verify that the menu target, anchor, and new archive entry each occur exactly once and that earlier menu rows and archives remain unchanged.

5. **Reset the active plan.** Replace the reviewed lane with the project's minimal cleared placeholder. Under the default convention:

```markdown
# Next Step

## Status

Status: Cleared after planner-approved archive; ready for the next approved plan.
```

Use the lane's own title for additional plan files.

6. **Update approved durable state.** Apply roadmap, architecture, decision, or operational-document updates required by the plan and supported by reviewed evidence. Preserve future work and unavailable production claims.

7. **Inspect final scope.** Compare the final changed-file set and each task-touched file with the plan, developer report, review, archive, reset, and retained initial dirty baseline. Derive the task-owned patch separately from pre-task owner hunks. Run diff, formatting, link, anchor, archive-uniqueness, and scope checks relevant to the repository.

8. **Stage the task-owned delta.** Exact-path staging is appropriate for files that were clean at baseline or are wholly task-created. For a task-touched path with pre-task changes, use selective hunk staging or an equivalently validated task-owned patch. If owner and task hunks cannot be separated confidently, stop closeout and report the staging blocker. Inspect staged name-status and the complete staged diff against the baseline evidence before commit.

9. **Create one focused commit.** Use a concise message for the reviewed step. Verify the commit contains the reviewed task-owned delta, archive/reset state, and intended paths; verify unrelated owner hunks and dirty files remain unstaged.

10. **Report closeout.** State the verdict, reviewed implementation reference, archive and reset result, navigation verification, focused commit hash, remaining unrelated workspace state, planner notes, and separately authorized next actions.

The workflow reaches completion after the focused commit succeeds. Push, merge, release, deployment, environment cleanup outside task-owned disposable resources, and other external actions remain separate permissions.

## Partial Closeout Recovery

If a closeout action fails, preserve completed durable mutations and report the exact gate. On resume:

1. inspect plan, history, menu, anchors, index, working tree, and commits;
2. identify the first incomplete gate;
3. verify previous gates rather than repeating them;
4. continue with exact task-owned paths;
5. keep completion pending until a focused commit containing the reviewed task-owned paths is verified.
