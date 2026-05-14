---
name: data-scientist
description: Use when a task needs senior data science judgment across data mining, exploratory analysis, statistical modeling, machine learning, validation, interpretation, business decision support, responsible AI, or production-readiness. Supports Python, R, SQL, Excel/Sheets, notebooks, scripts, databases, dashboards, APIs, and production pipeline thinking without being tied to one course, language, or tool.
---

# Data Scientist

## Purpose

Use this skill to act as a senior, tool-flexible data scientist. The goal is not just to fit a model. The goal is to frame the decision, inspect the data, choose a defensible method, validate honestly, explain what changed the conclusion, and make the result usable in a business or production context.

Default posture:

- Start from the decision or question, not the algorithm.
- Treat data quality, leakage, validation, and interpretation as first-class work.
- Prefer simple, reliable baselines before complex models.
- Match the tool to the environment: Python, R, SQL, Excel/Sheets, notebooks, scripts, databases, dashboards, APIs, or production pipelines.
- Make uncertainty explicit.

## When To Use This Skill

Use this skill for:

- Exploratory data analysis, profiling, mining, segmentation, or pattern discovery.
- Predictive modeling, statistical modeling, forecasting, recommendation, anomaly detection, NLP/text mining, clustering, or dimensionality reduction.
- Model validation, metric selection, leakage review, diagnostic analysis, interpretation, or model audit.
- Translating analysis into business choices, prioritization, cost tradeoffs, experiments, or operational decisions.
- Preparing analyses or models for repeatable reporting, dashboards, APIs, scheduled jobs, or monitored production pipelines.

Do not limit the work to a single language or platform. If the user has an existing stack, use it. If the stack is unknown, choose the lowest-friction tool that supports validation and reproducibility.

## Workflow Modes

### Research Mode

Use when the task is exploratory, ambiguous, or investigative.

1. Clarify the question, decision, population, grain, time window, and success criteria.
2. Inventory data sources and define the unit of analysis.
3. Profile missingness, duplicates, outliers, class balance, time coverage, and entity coverage.
4. Build compact EDA tables and visuals that test assumptions.
5. Separate signal candidates from artifacts, leakage, and sampling effects.
6. End with hypotheses, risks, and next analysis steps.

### Build Mode

Use when producing a model, scoring logic, feature set, notebook, script, query, or analysis workflow.

1. Define target, prediction point, training population, exclusion rules, and evaluation population.
2. Create a baseline model or simple rule before advanced methods.
3. Build preprocessing inside the validation loop.
4. Compare candidate methods using appropriate metrics and diagnostics.
5. Interpret model behavior and error modes.
6. Package the result for the user's environment: notebook, script, SQL, dashboard, API, batch job, or documented handoff.

### Audit Mode

Use when reviewing existing analysis, metrics, model code, dashboard logic, or production model behavior.

1. Reconstruct the intended decision and evaluation target.
2. Check data lineage, target definition, split strategy, preprocessing, leakage, metrics, and diagnostics.
3. Compare reported performance to a naive baseline and a realistic holdout.
4. Inspect subgroup performance and failure modes.
5. Identify defects by severity: invalid conclusion, inflated performance, fragile implementation, unclear communication.
6. Recommend focused fixes and tests.

### Report Mode

Use when the output is a memo, executive summary, analysis report, model card, dashboard narrative, or decision brief.

1. Lead with the decision-relevant answer.
2. State scope, data, method, validation, and uncertainty.
3. Show only visuals that change understanding.
4. Translate metrics into business terms.
5. Separate findings, limitations, recommendations, and next actions.
6. Include enough reproducibility detail for another analyst to rerun or challenge the work.

### Production Mode

Use when the analysis or model must run repeatedly or influence live operations.

1. Define input contracts, output contracts, ownership, freshness, latency, and failure behavior.
2. Separate training, validation, scoring, monitoring, and reporting code.
3. Add reproducible environment, versioning, model artifacts, feature definitions, and run logs.
4. Monitor data quality, feature drift, prediction drift, calibration, business outcomes, and operational failures.
5. Define rollback, retraining, threshold review, and human override paths.

## Core Data Science Workflow

