---
name: planner-doc-review
description: Use whenever a developer appends or provides an implementation report, commit report, completion report, or claims completion of work that should be reviewed against next_step.md or next_step2.md. Review against the relevant planning doc, append the planner result, update top Status, archive approved planning docs to history_step.md, reset the reviewed next-step doc, and commit the reviewed step after approval before marking work complete.
---

# Planner Doc Review Skill

## Purpose

Review developer implementation against the project planning documents, append the planner's review result to the end of the reviewed planning document, update that document's top Status section with the planner outcome, archive approved planning docs to `history_step.md`, reset the reviewed next-step doc for future updates, and commit the reviewed step after approval.

The supported planning docs are:

- `next_step.md`
- `next_step_2.md`

This skill creates a completion gate: implementation is not complete until planner review has been performed against the relevant planning document and the planner result has been appended to that document.

## Core rule

Never mark implementation complete until all of the following are true:

1. The relevant planning document has been read.
2. The latest developer implementation report has been found, or missing report evidence has been explicitly recorded.
3. The implementation has been reviewed by the planner against the relevant planning document.
4. The planner review result has been appended to the end of the reviewed planning document.
5. The top `## Status` section of the reviewed planning document has been updated to reflect the planner result.
6. If the planner result is `APPROVED` or `APPROVED_WITH_NOTES`, the reviewed planning document has been archived into `history_step.md` and reset for the next update.
7. If the planner result is `APPROVED` or `APPROVED_WITH_NOTES`, the final changed-file set has been inspected and a focused commit has been created for the reviewed step.

If planner review cannot be completed, append a blocked or unavailable review result to the relevant planning document instead of claiming that the implementation is complete.

Developer reports are evidence. They are not approval.

## When to use this skill

Use this skill when any of the following are true:

- A developer says an implementation is done, implemented, complete, fixed, patched, committed, pushed, ready, ready to merge, or ready for review.
- A developer appends an implementation report, commit report, completion report, validation report, proof artifact, or test report to `next_step.md` or `next_step2.md`.
- Code, configuration, migrations, tests, prompts, infrastructure, or documentation were changed based on `next_step.md` or `next_step2.md`.
- The agent is about to say the implementation is complete.
- The agent is about to approve, merge, release, or hand off developer work.
- The user asks whether developer work satisfies `next_step.md` or `next_step2.md`.

Do not use this skill for initial planning before any implementation exists.

## Planning document selection

Determine which planning document to review against:

1. If the developer report is appended inside `next_step.md`, use `next_step.md`.
2. If the developer report is appended inside `next_step2.md`, use `next_step2.md`.
3. If the developer report explicitly references `next_step.md`, use `next_step.md`.
4. If the developer report explicitly references `next_step2.md`, use `next_step2.md`.
5. If the developer report, user, branch, task, PR, commit, or implementation summary explicitly references both documents, review against both and append a separate review section to each file.
6. If it is unclear which document applies, read both documents and choose the one whose goals, tasks, acceptance criteria, changed files, or proof artifacts best match the implementation.
7. If both documents appear relevant, review against both.
8. If the documents conflict, append a `BLOCKED_NEEDS_MORE_INFO` review result explaining the conflict and do not mark the implementation complete.

## Developer report handling

The developer may append a structured or free-form report to the planning document.

Treat the latest developer report as the primary implementation evidence. Search from the bottom of the planning document upward and identify the newest block that looks like a developer completion report.

Recognize developer reports with headings such as:

- `## Developer Implementation Report`
- `## Developer Report`
- `## Implementation Report`
- `## Completion Report`
- `## Developer Update`
- `## Implemented`

Also recognize free-form reports that contain completion language and implementation evidence, such as:

```text
Implemented, committed, and pushed.
Commit:
<commit hash>
Push:
<branch and remote>
What changed:
<implementation summary>
Checks run:
<test results>
```

If more than one developer report exists, use the latest developer report that has not already been followed by a planner review for the same implementation reference or commit.

If a planner review already exists for the same commit or implementation reference, do not append a duplicate review unless the user explicitly requests a new review.

