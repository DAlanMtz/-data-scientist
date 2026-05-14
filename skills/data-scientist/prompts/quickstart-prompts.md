# Quickstart Prompts

Copy these prompts into an agent session to activate the `data-scientist` skill with stage, gate, artifact, and next-action discipline.

## Audit An Existing Notebook

```text
Use the data-scientist skill to audit this notebook. Identify the active stage, the relevant quality gate, and the right audit artifact. Review framing, data quality, target definition, leakage, preprocessing, validation, baselines, metrics, diagnostics, error analysis, responsible AI, reproducibility, and production readiness. Use severity levels for findings and end with the next correct action.
```

## Audit A Dataset

```text
Use the data-scientist skill to audit this dataset. Identify the active stage and Data Readiness Gate. Produce a Data Audit Report covering schema, grain, row counts, freshness, missingness, duplicates, valid ranges, referential integrity, leakage candidates, and whether the data is sufficient for the stated decision. Use severity levels and end with the next correct action.
```

## Create A Modeling Plan

```text
Use the data-scientist skill to create a Modeling Plan. First identify the active stage and quality gate. Define the target, grain, prediction point, available features, leakage risks, validation strategy, baseline, candidate models, metrics, error analysis plan, expected artifacts, and next correct action.
```

## Design A Validation Strategy

```text
Use the data-scientist skill to design a Validation Plan. Identify the active stage and Validation Gate. Recommend the split strategy, cross-validation or backtesting approach, group/time leakage controls, preprocessing placement, final holdout policy, baseline, metrics, calibration checks, and next correct action.
```

## Check Leakage Risk

```text
Use the data-scientist skill to check leakage risk. Identify the active stage and relevant gate. For each feature or field, assess prediction-time availability, target-derived information, post-outcome updates, duplicate/entity leakage, preprocessing leakage, and evaluation leakage. Produce severity-ranked findings and end with the next correct action.
```

## Compare Candidate Models

```text
Use the data-scientist skill to compare these candidate models. Identify the active stage and Model Comparison Gate. Produce a Model Comparison Report that includes baseline comparison, validation design, primary and secondary metrics, stability, calibration if probabilities are used, error analysis, interpretability, deployment cost, and the next correct action.
```

## Run Error Analysis

```text
Use the data-scientist skill to run error analysis. Identify the active stage and Diagnostics Gate. Produce an Error Analysis Report covering worst errors, false positives/false negatives or residuals, errors by time/segment/source/subgroup, missingness and outlier patterns, business impact, severity-ranked findings, and next correct action.
```

## Review Calibration And Thresholds

```text
Use the data-scientist skill to review calibration and thresholds. Identify the active stage and Calibration/Decision Gate. Produce a Calibration Report and threshold recommendation covering score bands, calibration curve, Brier/log loss where relevant, confusion matrix, precision/recall tradeoffs, cost/capacity constraints, business policy, and next correct action.
```

## Create A Decision Memo

```text
Use the data-scientist skill to create a Decision Memo. Identify the active stage and relevant quality gate. State the decision, recommendation, options considered, evidence, expected impact, uncertainty, risks, limitations, monitoring plan, owner, and next correct action.
```

## Create A Stakeholder Report

```text
Use the data-scientist skill to create a stakeholder report. Identify the active stage and Interpretation Gate. Produce the right artifact with executive summary, business question, data used, method, key findings, visuals with captions, interpretation, limitations, recommendation, next steps, and next correct action.
```

## Review Production Readiness

```text
Use the data-scientist skill to review production readiness. Identify the active stage and Production Gate. Produce a Deployment Readiness Report covering reproducibility, environment, config, data validation, feature consistency, model artifacts, batch/API inference, logging, monitoring, alerting, retraining, rollback, security/privacy, ownership, incident response, severity-ranked gaps, and next correct action.
```

## Create A Monitoring Plan

```text
Use the data-scientist skill to create a Monitoring Plan. Identify the active stage and Monitoring Gate. Define data quality, feature drift, prediction drift, label/performance monitoring, calibration, business KPIs, delayed-label handling, alert thresholds, owners, retraining triggers, champion/challenger process, and next correct action.
```

## Review A Dashboard Or Visualization

```text
Use the data-scientist skill to review this dashboard or visualization. Identify the active stage and relevant quality gate. Check data freshness, metric definitions, denominators, filters, chart choice, uncertainty, visual accessibility, misleading chart risks, unsupported conclusions, severity-ranked findings, and next correct action.
```

## Explain A Method Choice

```text
Use the data-scientist skill to explain the right method choice. Identify the active stage and quality gate. Compare candidate methods against target type, data shape, validation design, metrics, interpretability, deployment constraints, responsible-use risks, and next correct action.
```

## Convert Exploratory Notebook Work Into A Production-Ready Plan

```text
Use the data-scientist skill to convert this exploratory notebook into a production-ready plan. Identify the current stage and Production Gate. Produce an artifact plan covering modular pipeline steps, data contracts, feature generation, training/evaluation, model artifact storage, batch/API inference, logging, monitoring, tests, documentation, rollback, retraining, owners, and next correct action.
```

