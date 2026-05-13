# Model Card Template

Use this template to document a trained model, scoring rule, recommender, forecast model, anomaly detector, or production-facing analytic model.

## Model Card

### Model Name

`[model name and version]`

### Purpose

- Business problem:
- Decision supported:
- Model family:
- Owner:
- Status: `[experimental/pilot/production/deprecated]`

### Intended Use

- Intended users:
- Intended population:
- Intended action:
- Frequency of use:
- Human review role:

### Non-Intended Use

Do not use this model for:

- `[unsupported population]`
- `[unsupported decision]`
- `[causal claims if predictive only]`
- `[automated high-impact decisions if not approved]`

### Data Used

| Dataset | Source | Time window | Grain | Rows | Notes |
| --- | --- | --- | --- | ---: | --- |
| `[dataset]` | `[source]` | `[window]` | `[grain]` | `[n]` | `[notes]` |

Include known exclusions, sampling, label delay, and quality issues.

### Target Variable

- Target name:
- Definition:
- Outcome window:
- Positive class or units:
- Label source:
- Known label limitations:

### Features

| Feature family | Examples | Source | Availability at prediction time | Notes |
| --- | --- | --- | --- | --- |
| `[family]` | `[features]` | `[source]` | `[yes/no]` | `[notes]` |

Flag sensitive variables, proxy candidates, and production-unavailable features.

### Training And Evaluation Method

- Training period:
- Validation design:
- Test/holdout design:
- Cross-validation:
- Baseline:
- Candidate models considered:
- Selected model rationale:
- Preprocessing:
- Hyperparameters:

### Metrics

| Metric | Validation | Test/Holdout | Baseline | Notes |
| --- | ---: | ---: | ---: | --- |
| `[metric]` | `[value]` | `[value]` | `[value]` | `[notes]` |

Include threshold-specific metrics when actions are thresholded.

### Error Analysis

- Strongest performance areas:
- Weakest performance areas:
- Key false positives or overpredictions:
- Key false negatives or underpredictions:
- Segment/subgroup findings:
- Calibration findings:

### Interpretation

- Main predictive signals:
- Explanation method:
- Example explanation:
- Interpretation cautions:

### Limitations

- Data limitations:
- Method limitations:
- Validation limitations:
- Operational limitations:
- Generalization limits:

### Responsible AI Considerations

- Affected users:
- Sensitive/protected attributes reviewed:
- Proxy-risk review:
- Fairness/subgroup metrics:
- Privacy considerations:
- Human oversight:
- Misuse risks:
- Mitigations:

### Monitoring Plan

Monitor:

- Data freshness and schema.
- Feature drift.
- Prediction drift.
- Performance when labels arrive.
- Calibration.
- Business KPIs.
- Subgroup performance.
- System latency/errors.

Alert owner:

- `[owner/team]`

### Maintenance And Retraining Plan

- Retraining cadence:
- Retraining triggers:
- Champion/challenger process:
- Rollback plan:
- Deprecation criteria:

### Approval Status

| Role | Name | Decision | Date | Notes |
| --- | --- | --- | --- | --- |
| Business owner | `[name]` | `[approved/pending/rejected]` | `[date]` | `[notes]` |
| Data science owner | `[name]` | `[approved/pending/rejected]` | `[date]` | `[notes]` |
| Engineering owner | `[name]` | `[approved/pending/rejected]` | `[date]` | `[notes]` |
| Risk/legal/compliance | `[name]` | `[approved/pending/not needed]` | `[date]` | `[notes]` |

## Validation And Evaluation Guidance

- Include baseline comparison.
- Include split design and target timing.
- Report subgroup performance for consequential models.
- State if metrics are validation-only or final holdout.

## Common Failure Modes

- Intended use too broad.
- Limitations omitted.
- No non-intended use.
- Metrics reported without threshold or population.
- Monitoring plan is generic.
- Responsible AI review reduced to a checkbox.

