# Stage Templates

Use these templates as output contracts. Adapt names and section counts to the task, but keep the gates and fail-loud behavior.

## S1A: Direction Plan

Purpose: let the user judge whether the direction is right without reading code.

Required sections:

1. Target end state: one sentence.
2. Mechanism: explain how it works. For each key decision, list options, consequences, recommendation, and default action.
3. Current state and gaps: missing capabilities, labeled `must`, `should`, or `optional`.
4. Critical risks: likely failure points and uncertainty. Do not soften them.
5. User decisions: plain-language list with problem, options, consequences, recommendation, and default action.
6. Gate: `ready for S1B` or `needs user decision`.

Hard boundary: do not include code, function signatures, exact patches, or file-by-file implementation instructions.

## S1B: Signature-Level Architecture

Purpose: make the design specific enough that a fresh human or AI can implement the same system without inventing architecture.

Required sections:

0. Target end state: one sentence.
1. Current state: module-by-module structure and gap list, each marked `ready` or `needs design`.
2. Target architecture: for each gap, specify:
   - Interface signatures: new or changed classes, functions, methods, and fields with types and file paths.
   - Data structures or schema: persisted formats, config keys, enum values, units, and required fields.
   - Insertion points: file path and call site where the new path is wired.
   - Fail-loud points: invalid inputs, missing fields, stale data, corrupt state, permission boundaries, postconditions, and error handling.
3. Migration mapping and deletion items:
   - Map each caller from current to target behavior.
   - Name old paths, fallbacks, duplicate flags, or compatibility shims to delete after the new path is wired.
4. Ordered cuts:
   - One line per cut.
   - Include scope, touched files, dependency, parallel safety, rollback boundary, and narrow verify command.
   - Keep each cut to 10 touched files or fewer. Split larger cuts.
5. Verification plan:
   - Narrow verify command per cut.
   - Full verification command after all cuts are merged.
6. Design boundaries and risks:
   - Explicit non-goals.
   - Hard red lines.
   - Residual risks.
7. User decisions:
   - Same plain-language format as S1A.
8. Gate: `ready for S1B review` or `needs user decision`.

## S1B Review: Adversarial Review

Purpose: prove whether S1B can be handed to a fresh AI.

Review checklist:

- Are interfaces, fields, and schema truly signature-level?
- Are insertion points specific and executable?
- Are migration mappings and deletion items complete?
- Are fail-loud points and boundary conditions explicit?
- Can every ordered cut become one tracker item without new design?
- Are there contradictions, missing files, nonexistent functions, or unstated dependencies?

Output:

1. Revised S1B, with serious findings folded into the body.
2. Review record:
   - Review date.
   - Blocking and high-priority findings.
   - Revisions made.
   - Remaining user decisions.
   - Conclusion: `can finalize` or `return to S1B`.

## S2: Build Packet

Purpose: mechanically turn finalized S1B into an execution tracker and reusable one-item contract.

Inputs:

- Final S1B with section 4 ordered cuts.
- S1B review conclusion `can finalize`.

Output:

1. Tracker:

```markdown
- [ ] TASK-1: Short imperative title
  source: S1B section 4 cut N
  scope: files or modules
  verify: full command
  rollback: boundary or command
```

2. Execution contract:

```markdown
Read S1A, final S1B, S1B review record, and this tracker.
Choose the first unchecked task only.
Implement only that task.
Fail loud on missing inputs, stale data, unclear design, or invalid postconditions.
Do not add new architecture. If the tracker or S1B is unclear, stop and report the blocker.
Update the tracker and append one execution-log entry.
Run the task verify command if possible.
Output status, changes, verification result, and next task.
```

3. Blockers:
   - List every S1B cut that cannot become a tracker item without new design.
   - Do not invent missing verify commands or scope.

Gate: `ready for S3` only when every unchecked task has a concrete verify command.

## S3: One-Item Build

Purpose: execute exactly one tracker item.

Procedure:

1. Read S1A, final S1B, review record, tracker, and execution log.
2. Select the first unchecked task.
3. Implement only that task.
4. Update the tracker checkbox only if the task is actually complete.
5. Append an execution-log entry:
   - Timestamp.
   - Task ID.
   - Files changed.
   - Verify command.
   - Verify result.
   - Next task or blocker.
6. Run the verify command when safe and available. If not run, say `not verified` and explain why.
7. Stop after one item.

Output status values:

- `continue`: task completed and more unchecked tasks remain.
- `complete`: task completed and tracker is empty.
- `blocked`: user decision or missing input is required.
- `failed`: attempted execution failed and needs diagnosis.