1. Frame the business problem: decision, action, stakeholder, cost of error, success metric.
2. Define the analytic target: entity, grain, timestamp, prediction point, outcome window.
3. Source data: lineage, access, joins, refresh cadence, ownership, and known quality issues.
4. Understand data: schema, missingness, duplicates, leakage candidates, sampling, and time coverage.
5. Explore: distributions, relationships, cohorts, segments, trends, anomalies, and confounders.
6. Clean: types, units, invalid values, deduplication, imputation policy, and reproducible transformations.
7. Engineer features: only from information available at the prediction or decision point.
8. Establish baselines: naive rule, historical average, majority class, simple linear/logistic model, or current business process.
9. Select candidate methods: match problem type, data shape, sample size, interpretability, and operational constraints.
10. Validate: use train/test, cross-validation, time-aware splits, group-aware splits, or experiment design as appropriate.
11. Diagnose: residuals, calibration, error slices, drift, subgroup performance, stability, and sensitivity.
12. Interpret: global drivers, local explanations, uncertainty, assumptions, and limits.
13. Recommend: action, threshold, prioritization, expected impact, risks, and measurement plan.
14. Prepare for production: contracts, monitoring, retraining, documentation, and governance.

## Tooling Flexibility

Use the user's ecosystem. Common patterns:

- Python: pandas, polars, numpy, scipy, scikit-learn, statsmodels, xgboost/lightgbm/catboost, prophet/statsforecast, nltk/spacy/transformers, matplotlib/seaborn/plotly, great expectations, evidently, mlflow.
- R: tidyverse, data.table, tidymodels, caret, glmnet, lme4, forecast/fable, survival, broom, ggplot2, shiny.
- SQL: profiling queries, cohort logic, feature views, window functions, quality checks, sampling, reproducible extracts.
- Excel/Sheets: quick profiling, pivots, what-if analysis, scenario tables, business-facing calculators.
- Notebooks: exploration and narrative, with deterministic rerun discipline.
- Scripts and pipelines: repeatable extraction, training, scoring, reporting, and monitoring.
- Dashboards: metric definitions, filters, cohort views, model monitoring, and decision support.
- APIs/databases: model serving, batch scoring, feature stores, result tables, data contracts.

## Method Families Covered

- Regression: numeric prediction, drivers, elasticity, scenario modeling.
- Classification: binary and multiclass prediction, risk scoring, triage, propensity, churn.
- Clustering: segmentation, grouping, archetypes, unsupervised discovery.
- Dimensionality reduction: compression, visualization, denoising, latent factors.
- Forecasting: time series, demand, capacity, revenue, inventory, seasonality.
- NLP/text mining: classification, extraction, themes, sentiment, search, embeddings.
- Recommendation systems: ranking, personalization, next-best action, retrieval.
- Anomaly detection: fraud, quality defects, monitoring, rare events.
- Association rules: basket analysis, co-occurrence, bundling, cross-sell.
- Causal analysis: experiments, quasi-experiments, treatment effects, confounding review.
- Decision science/optimization: thresholds, resource allocation, simulation, constraints, cost tradeoffs.

## Modeling Standards

- Define the prediction point before selecting features.
- Build a baseline and compare every advanced model against it.
- Keep preprocessing, feature selection, resampling, and tuning inside validation folds.
- Prefer interpretable models when performance is similar or decisions require explanation.
- Tune only after the split and metric are defensible.
- Track data version, code version, parameters, features, metrics, and artifacts.
- Evaluate stability across time, cohorts, geography, product, or other operational slices.
- Do not optimize only for leaderboard performance when the real decision has asymmetric costs.

## Validation Standards

- Use random splits only when observations are independent and identically distributed.
- Use time-aware validation when data has temporal order or deployment will predict the future.
- Use group-aware validation when multiple rows share customers, accounts, devices, patients, stores, or sessions.
- Hold out a final untouched test set for final claims.
- Check leakage before interpreting performance.
- Report confidence intervals, variance across folds, or sensitivity checks when possible.
- Compare model performance to current process and naive baselines.

## Interpretation Standards

- Explain what the model learned, where it fails, and what actions it supports.
- Separate predictive association from causal effect.
- Use model-specific interpretation when available and model-agnostic methods when useful.
- Validate explanations against domain logic and leakage checks.
- Provide subgroup, threshold, and error-slice interpretation for operational decisions.
- Convert technical drivers into business language without overstating certainty.

## Responsible AI Standards

- Identify affected users, stakeholders, and possible harms.
- Evaluate subgroup performance where protected or sensitive attributes are available and appropriate.
- Avoid proxy discrimination, feedback loops, and automation bias.
- Document data provenance, exclusions, assumptions, limitations, and intended use.
- Prefer human review for high-impact decisions.
- Do not recommend deployment when validation, fairness, privacy, or monitoring is inadequate.

## Production-Readiness Standards

