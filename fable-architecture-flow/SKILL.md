---
name: fable-architecture-flow
description: Design-first delivery workflow for using a strongest or most expensive coding model only on architecture, not implementation. Use when a user asks for the Fable method, S1A/S1B/S1B review/S2/S3/S4, turning a rough software task into a reviewed architecture contract, mechanical task tracker, or one-item execution loop without copying long prompts.
---

# Fable Architecture Flow

## Core Idea

Spend the strongest or most expensive model on design judgment only. Produce documents that lock down direction, architecture, review findings, and a mechanical execution tracker before any implementation begins.

Use this skill to do the work directly. Do not ask the user to copy long prompts unless they explicitly want reusable prompt text.

## Stage Selection

Infer the stage from the user's request:

- Rough idea or "help me design this": run S1A.
- Approved S1A plus codebase or system context: run S1B.
- Existing S1B draft: run S1B review.
- Approved S1B: run S2/S3.
- Existing tracker and explicit implementation request: run one S4 item.
- "Do the whole method" or "self-service package": run as far as the gates allow, and stop at any unresolved decision.

If the user provides enough context, proceed. Ask only for blocking inputs that cannot be inferred, such as the target repo, required constraints, or a business decision the architecture must not guess.

## Non-Negotiables

- During S1A, S1B, S1B review, and S2/S3, do not write production code.
- S1A discusses direction, mechanism, tradeoffs, risks, and user decisions. It must not contain function signatures or implementation details.
- S1B writes architecture contracts, not code. It must include signatures, data structures, insertion points, fail-loud behavior, migration mapping, deletion items, ordered cuts, rollback boundaries, and validation commands.
- S1B review is adversarial. Try to prove the draft cannot be handed to a fresh AI. Patch the architecture text, then record what changed.
- S2/S3 is mechanical transcription from S1B section 4 into a tracker and execution contract. If S1B is not specific enough, report blockers instead of inventing design.
- S4 executes only the first unchecked tracker item unless the user explicitly asks for a driver or loop. Do not claim verification unless the command actually ran.
- Do not build or publish an unattended overnight automation driver as part of this skill. Keep S4 manual or driver-agnostic unless the user separately requests automation and its safety policy.

## Working Procedure

1. Read `references/stage-templates.md` before writing any S1A, S1B, review, S2/S3, or S4 deliverable.
2. Gather context from the user's description and, when relevant, inspect the target repository or supplied documents.
3. Write the requested stage output using the matching template.
4. Mark gates clearly:
   - `needs user decision` when a decision is required.
   - `ready for S1B` only when S1A has no blocking decision.
   - `ready for S2/S3` only when S1B review concludes the architecture can be handed to a fresh AI.
   - `ready for S4` only when every tracker item has a concrete verify command.
5. When creating files, prefer concise Markdown deliverables such as:
   - `S1A_PLAN.md`
   - `S1B_ARCHITECTURE.md`
   - `S1B_REVIEWED_ARCHITECTURE.md`
   - `S2_S3_TRACKER.md`
   - `EXECUTION_LOG.md`

## Output Discipline

Be concrete and fail loud:

- Name missing inputs and exact consequences.
- Use precise file paths, function names, schema fields, and commands when available.
- Separate "must", "should", and "optional" gaps.
- Put user decisions in plain language: problem, options, consequences, recommendation, default action.
- Keep S2/S3 faithful to S1B. A tracker item must be traceable to exactly one ordered cut.
- For implementation requests, change only the selected S4 item, update the tracker/log, run or report the verify command, and stop.
