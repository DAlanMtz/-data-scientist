# Workflow Layer

**Version:** 1.2 | **Last updated:** 2026-05-14

## Purpose

The workflow layer is the operating system for the `data-scientist` skill. It does not replace the references, templates, checklists, or examples. It tells the assistant **when** to use them, **in what order**, and **at what standard**.

Without a workflow layer, a skilled assistant still drifts: it answers the question asked rather than the question that should be asked. It builds models before the target is defined, skips baselines, misses leakage, and delivers outputs without knowing whether the project is at Stage 2 or Stage 8. The workflow layer prevents that drift.

## What This Layer Does

| Layer element | What it provides |
|---|---|
| `stage-index.md` | One-page quick reference — stage → gate → artifact → template → checklist → stop condition |
| `lifecycle.md` | The full arc of a data science project — stages, questions, evidence, and exit criteria |
| `stages.md` | Numbered stages with do/don't lists, inputs, outputs, and relevant supporting files |
| `quality-gates.md` | Explicit pass/fail criteria between stages — the checkpoint before advancing |
| `artifacts.md` | Standard deliverables — what to produce, when, and at what level of completeness |
| `definition-of-done.md` | Final completion checks for common data science deliverables |
| `rationalization-guardrails.md` | Shortcut prevention layer for common bad data science rationalizations |
| `response-patterns.md` | How to handle common user requests with discipline and without over-engineering |
| `severity-levels.md` | How to classify and communicate audit findings — Critical through Informational |

## What This Layer Does Not Do

- It does not replace `references/methodology-guide.md` or any other reference file. Those contain domain knowledge; this file contains structure.
- It does not replace templates or checklists. Those contain content; this layer routes to them.
- It does not enforce a rigid waterfall. Projects loop back, skip stages for good reason, and operate under real constraints. The workflow layer names those choices explicitly so they are deliberate rather than accidental.

## How To Use This Layer

When a new request arrives, the assistant should:

1. **Identify the stage** — Where is this project in the lifecycle? (`stages.md`)
2. **Check the gate** — Is the current stage complete enough to advance? (`quality-gates.md`)
3. **Select the artifact** — What should be produced at this stage? (`artifacts.md`)
4. **Apply severity** — If auditing or reviewing, classify findings. (`severity-levels.md`)
5. **Route to content** — Pull the relevant reference, template, checklist, or example.
6. **Apply the response pattern** — Match the user's request type to the correct posture. (`response-patterns.md`)
7. **Check definition of done** — Before declaring a deliverable complete, verify `definition-of-done.md`.
8. **Use guardrails** — When a shortcut appears, apply `rationalization-guardrails.md` and require minimum evidence.

## Proportional Use

Apply the workflow proportionally. Quick conceptual, syntax, or method-definition questions can be answered directly and briefly. Project-level modeling, auditing, reporting, validation, dashboard review, or production-readiness work should use the stage/gate/artifact workflow.

## Design Principles

- **Stage before speed.** Correctly placing the work in the lifecycle produces better outputs than jumping to the first plausible action.
- **Gates before advancement.** Incomplete framing, missing baselines, and unvalidated splits are more expensive to fix after modeling than before.
- **Artifacts over advice.** Concrete deliverables — a data audit, a validation plan, a model card — are more useful and more honest than general commentary.
- **Severity over vagueness.** Calling a finding Critical, High, Medium, Low, or Informational is more actionable than calling it "a concern."
- **Assumptions over silence.** When proceeding with incomplete information, name the assumptions and their risks. Do not silently fill gaps.
- **Done means checkable.** A deliverable is not complete until it meets the appropriate definition of done or names the blocking gaps.
