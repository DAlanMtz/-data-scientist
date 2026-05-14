# Pre-Modeling Checklist

Use before building any model, forecast, segmentation, recommender, anomaly detector, or decision rule.

## Business And Decision Clarity

- [ ] Business question is stated as a decision or action, not just a modeling task.
- [ ] Decision owner and user of the output are identified.
- [ ] Intended use and non-intended use are documented.
- [ ] Cost of wrong decisions is described.
- [ ] Operational constraints are known: timing, capacity, latency, budget, policy, or staffing.
- [ ] Success metric is tied to business value.
- [ ] Minimum useful performance or lift is defined.

## Target Definition

- [ ] Target variable is clearly named and defined.
- [ ] Outcome window is specified.
- [ ] Positive class or numeric unit is unambiguous.
- [ ] Label source is known.
- [ ] Label delay is understood.
- [ ] Ambiguous labels and exclusions are handled explicitly.
- [ ] Target does not encode post-decision information unless that is the actual prediction point.

## Unit Of Analysis And Grain

- [ ] One row represents a clearly defined entity/event/time period.
- [ ] Primary key or composite key is identified.
- [ ] Repeated entities are understood.
- [ ] Joins do not unintentionally change grain.
- [ ] Aggregations match the intended prediction or decision unit.

## Prediction Timing

- [ ] Prediction timestamp is defined.
- [ ] Features are limited to information available at prediction time.
- [ ] Data freshness requirements are known.
- [ ] Late-arriving data behavior is understood.
- [ ] Time zones and date semantics are checked.

## Data Sources

- [ ] Source tables/files/APIs/sheets are inventoried.
- [ ] Data owners are known.
- [ ] Refresh cadence is documented.
- [ ] Join keys are identified.
- [ ] Data lineage is sufficient to trace target and key features.
- [ ] Access, privacy, and retention constraints are understood.

## Schema And Types

- [ ] Required fields are present.
- [ ] Data types match business meaning.
- [ ] IDs with leading zeros are treated as strings.
- [ ] Dates parse correctly.
- [ ] Numeric units are consistent.
- [ ] Category levels are reviewed for unexpected values.

## Missingness

- [ ] Missing rate is measured by field.
- [ ] Missingness is checked by time, source, segment, and target.
- [ ] Missing values are distinguished from zero, not applicable, unknown, and not collected.
- [ ] Missingness that may be predictive or process-driven is flagged.
- [ ] Imputation strategy is not chosen before understanding missingness meaning.

## Duplicates And Outliers

- [ ] Exact duplicates are measured.
- [ ] Duplicate keys are measured.
- [ ] Near-duplicate entity/event/text records are considered.
- [ ] Outliers are identified and classified as real, error, or different population.
- [ ] Outlier handling does not remove important high-risk or high-value cases without justification.

## Leakage Risks

- [ ] Features are reviewed for future information.
- [ ] Status, resolution, refund, cancellation, diagnosis, or outcome-reason fields are inspected.
- [ ] Aggregates are cut off before prediction time.
- [ ] Preprocessing will be fit only on training data or inside validation folds.
- [ ] Entity overlap across train/test is considered.
- [ ] Text, documents, and repeated events are checked for duplicate leakage.

## Baseline And Metrics

- [ ] Baseline is defined before candidate models.
- [ ] Metric matches the business cost and action.
- [ ] For rare-event classification, accuracy is not the primary metric.
- [ ] For numeric prediction, over- and under-prediction costs are considered.
- [ ] For forecasting, naive or seasonal naive baseline is included.
- [ ] For ranking, `k` matches operational capacity.

## Responsible Use

- [ ] Affected people or stakeholders are identified.
- [ ] Sensitive or protected variables are flagged.
- [ ] Proxy variables are considered.
- [ ] Human review needs are assessed.
- [ ] Privacy, consent, and permitted-use constraints are checked.
- [ ] High-risk domain review is triggered if relevant.

## Minimum Acceptable Standard

- [ ] Business decision, target, grain, prediction time, baseline, metric, and validation approach are all defined.
- [ ] Major data quality and leakage risks are identified before modeling.
- [ ] There is enough data and label quality to support the intended claim.

## Strong Practice

- [ ] Data inventory includes owner, refresh cadence, grain, and known issues.
- [ ] Data quality checks are executable in SQL, Python, R, spreadsheet formulas, or pipeline tests.
- [ ] A short pre-modeling memo records assumptions and go/no-go decision.

## Red Flags

- [ ] "Predict X" is requested but no action changes based on the prediction.
- [ ] Target is a final status available only after the event.
- [ ] Feature list includes obvious outcome-derived fields.
- [ ] Row grain is unclear after joins.
- [ ] No baseline or success metric exists.
- [ ] Sensitive or high-impact use is proposed without review.

