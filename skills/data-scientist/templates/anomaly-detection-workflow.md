# Anomaly Detection Workflow

Use this workflow to identify unusual records, events, users, transactions, time periods, system states, or patterns that need investigation.

## Required Inputs

- Definition of anomaly and why it matters.
- Entity and event grain.
- Historical normal behavior.
- Known incident or anomaly labels if available.
- Investigation capacity and false-positive tolerance.
- Severity or business value rules.

## Expected Outputs

- Baseline anomaly rules.
- Candidate anomaly detection method.
- Alert threshold and expected alert volume.
- Investigation workflow and reason codes.
- False-positive management plan.
- Monitoring and alerting design.

## Step-By-Step Workflow

### 1. Define Anomaly

Specify:

- Point anomaly: one unusual record.
- Contextual anomaly: unusual given time, peer group, location, or entity.
- Collective anomaly: unusual sequence or group pattern.
- Severity and action needed.
- What is not an anomaly.

Without a useful anomaly definition, the system becomes noise generation.

### 2. Prepare Data

Check:

- Entity identifiers.
- Timestamps.
- Feature availability.
- Missingness and outliers.
- Known incident periods.
- Seasonality and peer groups.
- Label quality if labels exist.

Do not train "normal" behavior on known incident periods when avoidable.

### 3. Build Rule-Based Baselines

Start with:

- Business thresholds.
- Robust z-scores.
- IQR rules.
- Control limits.
- Rolling baseline deviations.
- Known fraud/defect/system rules.

Rules provide interpretability and a comparison point.

### 4. Candidate Methods

Use:

- Robust z-scores/IQR for simple numeric deviations.
- Isolation forest for multivariate anomaly scores.
- DBSCAN/HDBSCAN or density methods for unusual clusters/noise.
- One-class SVM when data size and feature scale are manageable.
- Time-series anomaly detection for seasonal/temporal deviations.
- Reconstruction-error approaches, such as autoencoders, when high-dimensional patterns justify complexity.

Choose methods that produce usable reasons or can be paired with reason-code logic.

### 5. Time-Series Anomalies

For time-indexed data:

- Model trend and seasonality.
- Compare actuals to expected range.
- Use rolling baselines.
- Detect spikes, drops, level shifts, and change points.
- Adjust for holidays, promotions, outages, and known events.

Alert on practical deviation, not every statistically unusual blip.

### 6. Threshold Setting

Set thresholds using:

- Historical known incidents.
- Analyst capacity.
- False-positive tolerance.
- Severity or value weighting.
- Alert volume targets.
- Review precision.

Use tiered thresholds when severity differs: monitor, review, urgent.

### 7. False-Positive Management

Reduce noise by:

- Grouping duplicate alerts.
- Suppressing repeated known benign patterns.
- Adding peer-group context.
- Requiring persistence across time.
- Adding minimum severity or value thresholds.
- Reviewing false-positive themes regularly.

An alert system that overwhelms users will be ignored.

### 8. Investigation Workflow

Each alert should include:

- Entity/event ID.
- Timestamp.
- Anomaly score or rule.
- Reason codes.
- Feature deviations.
- Peer or historical comparison.
- Recommended next action.
- Link to supporting records.
- Disposition field for reviewer outcome.

Reviewer feedback should feed evaluation and threshold updates.

### 9. Monitoring And Alerting

Monitor:

- Alert volume.
- Alert precision from reviewed cases.
- Known incident recall.
- Time-to-detect.
- False-positive themes.
- Feature drift.
- Seasonality changes.
- Reviewer workload.

Set ownership and response expectations for each alert severity.

## Validation And Evaluation Guidance

- If labels exist: precision@k, recall, PR-AUC, false-positive rate.
- If labels are incomplete: manual review yield, known incident replay, alert volume, and time-to-detect.
- Backtest historical incidents.
- Compare to rule baseline.
- Evaluate by segment and source.

## Interpretation Guidance

- Anomaly score means unusualness, not guilt or confirmed failure.
- Provide reason codes and peer comparisons.
- State whether anomaly is point, contextual, or collective.
- Separate detection from investigation outcome.

## Common Failure Modes

- No clear action after alert.
- Too many false positives.
- Seasonality treated as anomaly.
- Normal training data includes incidents.
- Threshold chosen without capacity.
- Method produces no reason codes.
- Alert duplicates flood reviewers.
- Model drift mistaken for incident spike.

## Responsible-Use Notes

- Use human review for fraud, abuse, employee, customer, or safety allegations.
- Avoid treating anomaly flags as proof.
- Monitor disproportionate alerting across sensitive or vulnerable groups.
- Protect privacy in investigation records.

## Tool-Flexible Notes

- Python/R: build robust statistics, isolation forests, density models, and backtests.
- SQL: implement rule baselines, rolling windows, alert tables, and reviewer dispositions.
- Excel/Sheets: useful for investigator review queues and threshold scenario analysis.
- Notebooks: compare methods with examples.
- Production pipelines: version rules/model, log alert outcomes, monitor alert volume, and define escalation paths.

