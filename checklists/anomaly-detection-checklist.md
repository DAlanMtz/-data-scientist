# Anomaly Detection Checklist

Use for anomaly, fraud, defect, quality, incident, monitoring, or alerting system review.

## Anomaly Definition And Impact

- [ ] Anomaly type is defined: point, contextual, or collective.
- [ ] Business impact is stated.
- [ ] Action after detection is defined.
- [ ] Non-anomalous unusual cases are described.
- [ ] Severity levels are defined if needed.
- [ ] Investigation capacity is known.

## Data And Labels

- [ ] Entity and event grain are defined.
- [ ] Timestamp and context fields are available.
- [ ] Historical normal period is identified.
- [ ] Known incident labels are inventoried if available.
- [ ] Label incompleteness is acknowledged.
- [ ] Known anomaly periods are excluded from normal training when appropriate.
- [ ] Seasonality and peer groups are understood.

## Baselines And Methods

- [ ] Rule-based baseline is included.
- [ ] Robust z-score or IQR method is considered.
- [ ] Rolling baseline or control chart is considered for time series.
- [ ] Isolation forest is considered for multivariate tabular anomalies.
- [ ] DBSCAN/density methods are considered when density structure matters.
- [ ] Reconstruction-error methods are justified by data complexity.
- [ ] Method provides or can be paired with reason codes.

## Thresholds And Alert Quality

- [ ] Threshold is tied to capacity, severity, or known incidents.
- [ ] Expected alert volume is estimated.
- [ ] False-positive cost is understood.
- [ ] False-negative cost is understood.
- [ ] Tiered thresholds are considered.
- [ ] Duplicate alert grouping is defined.
- [ ] Suppression rules for known benign patterns are documented.

## Validation

- [ ] Time-aware validation or backtesting is used.
- [ ] Known incidents are replayed where possible.
- [ ] Precision@k or alert yield is measured.
- [ ] Recall is measured where labels are credible.
- [ ] Time-to-detect is measured where timing matters.
- [ ] Performance is reviewed by segment/source/entity type.
- [ ] False-positive examples are inspected.

## Investigation Workflow

- [ ] Alert includes entity, timestamp, score/rule, and reason codes.
- [ ] Alert includes peer or historical comparison.
- [ ] Reviewer disposition is captured.
- [ ] Escalation process is defined.
- [ ] Human review is required before high-impact accusations or actions.
- [ ] Reviewer feedback feeds threshold and model review.

## Monitoring And Drift

- [ ] Alert volume is monitored.
- [ ] Alert precision/review yield is monitored.
- [ ] Feature drift is monitored.
- [ ] Seasonality and normal behavior shifts are monitored.
- [ ] False-positive themes are tracked.
- [ ] Alert fatigue is monitored.
- [ ] Owner and response SLA are defined.

## Minimum Acceptable Standard

- [ ] Anomaly definition, action, baseline, threshold, alert volume estimate, validation approach, and investigation workflow exist.

## Strong Practice

- [ ] Alerts are grouped, reason-coded, and linked to reviewer outcomes.
- [ ] Known incidents are replayed in backtests.
- [ ] Monitoring includes drift, alert quality, and analyst workload.

## Red Flags

- [ ] "Anomaly" means anything unusual with no action.
- [ ] Threshold is chosen only to maximize statistical rarity.
- [ ] Alert volume exceeds review capacity.
- [ ] Seasonality or business events are flagged as incidents.
- [ ] Anomaly score is treated as proof of fraud or wrongdoing.
- [ ] No human review for consequential actions.

