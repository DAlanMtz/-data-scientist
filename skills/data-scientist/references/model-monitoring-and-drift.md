# Model Monitoring And Drift

Use this guide after a model, scoring rule, forecast, recommender, anomaly detector, or dashboard metric is operational.

## Monitoring Layers

Monitor at four levels:

- Pipeline health: did the job run and deliver outputs?
- Data quality: did inputs match contract?
- Model behavior: did features, scores, calibration, or decisions shift?
- Business impact: did downstream outcomes improve or degrade?

Do not rely on one dashboard tile. Production issues usually appear first in volume, freshness, or distribution changes.

## Data Drift

Data drift means input feature distributions changed.

Monitor:

- Numeric distributions: mean, median, quantiles, missingness, range, PSI, KS-style comparisons.
- Category distributions: new categories, missing categories, frequency shifts.
- Text: language mix, document length, embedding distribution, topic mix.
- Time series: volume, seasonality, level shifts, missing periods.

Action:

- First check source changes, schema changes, unit changes, and population changes.
- Retrain only after understanding whether drift reflects real business change or data defect.

## Concept Drift

Concept drift means the relationship between inputs and outcome changed.

Signals:

- Performance drops while data quality is stable.
- Same score bands now have different outcome rates.
- Feature importance or error slices change materially.
- Business policy, product, competitor, or user behavior changed.

Action:

- Compare recent labeled data to historical validation.
- Review error examples.
- Consider retraining, feature changes, or target redefinition.

## Prediction Drift

Prediction drift means model outputs changed.

Monitor:

- Score distribution.
- Share above threshold.
- Average predicted probability or value.
- Forecast level by horizon.
- Recommendation exposure distribution.
- Alert volume for anomaly detection.

Prediction drift may be desirable if the population changed. Investigate before treating it as failure.

## Label Drift

Label drift means target rate or target definition changed.

Monitor:

- Outcome rate by time and segment.
- Label availability delay.
- Label missingness.
- Label source changes.
- Policy changes affecting labels.

If labels arrive late, separate true performance changes from incomplete labels.

## Performance Decay

Monitor when outcomes become available:

- Regression: MAE, RMSE, bias, interval coverage.
- Classification: precision, recall, PR AUC, ROC AUC, calibration, lift, confusion matrix.
- Forecasting: error by horizon, bias, coverage.
- Recommendation: online conversion, retention, CTR, revenue, diversity, guardrails.
- Anomaly detection: alert precision, incident recall, alert volume, time-to-detect.

Compare to:

- Launch validation.
- Recent rolling baseline.
- Current business process.
- Champion model.

## Monitoring Metrics

Minimum production panel:

- Last successful run.
- Input row count.
- Scored row count.
- Missingness of critical features.
- New/unseen categories.
- Score distribution.
- Threshold action count.
- Performance on available labels.
- Business KPI and guardrails.
- Error rate and latency.

For dashboards, show data freshness and model version.

## Population Stability

Use population stability checks when scoring populations may change.

Track:

- Population size.
- Segment mix.
- Acquisition channel mix.
- Geography/product/plan mix.
- Entity tenure mix.
- Eligibility criteria changes.

If the scored population no longer resembles validation, performance claims may not hold.

## Feature Distribution Changes

For each important feature:

- Compare recent production distribution to training and validation.
- Monitor missingness and default usage.
- Check top categories.
- Check range and quantiles.
- Track source-specific differences.

Prioritize features with high importance, high business sensitivity, or known quality issues.

## Calibration Drift

Monitor when scores are probabilities or expected values.

Checks:

- Reliability curve by recent period.
- Observed rate by score band.
- Calibration-in-the-large.
- Brier score.
- Log loss.
- Group-level calibration.

If calibration drifts but ranking remains good, recalibration may be enough. If ranking also decays, retraining or redesign may be needed.

## Retraining Triggers

Possible triggers:

- Performance below agreed threshold.
- Calibration outside tolerance.
- Major feature drift plus performance risk.
- Business process or product change.
- New data source or label definition.
- Scheduled refresh after enough new labels.
- Regulatory or policy change.

Retraining process:

1. Diagnose issue.
2. Create candidate model.
3. Compare to incumbent on recent and historical validation.
4. Review responsible AI and operational metrics.
5. Approve rollout or keep incumbent.

## Alerting

Alerts should be actionable.

For each alert define:

- Condition.
- Severity.
- Owner.
- Expected response time.
- Diagnostic links.
- Fallback or rollback action.

Avoid alert floods. Use grouping, severity levels, and suppression windows.

## Post-Deployment Evaluation

Evaluate:

- Did users act on model outputs?
- Did action rates change?
- Did business KPI improve?
- Did error burden shift?
- Are there unexpected side effects?
- Are users overriding the model?
- Are outcomes being logged for future learning?

Offline validation does not prove operational impact. Measure after launch.

## Shadow Testing

Use shadow mode before full launch when risk is meaningful.

Pattern:

- Run model on live data without affecting decisions.
- Log scores and would-have-actions.
- Compare to current process.
- Evaluate labels once available.
- Review operational volumes and edge cases.

Shadow testing catches data availability and scoring issues that offline validation misses.

## Champion And Challenger

Champion: current production model or process.

Challenger: candidate replacement or alternative.

Compare:

- Same production population.
- Same time windows.
- Same outcome definitions.
- Performance and calibration.
- Business KPIs.
- Fairness and guardrails.
- Operational cost and latency.

Promote the challenger only when improvement is meaningful and risks are addressed.

## When Labels Are Delayed Or Unavailable

Monitor proxies carefully:

- Data and feature drift.
- Prediction drift.
- Score/action volume.
- Calibration on partial labels, with delay adjustment.
- Human review yield.
- Business leading indicators.
- Known incident recall.
- Sampled manual audits.

Do not claim performance improvement from unlabeled proxy metrics alone. Use them as early warning until outcomes arrive.