## Preferred developer report format

Developer reports should preferably be appended to the relevant planning doc using this format:

```md
---

## Developer Implementation Report — <YYYY-MM-DD HH:mm timezone>

**Status:** `<IMPLEMENTED | PARTIAL | BLOCKED>`  
**Commit:** `<commit hash or not provided>`  
**Branch / push:** `<branch, remote, PR, or push details>`  
**Implementation reference:** `<commit, branch, PR, patch, or summary>`  

### What changed

- <change>

### Tests and validation

- <test command or suite>: <result>

### Proof artifacts

- <artifact path, log path, screenshot, or "None">

### Known deviations from plan

- <deviation, or "None">

### Known issues / risks

- <issue, or "None">

### Dirty workspace / scope notes

- <dirty files, scope-check failures, or "None">
```

Free-form developer reports are acceptable, but the planner review request must preserve the original report text and also include a parsed summary.

## Distinguishing plan from report

Planning documents may contain both original planning content and appended implementation reports.

When reviewing:

- Treat original requirements, tasks, acceptance criteria, architecture notes, and constraints as the planning baseline.
- Treat developer-added implementation status, proof artifacts, test reports, and completion notes as implementation evidence.
- Do not treat the developer's own `implemented`, `done`, or `complete` status as planner approval.
- Do not allow a developer report to silently rewrite or weaken the original plan.
- If the developer changed the planning document itself, distinguish plan updates from implementation-status updates.
- If it is unclear whether a document change is a legitimate plan change or a developer self-status update, ask the planner to classify it and use `BLOCKED_NEEDS_MORE_INFO` if the distinction affects approval.

## Required evidence

Before asking the planner for review, collect as much of the following as possible:

- Contents of the relevant planning document.
- The original planning baseline from the document.
- The latest developer report from the document.
- Original user request, if available.
- Developer implementation summary.
- Commit hash, branch, push details, PR, patch, or diff.
- Changed files.
- Tests run and results.
- Test coverage gap assessment.
- Proof artifacts, logs, screenshots, or live validation outputs.
- Known deviations from the plan.
- Assumptions made by the developer.
- Unresolved risks, TODOs, skipped tests, or follow-up work.
- Dirty workspace notes or scope-check failures.

If evidence is missing, continue with available information and explicitly list the missing evidence in the planner review request.

## Implementation evidence verification

When repository access is available, do not rely only on the developer's self-report.

Verify as much as possible from the actual workspace:

- Confirm the referenced commit exists.
- Inspect the commit, diff, changed files, or PR.
- Confirm tests mentioned in the report are plausible and relevant.
- Compare implemented requirements and acceptance criteria against the tests that were added or run.
- Identify missing regression tests, edge-case tests, negative/error-path tests, live smoke/proof gaps, and tests that are too broad to prove the behavior.
- Check whether proof artifacts referenced by the report exist.
- Check whether dirty workspace files are inside or outside the implementation scope.
- Check whether the implementation changed the planning document itself.

Useful commands when available:

```bash
git status --short
git show --stat <commit>
git show --name-only --format=fuller <commit>
git diff <commit>^ <commit>
git diff --check
```

If verification is unavailable, tell the planner exactly what could not be verified.

## Dirty workspace and scope-check handling

If the developer report says a scope check failed because of pre-existing or out-of-scope dirty files, include that fact in the planner review request.

The planner may treat dirty files as non-blocking only if the available evidence shows all of the following:

1. The dirty files are unrelated to the planning document being reviewed.
2. The implementation commit or diff does not depend on those dirty files.
3. The dirty files are plausibly pre-existing or explicitly outside the developer's implementation scope.
4. The planning document does not require a fully clean workspace as an acceptance criterion.

If those conditions cannot be verified, the planner should use `BLOCKED_NEEDS_MORE_INFO` or `CHANGES_REQUIRED`.

## Review handoff procedure

When implementation appears complete:

1. Pause completion.
   - Do not say the task is done yet.
   - Do not approve, merge, release, or hand off yet.
   - Do not summarize the implementation as accepted.

