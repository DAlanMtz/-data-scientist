# Stage Index — Quick Reference

One-page map of the full lifecycle. Use this to orient quickly: find the stage, identify the gate, locate the artifact and template, confirm the checklist, check definition of done, and know the stop condition before proceeding.

---

| Stage | Name | Gate to pass | Main artifact | Main template | Main checklist | Key references | Stop condition |
|---|---|---|---|---|---|---|---|
| **0** | Intake and Framing | Framing Gate | Project Brief | `project-brief-template.md` | `pre-modeling-checklist.md` §Business | `lifecycle.md` S0 | No decision, stakeholder, or success metric defined |
| **1** | Data Understanding and Quality Audit | Data Readiness Gate | Data Audit | `data-audit-report-template.md` | `data-quality-checklist.md` | `validation-and-leakage-checklist.md` | Leakage candidates unresolved; grain unconfirmed; data insufficient |
| **2** | Exploratory Analysis | No named gate — exit criteria in lifecycle.md S2 | EDA Summary | `eda-summary-template.md` | `pre-modeling-checklist.md` §Target Definition | `diagnostics-guide.md` | No hypotheses documented; modeling readiness unknown |
| **3** | Target, Feature, and Validation Design | Validation Gate | Validation Plan | `validation-plan-template.md` | `pre-modeling-checklist.md` (full) | `validation-and-leakage-checklist.md`, `metrics-guide.md` | Target undefined; prediction point missing; split strategy unjustified |
| **4** | Baseline Modeling | Baseline Gate | Experiment Log (baseline entry) | `experiment-log-template.md` | `pre-modeling-checklist.md` §Baseline And Metrics | `model-selection-guide.md`, `metrics-guide.md` | No baseline built; baseline uses future features; result from training set only |
| **5** | Model Development and Comparison | Model Comparison Gate | Experiment Log (full) + Model Comparison Report | `modeling-plan-template.md`, `experiment-log-template.md`, `model-comparison-report-template.md` | `supervised-learning-checklist.md` | `model-selection-guide.md`, `metrics-guide.md` | Only one model evaluated; tuning before split locked; model selected on training performance |
| **6** | Diagnostics and Error Analysis | Diagnostics Gate | Error Analysis Report | `error-analysis-report-template.md` | `model-audit-checklist.md`, `responsible-ai-checklist.md` | `diagnostics-guide.md` | Subgroup analysis skipped; systematic errors uninvestigated; no out-of-time check |
| **7** | Calibration, Thresholds, and Decision Policy | Calibration/Decision Gate | Calibration Report + Decision Memo | `calibration-report-template.md`, `decision-memo-template.md` | No dedicated checklist — see quality-gates.md Calibration/Decision Gate | `metrics-guide.md`, `diagnostics-guide.md` | Threshold not analyzed; calibration unchecked; decision policy undocumented |
| **8** | Interpretation and Reporting | Interpretation Gate | Model Card + Business Report | `model-card-template.md`, `analysis-report-template.md` | `responsible-ai-checklist.md` | `interpretation-templates.md`, `reporting-templates.md` | Model card missing; limits not documented; no business translation |
| **9** | Deployment Readiness | Production Gate | Deployment Readiness Report | `deployment-readiness-report-template.md` | `deployment-checklist.md`, `responsible-ai-checklist.md` | `production-readiness-guide.md`, `production-pipeline-template.md`, `data-quality-and-contracts.md` | Input/output contract informal; artifact unversioned; monitoring plan absent |
| **10** | Monitoring and Iteration | Monitoring Gate _(ongoing)_ | Monitoring Plan | `monitoring-plan-template.md` | `deployment-checklist.md` §Monitoring And Alerting | `model-monitoring-and-drift.md`, `diagnostics-guide.md` | No monitoring active; no retraining trigger; no review schedule |

---

## How to Use This Index

1. **Identify the stage** — Where is the current work in the lifecycle? If unsure, use `lifecycle.md` to read the full stage descriptions.
2. **Check the gate** — Has the named gate passed? If not, return to the prior stage. See `quality-gates.md` for pass requirements.
3. **Find the artifact** — What should be produced? See `artifacts.md` for minimum and strong-version contents.
4. **Open the template** — Use the template in `templates/` to structure the output.
5. **Run the checklist** — The listed checklist confirms the work is complete before the gate is declared passed.
6. **Check definition of done** — Before calling an artifact complete, verify `definition-of-done.md`.
7. **Apply shortcut guardrails** — If the user or assistant is rationalizing a shortcut, use `rationalization-guardrails.md`.
8. **Load the reference** — The key reference provides depth for the method or standard in question.
9. **Apply the stop condition** — If the stop condition is true, do not advance. Name it explicitly and route back.

---

## Shortcut: Common Entry Points

| Request type | Likely stage | First action |
|---|---|---|
| "Help me build a model for X" | Stage 0 | Open `project-brief-template.md` |
| "Review this notebook / dataset" | Stage 1 or 6 | Open `data-audit-report-template.md` or `error-analysis-report-template.md` |
| "Is this feature leaking?" | Stage 1 or 3 | Check `validation-and-leakage-checklist.md`; update Data Audit |
| "Which model should I use?" | Stage 3 or 5 | Confirm Validation Gate passed; open `modeling-plan-template.md` |
| "How do I evaluate performance?" | Stage 3 or 7 | Open `validation-plan-template.md` or `decision-memo-template.md` |
| "Is this ready to deploy?" | Stage 9 | Open `deployment-readiness-report-template.md`; check Production Gate |
| "Something seems off in production" | Stage 10 | Open `monitoring-plan-template.md`; apply `severity-levels.md` |
| "Can we skip this check?" | Any gated stage | Open `rationalization-guardrails.md`; require minimum evidence |
| "Is this artifact done?" | Any artifact handoff | Open `definition-of-done.md`; check blocking gaps |

---

## Severity Levels Quick Reference

See `severity-levels.md` for full definitions.

| Level | Gate impact | Work stops? |
|---|---|---|
| Critical | Blocks gate | Yes |
| High | Blocks gate (conditionally) | Conditionally |
| Medium | Does not block | No |
| Low | Does not block | No |
| Informational | Does not block | No |
