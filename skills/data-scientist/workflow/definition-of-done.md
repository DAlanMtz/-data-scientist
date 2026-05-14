# Definition Of Done

Use this file before treating a data science artifact as complete, reliable, or ready for handoff. The definitions are intentionally concrete: an artifact is not done because it is long or polished; it is done when it contains the evidence needed for the next decision.

---

## Project Brief

- **Minimum done criteria:** Defines decision, stakeholder, unit of analysis, time window, population, success metric, constraints, and open questions.
- **Strong done criteria:** Adds current process, cost of errors, decision cadence, responsible-use constraints, assumptions, and out-of-scope items.
- **Blocking gaps:** No decision owner; success metric only technical; grain unclear; no time window.
- **Quality gate connection:** Framing Gate.
- **Related template:** `templates/project-brief-template.md`.

## Data Audit Report

- **Minimum done criteria:** Lists data sources, grain, row counts, date coverage, schema, missingness, duplicates, key integrity, and leakage candidates.
- **Strong done criteria:** Adds data lineage, freshness, join validation, range/category checks, quality issue severity, and sufficiency statement.
- **Blocking gaps:** Grain unconfirmed; leakage candidates unresolved; no key or date checks; source coverage unknown.
- **Quality gate connection:** Data Readiness Gate.
- **Related template:** `templates/data-audit-report-template.md`.

## EDA Summary

- **Minimum done criteria:** Summarizes target distribution, key feature distributions, relationships, segments, outliers, data quality flags, and modeling-readiness implications.
- **Strong done criteria:** Adds visual captions, cohort/time views, uncertainty notes, feature ideas with leakage risk, and recommended next stage.
- **Blocking gaps:** Charts without takeaways; target timing not checked; no data quality implications; no readiness statement.
- **Quality gate connection:** Stage 2 exit criteria.
- **Related template:** `templates/eda-summary-template.md`.

## Validation Plan

- **Minimum done criteria:** Defines target, grain, prediction point, split strategy, leakage controls, baseline, metrics, and final holdout policy.
- **Strong done criteria:** Adds group/time-aware rationale, cross-validation design, calibration plan, subgroup analysis, and test-set protection rules.
- **Blocking gaps:** Split strategy unjustified; metric not tied to decision; preprocessing leakage unaddressed; no baseline.
- **Quality gate connection:** Validation Gate.
- **Related template:** `templates/validation-plan-template.md`.

## Modeling Plan

- **Minimum done criteria:** Defines target, grain, prediction point, available features, leakage risks, validation strategy, baseline, candidate models, metrics, error analysis plan, and expected artifacts.
- **Strong done criteria:** Adds feature set versions, tuning protocol, model complexity rationale, interpretability requirements, deployment constraints, and responsible-use review.
- **Blocking gaps:** Model family selected before validation plan; no baseline; no feature availability review; no error analysis plan.
- **Quality gate connection:** Validation Gate and Baseline Gate.
- **Related template:** `templates/modeling-plan-template.md`.

## Experiment Log

- **Minimum done criteria:** Records experiment ID, date, owner, dataset version, split, feature set, method, hyperparameters, metrics, and decision.
- **Strong done criteria:** Adds hypothesis, diagnostics, error analysis, responsible-use notes, runtime, artifact links, and follow-up actions.
- **Blocking gaps:** Metrics without data/split version; only successful runs logged; test-set tuning not disclosed.
- **Quality gate connection:** Baseline Gate and Model Comparison Gate.
- **Related template:** `templates/experiment-log-template.md`.

## Model Comparison Report

- **Minimum done criteria:** Compares baseline and candidate models on the same data, split, metric, and target definition.
- **Strong done criteria:** Adds validation variance, calibration, subgroup performance, error analysis, interpretability, runtime, deployment cost, and model selection rationale.
- **Blocking gaps:** No baseline; inconsistent splits; model chosen on training performance; metric not decision-relevant.
- **Quality gate connection:** Model Comparison Gate.
- **Related template:** `templates/model-comparison-report-template.md`.

## Error Analysis Report

- **Minimum done criteria:** Reviews error cases, error by segment/time/source, systematic failure modes, and recommended fixes.
- **Strong done criteria:** Adds confidence/error severity, subgroup review, data quality linkage, threshold sensitivity, and business impact of errors.
- **Blocking gaps:** Only aggregate metrics; no false positive/false negative or residual review; subgroup failures ignored.
- **Quality gate connection:** Diagnostics Gate.
- **Related template:** `templates/error-analysis-report-template.md`.

## Calibration Report

- **Minimum done criteria:** Shows calibration curve or score-band observed rates, Brier/log loss where relevant, and probability-use implications.
- **Strong done criteria:** Adds group-level calibration, threshold tradeoffs, recalibration options, and decision impact.
- **Blocking gaps:** Scores used as probabilities with no calibration check; threshold chosen without cost/capacity rationale.
- **Quality gate connection:** Calibration/Decision Gate.
- **Related template:** `templates/calibration-report-template.md`.

## Decision Memo

- **Minimum done criteria:** States decision, recommendation, evidence, expected impact, risks, assumptions, and next action.
- **Strong done criteria:** Adds options considered, tradeoff curves, sensitivity analysis, owner, monitoring plan, and review trigger.
- **Blocking gaps:** Recommendation not tied to action; causal overclaiming; no uncertainty or limitation statement.
- **Quality gate connection:** Calibration/Decision Gate and Interpretation Gate.
- **Related template:** `templates/decision-memo-template.md`.