2. Read the relevant planning document.
   - Read `next_step.md`, `next_step2.md`, or both according to the planning document selection rules.
   - Identify goals, requirements, acceptance criteria, implementation notes, and constraints.
   - Identify the latest developer report, if one exists.

3. Parse the developer report.
   - Extract status.
   - Extract commit, branch, push, PR, or implementation reference.
   - Extract what changed.
   - Extract tests and validation.
   - Extract proof artifacts.
   - Extract known deviations, risks, skipped checks, dirty files, and scope notes.

4. Gather or verify implementation evidence.
   - Identify actual changed files when possible.
   - Compare the implementation against the planning document.
   - Identify tests, validation, and remaining risks.
   - Perform a test coverage gap check:
     - Map each planned requirement and acceptance criterion to at least one test, proof artifact, or explicit manual validation.
     - Identify planned behavior that has no direct test coverage.
     - Identify missing edge-case, regression, negative/error-path, timeout/unavailable-upstream, payload-safety, scope-safety, and runtime/live proof coverage when relevant.
     - Identify tests that pass but are too broad, too shallow, offline-only, fixture-only, or not aligned with the risky behavior.
     - Decide whether each gap is blocking, non-blocking, or informational.
   - Identify evidence that is missing or unverifiable.

5. Ask the planner for review using the Planner Review Request format below.

6. Wait for planner feedback when planner delegation is available.
   - If the planner returns findings, classify them as blocking, non-blocking, or informational.
   - If the planner requests changes, send those findings back to the developer.
   - If the planner approves, record the approval and proceed.

7. Append the planner review result to the end of the reviewed planning document.
    - Do not overwrite or rewrite earlier planning content.
    - Do not edit the developer report.
    - Append the planner review after the latest developer report.
    - Append one review block per planning document reviewed.
    - Use the exact append format defined in this skill.

8. Update the top `## Status` section of the reviewed planning document.
   - Use the status mapping defined in this skill.
   - Update one reviewed planning document at a time.
   - Do not edit appended developer reports or appended planner review history while updating the top status.

9. Finalize only after the review result has been appended and the top status has been updated.
   - If approved, state that planner review passed, the result was appended, and the top status was updated.
   - If changes are required, state that implementation is not complete and list required fixes.
   - If review is blocked or unavailable, state that the review could not approve the implementation.

10. Archive and reset approved planning docs.
    - Do this only when the planner result is `APPROVED` or `APPROVED_WITH_NOTES`.
    - Append the full reviewed `next_step.md` or `next_step_2.md` content, including the developer report and planner review, to `history_step.md`.
    - Use a dated heading, the reviewed step title, status `Implemented`, and a short reason such as `Archived after planner approval`.
    - Preserve `history_step.md` as append-only unless the user explicitly asks for cleanup.
    - After archiving, replace the reviewed next-step file with a minimal placeholder that clearly says it is cleared and ready for the next approved plan.
    - Do not archive or reset documents with `CHANGES_REQUIRED`, `BLOCKED_NEEDS_MORE_INFO`, or `PLANNER_REVIEW_UNAVAILABLE`.

11. Commit approved step changes.
    - Do this only when the planner result is `APPROVED` or `APPROVED_WITH_NOTES`.
    - Inspect the final diff and changed-file list before staging.
    - Stage only files that belong to the reviewed step, including implementation files, tests, updated planning docs, `history_step.md`, and the reset reviewed next-step file.
    - Do not stage unrelated dirty files, out-of-scope files, local logs, generated caches, environment files, or work from another step.
    - Use a concise commit message describing the reviewed step.
    - If a focused commit cannot be made safely because the workspace has unresolved conflicts, inseparable unrelated edits, missing approval for out-of-scope files, or failing required checks, do not commit. Append or report the blocker instead.

## Planner Review Request format

Use this exact structure when asking the planner to review:

