# Model Performance Dashboard Template

Use this for monitoring model quality, data drift, calibration, thresholds, and operational health after a model influences decisions.

## Model / Version Metadata

- Model name:
- Model version:
- Deployment environment:
- Training data window:
- Scoring population:
- Owner:
- Last retrained:

## Data Freshness

- Latest prediction timestamp:
- Latest label timestamp:
- Label delay:
- Expected refresh:
- Stale-data threshold:

## Prediction Volume

- Predictions by time:
- Prediction volume by segment:
- Score distribution:
- Decision/action distribution:

Recommended visuals: KPI cards, line chart, histogram, stacked bar.

## Performance Metrics

Only show when labels are available.

| Metric | Current | Baseline/target | Prior period | Status |
| --- | ---: | ---: | ---: | --- |
| `[AUC/F1/MAE/RMSE/etc.]` | `[value]` | `[target]` | `[prior]` | `[status]` |

Separate classification, regression, ranking, and forecasting metrics as appropriate.

## Calibration

- Calibration curve:
- Brier score or calibration error:
- Score-band observed rates:
- Calibration by segment:
- Probability-use warning if not calibrated:

## Threshold Outcomes

- Current threshold:
- Volume above threshold:
- False positives/false negatives where labels available:
- Capacity constraint:
- Threshold review trigger:

Recommended visuals: threshold tradeoff chart, confusion matrix panel, score distribution.

## Segment-Level Performance

Segments to monitor:

- Time period:
- Geography/region:
- Product/channel:
- Protected or sensitive groups where appropriate and lawful:
- Operational owner:

Show sample sizes and avoid overinterpreting tiny segments.

## Drift Indicators

- Feature distribution drift:
- Prediction drift:
- Label/outcome drift:
- Population stability:
- Data quality drift:

Recommended visuals: drift KPI, PSI/KS table, distribution comparison, ranked drift features.

## Error Analysis

- Top false positives / high residuals:
- Top false negatives / underpredictions:
- Error by segment:
- Error reason categories:
- Data quality linkage:

## Alert Rules

| Alert | Threshold | Severity | Owner | Action |
| --- | --- | --- | --- | --- |
| `[metric drift]` | `[threshold]` | `[severity]` | `[owner]` | `[action]` |

## Retraining / Rollback Notes

- Retraining trigger:
- Rollback trigger:
- Human review path:
- Champion/challenger status:
- Open production risks:

## QA Checks

- [ ] Metrics are separated by model version.
- [ ] Label delay is visible.
- [ ] Calibration is reviewed if scores are used as probabilities.
- [ ] Segment performance includes sample sizes.
- [ ] Alerts have thresholds, owners, and actions.