## Analysis Report

- **Minimum done criteria:** Contains executive summary, business question, data used, method, key findings, interpretation, limitations, recommendation, and next steps.
- **Strong done criteria:** Adds reproducibility details, visual captions, uncertainty, denominator checks, and appendix diagnostics.
- **Blocking gaps:** Findings without evidence; visuals without captions; limitations hidden; recommendation missing.
- **Quality gate connection:** Interpretation Gate.
- **Related template:** `templates/analysis-report-template.md`.

## Model Card

- **Minimum done criteria:** Defines model name, purpose, intended use, non-intended use, data, target, features, training/evaluation method, metrics, limitations, responsible AI, monitoring, and approval status.
- **Strong done criteria:** Adds subgroup performance, calibration, human review path, rollback/retraining plan, and non-intended use examples.
- **Blocking gaps:** No intended use; no limitations; no monitoring plan; high-impact model lacks responsible-use review.
- **Quality gate connection:** Interpretation Gate and Production Gate.
- **Related template:** `templates/model-card-template.md`.

## Deployment Readiness Report

- **Minimum done criteria:** Covers reproducibility, environment, data validation, feature consistency, artifact storage, logging, monitoring, owner, rollback, and retraining.
- **Strong done criteria:** Adds dry run/shadow mode results, tests, incident response, privacy/security review, and champion/challenger process.
- **Blocking gaps:** Notebook-only process; no input/output contracts; no monitoring; no rollback; no owner.
- **Quality gate connection:** Production Gate.
- **Related template:** `templates/deployment-readiness-report-template.md`.

## Monitoring Plan

- **Minimum done criteria:** Defines monitored inputs, data quality, feature drift, prediction drift, performance, calibration, business KPIs, alert thresholds, owners, and review cadence.
- **Strong done criteria:** Adds delayed-label handling, subgroup monitoring, incident workflow, retraining triggers, champion/challenger comparison, and dashboard/runbook links.
- **Blocking gaps:** No label arrival plan; no alert owner; no retraining trigger; only system uptime monitored.
- **Quality gate connection:** Monitoring Gate.
- **Related template:** `templates/monitoring-plan-template.md`.

## Visual Report

- **Minimum done criteria:** Defines audience, decision supported, business question, data used, executive visual summary, key metrics, chart inventory, findings, limitations, recommendation, and next action.
- **Strong done criteria:** Adds a clear visual story sequence, consistent design system, takeaway captions, uncertainty/denominator notes, appendix separation, and export/readability review.
- **Blocking gaps:** Charts without questions; no decision supported; captions only name chart types; inconsistent metric definitions; recommendation missing or unsupported.
- **Quality gate connection:** Interpretation Gate.
- **Related template:** `templates/visual-report-template.md`.

## Dashboard Design Brief

- **Minimum done criteria:** Defines users, decisions supported, primary KPIs, metric definitions, data sources, grain, refresh cadence, filters, layout plan, access/privacy needs, success criteria, and owner.
- **Strong done criteria:** Adds selected dashboard archetype from `templates/dashboards/`, component plan, user workflows, drill-down needs, alerts/thresholds, data quality dependencies, unsupported decisions, stakeholder acceptance criteria, and maintenance process.
- **Blocking gaps:** Dashboard built before decisions/users are defined; no metric definitions; grain unclear; no refresh/freshness plan; no owner.
- **Quality gate connection:** Interpretation Gate for communication dashboards; Production or Monitoring Gate for operational dashboards.
- **Related template:** `templates/dashboard-design-brief-template.md`.

## Dashboard QA Checklist

- **Minimum done criteria:** Verifies data freshness, metric definitions, filters, aggregation/grain, totals/subtotals, date ranges, cross-visual consistency, permissions/privacy, performance, and signoff decision.
- **Strong done criteria:** Adds source reconciliation, user-group permission testing, screen-size review, severity-labeled issues, publish decision, and maintenance cadence confirmation.
- **Blocking gaps:** Primary KPIs cannot be reconciled; users cannot see freshness; filters silently change definitions; unauthorized access; no stakeholder signoff.
- **Quality gate connection:** Interpretation Gate for reporting dashboards; Monitoring Gate for operational monitoring dashboards.
- **Related template:** `templates/dashboard-qa-checklist-template.md`.

## HTML Report

- **Minimum done criteria:** Provides self-contained HTML with title, audience, decision, data freshness, executive summary, KPI cards, chart containers, findings, limitations, recommendations, and print/export guidance.
- **Strong done criteria:** Adds design tokens, responsive layout, print-friendly CSS, accessible semantic sections, readable tables, and report QA notes.
- **Blocking gaps:** Output depends on hidden local assets without explanation; charts have no captions; print/PDF export is unreadable; recommendation or limitations missing.
- **Quality gate connection:** Interpretation Gate.
- **Related template:** `templates/html-report-template.md`.

---

## Completion Rule

Before saying an artifact is complete, check:

1. Minimum done criteria are met.
2. No blocking gaps remain.
3. The relevant gate can pass or the remaining limitation is explicitly documented.
4. The next correct action is named.