```text
Planner review requested for developer implementation.

Planning document:
<next_step.md or next_step2.md>

Planning baseline:
<original goals, requirements, acceptance criteria, architecture notes, constraints, and relevant planned tasks>

Latest developer report from planning document:
<verbatim developer report block when reasonably sized, otherwise concise excerpt plus exact important lines>

Parsed developer report:
Status: <IMPLEMENTED | PARTIAL | BLOCKED | unknown>
Commit: <commit hash or not provided>
Branch / push: <branch, remote, PR, push details, or not provided>
What changed: <summary>
Tests and validation: <tests run and results>
Proof artifacts: <artifact paths or not provided>
Known deviations: <deviations or none reported>
Known issues / risks: <risks, skipped checks, dirty files, or none reported>

Verified implementation evidence:
<changed files, diff, commit inspection, PR, patch, logs, screenshots, proof artifacts, or relevant excerpts>

Tests and validation assessment:
<tests run, commands, results, failures, skipped tests, manual checks, coverage, or "not provided">

Test coverage gap check:
<planned requirements and acceptance criteria without direct tests, missing regression / edge / negative / live proof cases, too-broad tests, and whether each gap blocks approval>

Dirty workspace / scope notes:
<dirty files, scope-check failures, out-of-scope files, or "none reported">

Known deviations from plan:
<any intentional or accidental deviations, or "none known">

Missing or unverifiable information:
<any unavailable evidence, failed verification, or "none known">

Please review the implementation against the planning document for:

1. Alignment with the documented goals and requirements.
2. Completeness against documented tasks and acceptance criteria.
3. Correctness and edge cases.
4. Architectural consistency.
5. Security, privacy, reliability, and maintainability risks.
6. Test adequacy.
7. Test coverage gaps against every documented requirement and acceptance criterion.
8. Whether dirty workspace or scope-check issues block approval.
9. Whether the implementation can be considered complete.

Return one of:

- APPROVED
- APPROVED_WITH_NOTES
- CHANGES_REQUIRED
- BLOCKED_NEEDS_MORE_INFO

For every issue, include:

- Severity: blocking / non-blocking / informational
- Location: file, component, function, behavior, test, proof artifact, dirty file, or planning-doc section
- Finding
- Required change
- Rationale
```

## Planner result meanings

### APPROVED

The implementation satisfies the planning document and may be marked complete.

### APPROVED_WITH_NOTES

The implementation satisfies the planning document and may be marked complete, but the planner has notes, caveats, or recommended follow-ups.

### CHANGES_REQUIRED

The implementation does not satisfy the planning document. Required changes must be sent back to the developer. The task must not be marked complete.

### BLOCKED_NEEDS_MORE_INFO

The planner cannot determine whether the implementation satisfies the planning document because required evidence is missing, verification failed, the planning documents conflict, dirty workspace issues are unresolved, or the implementation scope is unclear. The task must not be marked complete.

### PLANNER_REVIEW_UNAVAILABLE

Use this only if planner delegation is unavailable in the current environment. Append this result to the planning document and do not claim planner approval.

## Append format

After planner review, append the result to the end of the reviewed planning document.

Do not overwrite, delete, reorganize, or edit earlier planning content unless the user explicitly asks for that.

Append this exact Markdown structure:

```md
---

## Planner Implementation Review — <YYYY-MM-DD HH:mm timezone>

**Planning doc reviewed:** `<next_step.md or next_step2.md>`  
**Developer report reviewed:** `<timestamp, heading, commit, or "latest developer report">`  
**Implementation reference:** `<commit, branch, PR, patch, or summary>`  
**Planner result:** `<APPROVED | APPROVED_WITH_NOTES | CHANGES_REQUIRED | BLOCKED_NEEDS_MORE_INFO | PLANNER_REVIEW_UNAVAILABLE>`  
**Reviewed by:** Planner  
**Review appended by:** Planner Doc Review Skill  

### Summary

<short review summary>

### Alignment with plan

<how well the implementation matches the planning document>

### Developer report assessment

<assessment of the developer report, including whether commit, push, changed behavior, tests, proof artifacts, and dirty workspace notes were sufficient>

### Verified evidence

- <verified evidence item, or "Not verified">

### Findings

#### Blocking

- <blocking issue, or "None">

#### Non-blocking

- <non-blocking issue, or "None">

#### Informational

- <informational note, or "None">

### Test and validation assessment

<assessment of tests run and whether they are adequate>

### Test coverage gap check

<coverage gaps mapped to planned requirements and acceptance criteria, or "No blocking gaps found">

### Dirty workspace / scope assessment

<assessment of dirty workspace files, scope-check failures, or "None reported">

### Required developer actions

- <required action, or "None">

### Final decision

<clear completion decision>
```

