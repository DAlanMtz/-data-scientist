# Supervised Learning Checklist

Use for classification and regression model review before trusting results or preparing deployment.

## Target And Data

- [ ] Target definition is correct and decision-relevant.
- [ ] Target timing and outcome window are documented.
- [ ] Labels are available only after the prediction point.
- [ ] Label noise, ambiguity, and delay are assessed.
- [ ] Unit of analysis is consistent across features and target.
- [ ] Training population matches intended scoring population.

## Splitting And Validation

- [ ] Train/test split is documented.
- [ ] Random split is used only when observations are independent.
- [ ] Time-aware split is used for future-facing prediction.
- [ ] Group-aware split is used for repeated customers/accounts/devices/sessions/documents.
- [ ] Validation design matches deployment scenario.
- [ ] Final holdout is not used for tuning.
- [ ] Cross-validation keeps preprocessing inside folds.
- [ ] Nested CV is considered when tuning is extensive.

## Feature Preprocessing

- [ ] Imputation is fit only on training data or inside folds.
- [ ] Encoding is fit only on training data or inside folds.
- [ ] Scaling is fit only on training data or inside folds.
- [ ] Target encoding uses fold-safe smoothing.
- [ ] Rare/unseen categories have defined behavior.
- [ ] Text, embeddings, PCA, or feature selection are fit leakage-safely.
- [ ] Resampling for imbalance is done only inside training folds.
- [ ] Feature definitions are available at prediction time.
- [ ] If classical variable selection was used (backward elimination, forward selection, stepwise), the entire selection process is nested inside validation folds — not run on the full dataset.
- [ ] If selecting features data-driven, the selection method (regularization, RFE, importance-based) is applied inside training only, not fit on the validation or test set.

## Baselines And Candidate Models

- [ ] Naive/current-process baseline is included.
- [ ] Simple interpretable model is included where appropriate.
- [ ] Candidate models are compared on the same split and metric.
- [ ] Hyperparameter tuning search space is documented.
- [ ] Model complexity is justified by validated lift.
- [ ] Runtime, maintainability, and deployment constraints are considered.

## Metrics

- [ ] Primary metric matches business objective.
- [ ] Secondary metrics expose tradeoffs.
- [ ] Metric uncertainty or fold variability is reported where possible.
- [ ] Segment/subgroup metrics are reviewed.
- [ ] Results are compared to baseline, not just absolute scores.

## Classification Notes

- [ ] Class balance is measured overall and by split.
- [ ] Confusion matrix is shown at selected threshold.
- [ ] Precision, recall, and F1 are reported when thresholded actions exist.
- [ ] ROC-AUC is not used alone for rare events.
- [ ] PR-AUC, lift, or precision@k is used for imbalanced or capacity-limited use cases.
- [ ] Calibration is checked if probabilities are used.
- [ ] Threshold selection is based on cost, capacity, or required precision/recall.
- [ ] Threshold is not chosen on the final test set.

## Regression Notes

- [ ] Target units and valid range are clear.
- [ ] MAE and RMSE are interpreted in business units.
- [ ] R-squared is not the sole success metric.
- [ ] MAPE is avoided when actuals can be zero or near zero.
- [ ] Residual diagnostics are reviewed.
- [ ] Bias by segment and prediction range is checked.
- [ ] Outlier and influential point impact is assessed.
- [ ] Prediction intervals are considered when uncertainty matters.

## Error Analysis

- [ ] Worst errors or most confident wrong predictions are inspected.
- [ ] Errors are sliced by time, source, segment, and subgroup.
- [ ] Missingness and outlier patterns in errors are reviewed.
- [ ] Failure modes lead to concrete fixes or caveats.
- [ ] Error cost is translated into business impact.

## Interpretability

- [ ] Feature importance or coefficients are reviewed for leakage and proxy risk.
- [ ] Explanations are validated against domain knowledge.
- [ ] Predictive associations are not described as causal effects.
- [ ] Local explanations or reason codes are available if users need them.

## Deployment Readiness

- [ ] Scoring inputs and output schema are defined.
- [ ] Preprocessing and model artifact are versioned together.
- [ ] Feature refresh path is reliable.
- [ ] Monitoring metrics are defined.
- [ ] Retraining and rollback triggers are documented.
- [ ] Human review or override exists for high-impact decisions.

## Minimum Acceptable Standard

- [ ] Valid target, leakage-safe split, baseline comparison, appropriate metric, and error analysis exist.
- [ ] Final performance claim uses an untouched holdout or defensible validation design.

## Strong Practice

- [ ] Calibration, subgroup performance, and threshold/cost analysis are included.
- [ ] Experiment log records data, split, feature set, model, parameters, and decision.
- [ ] Production requirements are reviewed before selecting the final model.

## Red Flags

- [ ] Full dataset preprocessing before splitting.
- [ ] Random split despite time or entity dependence.
- [ ] Accuracy headline for rare-event classification.
- [ ] Test set used repeatedly for tuning.
- [ ] Model wins only by tiny unstable metric gains.
- [ ] Deployment is proposed with no monitoring or owner.
- [ ] Variable selection run on full dataset before splitting, then test-set performance reported as unbiased.

