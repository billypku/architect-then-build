# Fable Architecture Flow

This repository packages the S1 -> S4 "expensive model writes architecture, cheap model executes" method as a reusable Codex skill.

## Skill

Use the self-contained skill folder:

- `fable-architecture-flow/`

Example invocation:

```text
Use $fable-architecture-flow to turn this task into S1A/S1B architecture, adversarial review, and an executable tracker.
```

## What It Does

- S1A: turn a rough task into a direction plan the user can review without reading code.
- S1B: turn the approved plan into signature-level implementation architecture.
- S1B review: adversarially patch holes before handing the plan to another AI.
- S2/S3: mechanically convert the finalized architecture into a tracker and execution contract.
- S4: execute exactly one tracker item at a time, with verification discipline.

The skill intentionally does not publish an unattended overnight execution driver. It keeps the public workflow manual or driver-agnostic.

## Source Material

- `ARTICLE.md`: narrative explanation.
- `PROMPTS_S1_S4.md`: original copy-paste prompt version.
- `TWITTER.md`: short-form sharing copy.