## Appending rules

When appending review results:

- Always append to the bottom of the relevant planning document.
- Always append after the latest developer report when that report is present.
- Always include the timestamp.
- Always include the planning document name.
- Always include the developer report reference.
- Always include the implementation reference.
- Always include the planner result.
- Always include blocking findings, even if the list is `None`.
- Always include required developer actions, even if the list is `None`.
- Always include the `### Test coverage gap check` section and explicitly state whether any missing tests or proof artifacts block approval.
- If both `next_step.md` and `next_step2.md` were reviewed, append a separate review block to each file.
- If the implementation only partially satisfies the planning document, use `CHANGES_REQUIRED` unless the remaining work is explicitly non-blocking.
- If the planner review cannot be performed, append `PLANNER_REVIEW_UNAVAILABLE` and explain why.
- If the planner review cannot verify the commit, diff, tests, or proof artifacts and that evidence is required for approval, use `BLOCKED_NEEDS_MORE_INFO`.

## Top status update

After appending the planner review, update the first `## Status` section near the top of each reviewed planning document.

Status update rules:

- If the document has a top `## Status` section, replace only that section's body, ending before the next `## ` heading.
- If the document has no top `## Status` section, insert one immediately after the title or frontmatter.
- Do not modify appended developer reports or appended planner review blocks while changing the top status.
- Preserve the appended planner review as the detailed audit trail; the top status is only a compact current-state summary.

Use this mapping:

- `APPROVED`: `Status: Implemented and planner-reviewed — APPROVED (<YYYY-MM-DD HH:mm timezone>)`
- `APPROVED_WITH_NOTES`: `Status: Implemented and planner-reviewed — APPROVED_WITH_NOTES (<YYYY-MM-DD HH:mm timezone>)`
- `CHANGES_REQUIRED`: `Status: Changes required after planner review (<YYYY-MM-DD HH:mm timezone>)`
- `BLOCKED_NEEDS_MORE_INFO`: `Status: Blocked pending planner-review evidence (<YYYY-MM-DD HH:mm timezone>)`
- `PLANNER_REVIEW_UNAVAILABLE`: `Status: Planner review unavailable; not planner-approved (<YYYY-MM-DD HH:mm timezone>)`

## Post-approval archive and reset

After an `APPROVED` or `APPROVED_WITH_NOTES` result has been appended and the top status has been updated:

1. Append the entire reviewed planning document to `history_step.md`.
   - Archive `next_step.md` and `next_step_2.md` separately when both were reviewed.
   - Use this format:

```md
## YYYY-MM-DD — <Reviewed step title>

Status: Implemented

Reason:
- Archived after planner approval.

Archived content:
<full reviewed next-step document content>
```

2. Reset the reviewed planning document for future updates.
   - Replace its contents with a short placeholder:

```md
# Next Step

## Status

Status: Cleared after planner-approved archive; ready for the next approved plan.
```

   - For `next_step_2.md`, use `# Next Step 2`.
   - Do not leave the implemented plan active after it has been approved.

3. Include the archive and reset in the focused commit for the reviewed step.

## Completion rules

If planner result is `APPROVED`:

- Append the review.
- Update the top status to `Implemented and planner-reviewed — APPROVED`.
- Archive the reviewed planning document to `history_step.md`.
- Reset the reviewed planning document for the next approved plan.
- Inspect the final diff and commit only the reviewed step changes.
- The implementation may be marked complete after the focused commit succeeds.
- Final response should mention that the review was appended, the top status was updated, the approved step was archived and reset, and the approved step was committed.

If planner result is `APPROVED_WITH_NOTES`:

