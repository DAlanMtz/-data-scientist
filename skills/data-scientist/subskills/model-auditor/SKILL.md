---
name: model-auditor
description: Use when auditing, validating, challenging, or stress-testing an existing model, notebook, backtest, experiment, scoring system, or model claim. Covers leakage and target integrity, validation design, metrics and baselines, calibration and thresholds, and production readiness. Produces severity-ranked findings and a release decision (Block / Caution / Pass).
---

# Model Auditor

## Purpose

Use this sub-skill to audit, validate, or challenge an existing model, notebook, backtest, experiment, scoring system, or model claim. The posture is evidence-first and skeptical: assume claims need verification until the available evidence supports them.

This sub-skill provides checklist structure, a severity-ranked findings format, and a release decision framework. It does not replace the parent `data-scientist` skill's methodology guidance — it applies that judgment in interrogation mode against work that already exists.

## When To Use This Sub-Skill

Activate when:

- The user asks to audit, validate, review, stress-test, verify, inspect, or challenge a model.
- The user asks for a production-readiness check on a model or notebook.
- The user asks to check for leakage, overfitting, data contamination, or suspicious performance.
- The user says "something seems off with our performance/results."
- The user asks whether a model is ready to deploy.
- The user presents a model claim (e.g., "our model achieves AUC 0.87") and wants it evaluated.
- The task involves a backtest, experiment, or scoring system that needs its methodology challenged.

## When Not To Use This Sub-Skill

| Situation | Use instead |
|---|---|
| First-pass EDA, data profiling, exploratory investigation | Parent skill, Research Mode |
| Building a new model from scratch | Parent skill, Build Mode |
| Dashboard design, visual reports, HTML output | Parent skill → `dashboard-designer` |
| Metric selection for a new project | Parent skill |
| Investigating production drift behavior | Parent skill, Production Mode first |

## Routing Table

| Task | Use |
|---|---|
| Audit an existing model, notebook, backtest, or experiment | `model-auditor` |
| Deployed model showing drift → investigate production behavior | Parent skill, Production Mode first |
| Deployed model → challenge validity, deployment readiness, leakage, metrics, or claims | `model-auditor` |
| Design a new validation strategy | Parent skill |
| Build or generate an HTML dashboard | Parent skill → `dashboard-designer` |
| Full lifecycle data science project | Parent skill |

## Audit Workflow

1. **State the model claim.** What does the model do? What performance is claimed? What is the source of the claim?
2. **Identify the data population.** Who, when (date range), what grain (one row = ?), any known population shifts.
3. **Check leakage and target integrity.** → `checklists/leakage-and-target-integrity.md`
4. **Check validation and splits.** → `checklists/validation-and-splits.md`
5. **Check metrics and baselines.** → `checklists/metrics-and-baselines.md`
6. **Check calibration and thresholds.** Skip if the model does not produce probabilities or continuous scores. → `checklists/calibration-and-thresholds.md`
7. **Check production readiness.** Skip if pre-production. → `checklists/production-readiness.md`
8. **Produce a severity-ranked audit report.** → `templates/audit-report.md` with release decision: **Block / Caution / Pass**

## Severity

Use `Critical / High / Medium / Low / Informational` from `../../workflow/severity-levels.md`. Do not define a separate severity scale. The release decision (`Block / Caution / Pass`) is a separate final field derived from the severity of findings — it is not a severity level itself. See `templates/severity-table.md` for release decision guidance.

## Supporting Files

**Checklists** — load each domain relevant to the audit:
- `checklists/leakage-and-target-integrity.md`
- `checklists/validation-and-splits.md`
- `checklists/metrics-and-baselines.md`
- `checklists/calibration-and-thresholds.md`
- `checklists/production-readiness.md`

**Templates** — produce a structured report:
- `templates/audit-report.md` — findings table, open items, release decision, and next action
- `templates/severity-table.md` — release decision guidance keyed to severity levels

**Example prompt:**
- `examples/notebook-audit-prompt.md` — copy-paste prompt to activate this sub-skill against a notebook or modeling workflow
