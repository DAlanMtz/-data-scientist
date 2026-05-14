# Model Audit Checklist

Use as the main senior review checklist for an existing project, notebook, model, report, dashboard, or production scoring process.

## Problem Framing

- [ ] Business decision is clear.
- [ ] Intended use and user are documented.
- [ ] Non-intended use is documented.
- [ ] Population and time window are defined.
- [ ] Cost of errors is understood.
- [ ] Success metric matches decision.
- [ ] Current process or baseline is identified.

## Data Quality

- [ ] Source inventory is complete.
- [ ] Dataset grain is correct.
- [ ] Primary keys and joins are validated.
- [ ] Missingness is measured and interpreted.
- [ ] Duplicates are measured and resolved or justified.
- [ ] Outliers are reviewed.
- [ ] Data types and units are correct.
- [ ] Freshness and coverage are adequate.
- [ ] Data contract or quality checks exist for recurring use.

## Target Definition

- [ ] Target is decision-relevant.
- [ ] Target timing is clear.
- [ ] Outcome window is defined.
- [ ] Label source and delay are known.
- [ ] Ambiguous or excluded cases are handled.
- [ ] Target rate/distribution is plausible.
- [ ] Target is not a future status masquerading as a prediction target.

## Leakage

- [ ] Feature availability at prediction time is verified.
- [ ] Outcome-derived fields are excluded or justified.
- [ ] Aggregations are cutoff-safe.
- [ ] Entity leakage is checked.
- [ ] Duplicate leakage is checked.
- [ ] Text/document leakage is checked where relevant.
- [ ] Preprocessing leakage is prevented.
- [ ] Evaluation leakage from repeated test-set tuning is assessed.

## Preprocessing And Features

- [ ] Imputation, encoding, scaling, and selection are fit inside training/folds.
- [ ] Feature definitions are reproducible.
- [ ] Rare/unseen category handling is defined.
- [ ] Feature transformations are documented.
- [ ] Feature selection method is leakage-safe.
- [ ] Production availability is reviewed.
- [ ] Sensitive/proxy features are flagged.

## Splitting And Validation

- [ ] Split strategy matches deployment.
- [ ] Time-aware split is used when predicting the future.
- [ ] Group-aware split is used when entities repeat.
- [ ] Cross-validation is appropriate.
- [ ] Final holdout is preserved.
- [ ] Split row counts and target rates are reported.
- [ ] Validation variance or stability is considered.

## Baselines And Model Comparison

- [ ] Naive/current-process baseline is included.
- [ ] Simple interpretable baseline is included where appropriate.
- [ ] Candidate models use same data, split, and metrics.
- [ ] Hyperparameter tuning is documented.
- [ ] Complexity is justified by meaningful lift.
- [ ] Runtime and maintenance cost are considered.

## Metrics

- [ ] Primary metric matches business objective.
- [ ] Secondary metrics expose tradeoffs.
- [ ] Classification threshold metrics are reported when actions are thresholded.
- [ ] Regression metrics are in business units.
- [ ] Forecast metrics are horizon-specific.
- [ ] Ranking metrics use actual `k`.
- [ ] Calibration metrics are included when probabilities drive decisions.

## Diagnostics And Error Analysis

- [ ] Residuals, confusion matrix, calibration, lift, or equivalent diagnostics are reviewed.
- [ ] Error slices by time, segment, source, and subgroup are reviewed.
- [ ] Worst errors or confident wrong cases are inspected.
- [ ] Performance is compared across validation windows.
- [ ] Failure modes lead to concrete recommendations.

## Interpretability

- [ ] Explanation method is appropriate for model and audience.
- [ ] Feature importance is not presented as causality.
- [ ] Top drivers are checked for leakage and proxy risk.
- [ ] Local explanations or reason codes exist if operators need them.
- [ ] Limitations of interpretation are documented.

## Responsible AI

- [ ] Affected stakeholders are identified.
- [ ] Sensitive and proxy variables are reviewed.
- [ ] Subgroup performance is checked where possible and appropriate.
- [ ] Privacy and consent constraints are reviewed.
- [ ] Human oversight exists for high-impact decisions.
- [ ] Misuse and non-intended use are documented.
- [ ] Escalation is recommended for high-risk domains.

## Business Decision Fit

- [ ] Model output maps to a real action.
- [ ] Threshold, ranking, or policy is specified.
- [ ] Capacity and cost constraints are included.
- [ ] Expected business impact is estimated.
- [ ] Measurement plan exists for post-deployment impact.
- [ ] A simpler rule/dashboard/process fix is considered if sufficient.

## Documentation And Reproducibility

- [ ] Code can be rerun.
- [ ] Data version is recorded.
- [ ] Environment/dependencies are documented.
- [ ] Feature set and model parameters are recorded.
- [ ] Experiment log or decision record exists.
- [ ] Model card or report exists for production-facing work.
- [ ] Results in report match executed code.

## Production Readiness

- [ ] Input/output schemas are defined.
- [ ] Preprocessing and model artifact are versioned together.
- [ ] Batch/API scoring path is defined.
- [ ] Logging is defined.
- [ ] Monitoring is defined.
- [ ] Retraining and rollback are defined.
- [ ] Owner and incident response are defined.

## Minimum Acceptable Standard

- [ ] No material leakage.
- [ ] Validation matches use case.
- [ ] Baseline comparison exists.
- [ ] Metrics match business decision.
- [ ] Error analysis and limitations are documented.
- [ ] Deployment is not recommended without production readiness and responsible-use review.

## Strong Practice

- [ ] Audit includes severity-ranked findings.
- [ ] Recommendations separate must-fix validity issues from improvements.
- [ ] Business owner can explain how the model will be used.
- [ ] Monitoring and decision impact measurement are ready before launch.

## Red Flags

- [ ] High performance with no leakage review.
- [ ] Random split for temporal or repeated-entity data.
- [ ] No baseline.
- [ ] Metrics reported without threshold or cost context.
- [ ] Notebook cannot be rerun.
- [ ] Model output does not connect to a decision.
- [ ] High-impact model lacks fairness/privacy/human-review assessment.

