# Architect Then Build

This repository packages the "expensive model designs, cheap model builds" method as a reusable Codex skill.

## Skill

Use the self-contained skill folder:

- `architect-then-build/`

Example invocation:

```text
Use $architect-then-build to turn this task into reviewed architecture and a one-item build tracker.
```

## What It Does

- S1A: turn a rough task into a direction plan the user can review without reading code.
- S1B: turn the approved plan into signature-level implementation architecture.
- S1B review: adversarially patch holes before handing the plan to another AI.
- S2: mechanically convert the finalized architecture into a build packet: tracker plus execution contract.
- S3: execute exactly one tracker item at a time, with verification discipline.

The skill intentionally does not publish an unattended overnight execution driver. It keeps the public workflow manual or driver-agnostic.

## Naming Note

In the older draft, S2 and S3 were written together because the public version did not include the private driver layer. This version makes the public workflow explicit: S2 creates the build packet, and S3 executes one tracker item. In an internal automated driver, S3 can instead mean arming/preflight before a separate run loop, but that driver layer is not part of this public skill.

## Source Material

- `ARTICLE.md`: narrative explanation.
- `PROMPTS.md`: original copy-paste prompt version, updated to the public S1A, S1B, review, S2, and S3 flow.
- `TWITTER.md`: short-form sharing copy.