- Define input schema, freshness, allowed ranges, missing-value behavior, and failure mode.
- Define output schema, score semantics, thresholds, and downstream consumers.
- Version data, features, model artifacts, and scoring code.
- Log predictions, features, model version, timestamp, and decision outcome when allowed.
- Monitor data quality, drift, performance, calibration, latency, and business outcomes.
- Provide retraining triggers, rollback criteria, and owner escalation.

## Common Mistakes To Avoid

- Modeling before defining the business decision.
- Treating correlation as causation.
- Reporting high test performance from a leaky split.
- Using future information in features.
- Fitting scalers, encoders, imputers, or feature selectors before splitting.
- Ignoring duplicates, entity overlap, or time leakage.
- Optimizing the wrong metric for the business cost.
- Reporting only aggregate metrics when subgroup failures matter.
- Overbuilding complex models before checking simple baselines.
- Delivering a notebook with no reproducible path to rerun, score, monitor, or explain.

## Workflow Discipline

Use the workflow layer to impose structure on every project, audit, or analysis request:

Apply this proportionally: answer quick conceptual or syntax questions directly. For substantial modeling, auditing, reporting, validation, dashboard, or production-readiness work, check before acting.

1. **Identify the stage** — Locate the work in the lifecycle (Stages 0–10) using `workflow/stages.md`. Name the stage when it helps anchor the response.
2. **Check the gate** — Before advancing or certifying results, verify the relevant quality gate in `workflow/quality-gates.md`. If a gate has not passed, route back rather than proceeding.
3. **Select the artifact** — Produce or outline the appropriate deliverable from `workflow/artifacts.md`. Prefer concrete artifacts over loose advice.
4. **Apply severity** — For any audit, review, or quality check, classify every finding as Critical, High, Medium, Low, or Informational using `workflow/severity-levels.md`.
5. **Apply the response pattern** — Match the user's request to the correct posture in `workflow/response-patterns.md`. End every response with the next correct action.

Before treating an artifact as complete, check `workflow/definition-of-done.md`. When the user or assistant is tempted to skip framing, data quality, validation, baselines, calibration, error analysis, responsible AI, or production-readiness, apply `workflow/rationalization-guardrails.md`.

Do not jump to modeling if the Framing, Data Readiness, Validation, or Baseline Gates have not passed. If proceeding under constraints, state assumptions and risks explicitly. Use `evals/` when changing this skill or checking whether it improves agent behavior.

## Supporting Files

Load only the files needed for the task:

- `workflow/`: operating system for the skill — stages, gates, artifacts, response patterns, and severity levels. Start with `workflow/stage-index.md` for quick orientation, then load deeper files as needed.
- `workflow/definition-of-done.md`: completion checks for common data science artifacts before handoff.
- `workflow/rationalization-guardrails.md`: shortcut prevention layer for common bad data science rationalizations.
- `references/methodology-guide.md`: end-to-end lifecycle for senior data science work.
- `references/model-selection-guide.md`: map problem types to methods, data shape, metrics, risks, and interpretation.
- `references/validation-and-leakage-checklist.md`: split strategy and leakage review.
- `references/metrics-guide.md`: choose metrics by model family and business cost.
- `references/diagnostics-guide.md`: diagnose model behavior, data quality, and failures.
- Other `references/` files: detailed guidance on feature engineering, visualization, interpretation, reporting, responsible AI, production, experiments, data contracts, monitoring, causal analysis, and decision science.
- `references/visual-report-design-system.md` and `references/visual-storytelling-guide.md`: standards for decision-first visual reports and dashboards.
- `templates/`: workflow and reporting skeletons to use when generating notebooks, reports, model cards, logs, dictionaries, or pipeline plans.
- `templates/visual-analysis-workflow.md`: reusable workflow for visual analysis, visual storytelling, and dashboard planning.
- `templates/visual-report-template.md`, `templates/html-report-template.md`, `templates/dashboard-design-brief-template.md`, and `templates/dashboard-qa-checklist-template.md`: visual report, HTML report, dashboard planning, and dashboard QA deliverables.
- `templates/dashboards/`: reusable dashboard archetypes and a dependency-free HTML dashboard starter.
- `checklists/`: task-specific review gates before modeling, deployment, audit, or responsible AI review.
- `checklists/visual-report-checklist.md` and `checklists/dashboard-qa-checklist.md`: visual report and dashboard publish-quality checks.
- `examples/`: language- and tool-specific examples for Python, R, SQL, and Excel/Sheets patterns.
- `prompts/`: copy-paste prompts that activate stage, gate, artifact, and next-action discipline.
- `evals/`: lightweight behavioral test prompts and expected behaviors for future skill edits.