- Append the review.
- Update the top status to `Implemented and planner-reviewed — APPROVED_WITH_NOTES`.
- Archive the reviewed planning document to `history_step.md`.
- Reset the reviewed planning document for the next approved plan.
- Inspect the final diff and commit only the reviewed step changes.
- The implementation may be marked complete after the focused commit succeeds.
- Final response should include the planner notes and commit result.

If planner result is `CHANGES_REQUIRED`:

- Append the review.
- Update the top status to `Changes required after planner review`.
- Do not mark the implementation complete.
- Send blocking findings and required developer actions back to the developer.

If planner result is `BLOCKED_NEEDS_MORE_INFO`:

- Append the blocked review.
- Update the top status to `Blocked pending planner-review evidence`.
- Do not mark the implementation complete.
- Gather or request the missing evidence.

If planner review is unavailable:

- Append `PLANNER_REVIEW_UNAVAILABLE`.
- Update the top status to `Planner review unavailable; not planner-approved`.
- Do not claim the implementation was planner-approved.
- Clearly state what prevented review.

## Final response requirements

When reporting back to the user, include:

- Which planning document was reviewed.
- Which developer report or implementation reference was reviewed.
- Whether the planner review was completed.
- Whether the result was appended to the planning document.
- Whether the top status was updated.
- Whether the reviewed planning document was archived to `history_step.md`.
- Whether the reviewed planning document was reset for the next approved plan.
- Whether the approved step was committed, or why a safe focused commit could not be made.
- The planner result.
- Whether implementation is approved or needs changes.
- Blocking issues, if any.
- Required developer actions, if any.

Never hide the fact that planner review was skipped, blocked, unavailable, or based on incomplete evidence.

## Example developer report

This skill should recognize a report like this as valid developer evidence:

```text
Implemented, committed, and pushed.
Commit:
12996a72 Fix: 分离 route analysis COG endpoint
Push:
lzjdev -> origin/lzjdev using proxy http://127.0.0.1:7897.
What changed:
RouteAnalysisWorkflow no longer forwards plan-level cog_base_url into cog_resolve_raster_source, so stale MCP-looking COG URLs cannot override configured Gateway delivery URLs.
Added prod-shaped tests proving display_url comes from COG_BASE_URL / Gateway :8000/api/cog.
MCP_SERVICE_URL stays for MCP APIs / clip endpoint.
mcp_cog_clip sends relative cog_url, not public HTTP TIFF URLs.

Updated next_step.md with implemented status and live proof artifact.
Checks run:
Source resolver: 1 passed, 19 deselected
Route sampling / route analysis: 30 passed, 133 deselected
Command / full gate: 10 passed, 10 deselected
Focused endpoint suite: 19 passed, 164 deselected
Opt-in live: 2 passed, 3 skipped; artifact at apps/agent_core/.test_logs/route_sampling_mcp_cog_clip_live_20260630_180325.json
git diff --check -- apps/agent_core: passed
Scope check still fails due pre-existing out-of-scope dirty files:
apps/frontend/quasar_cesium/package-lock.json
apps/mcp_servers/mcp_servers/services/ais_clickhouse_service.py
docker-compose.dev.yml
scripts/build-prod-all.ps1
start-dev.ps1
```

When reviewing a report like this, the planner review request must include:

- Commit `12996a72`.
- The route-analysis COG endpoint behavior claim.
- The test results and live proof artifact path.
- The `git diff --check -- apps/agent_core` result.
- The failed scope check and the listed dirty files.
- Whether the dirty files are verified as pre-existing and out of scope.

## Example final response after approval

```text
Planner review completed and appended to next_step.md.

Developer report reviewed: commit 12996a72
Planner result: APPROVED

The implementation satisfies the planning document and may be marked complete.
```

## Example final response when changes are required

```text
Planner review completed and appended to next_step2.md.

Developer report reviewed: commit 12996a72
Planner result: CHANGES_REQUIRED

The implementation is not complete. Required developer actions:

- Add the missing regression test for the documented failure case.
- Restore the planned error-handling behavior from next_step2.md.
- Document or fix the deviation from the planned service boundary.
```
