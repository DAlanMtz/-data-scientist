# Experiment Design And Tracking

Use this guide to keep model and analysis experiments fair, reproducible, and decision-oriented.

## Baselines

Every experiment needs a baseline:

- Current business process.
- Majority class, mean, median, naive forecast, seasonal naive forecast.
- Simple linear/logistic model.
- Popularity or recency recommender.
- Existing production model.

Record baseline performance before tuning complex models. If a complex method does not clearly beat the baseline under the right validation design, do not promote it.

## Experiment Logs

Maintain a log for any nontrivial modeling project. It can live in a notebook table, spreadsheet, Markdown file, MLflow/W&B-style tracker, database table, or project issue.

Minimum structure:

| Field | Description |
| --- | --- |
| experiment_id | Unique run or comparison ID |
| date | Run date |
| owner | Person or agent running it |
| question | What this experiment tests |
| data_version | Snapshot, query, file hash, or extraction timestamp |
| target_version | Target definition and outcome window |
| split_version | Split logic, seed, cutoff, or fold definition |
| feature_set | Feature list or feature set ID |
| method | Model or analysis method |
| params | Key hyperparameters and config |
| metrics | Primary and secondary metrics |
| diagnostics | Error, calibration, stability, or subgroup notes |
| decision | Keep, reject, revise, or investigate |
| notes | Caveats and follow-up |

## Versioning

Version:

- Data extract or table partitions.
- Target logic.
- Feature definitions.
- Train/validation/test split.
- Code.
- Config.
- Model artifact.
- Reported metrics.

Do not compare experiments that silently use different target definitions or validation splits.

## Train/Test Split Records

Record:

- Split type: random, stratified, time, group, rolling, nested.
- Date cutoffs.
- Group keys.
- Random seed.
- Row counts and target rates by split.
- Exclusion rules.
- Reason the split matches deployment.

If the split changes, previous metric comparisons may no longer be valid.

## Feature Set Tracking

Track:

- Feature names and definitions.
- Source tables/files.
- Time windows.
- Availability at prediction time.
- Missing-value handling.
- Encoding and transformation choices.
- Whether feature is production-ready.

Use feature set IDs such as `baseline_features_v1`, `behavior_30d_v2`, or `text_embeddings_v1`.

## Hyperparameter Tracking

Record only what affects results:

- Model class and library/version.
- Search space.
- Selected parameters.
- Tuning metric.
- Tuning split or folds.
- Early stopping rules.
- Random seed.

Do not tune on the final test set. If that happened, create a new holdout or downgrade the claim.

## Fair Comparisons

For fair model comparisons:

- Use the same target.
- Use the same train/validation/test split.
- Use the same candidate population.
- Use the same feature availability rules.
- Evaluate with the same metrics.
- Include the baseline.
- Compare uncertainty, not only point estimates.
- Account for runtime, dependencies, maintainability, and production cost.

Reject comparisons where one model benefits from future data, extra labels, or test-set tuning.

## Ablation Tests

Use ablation to learn what matters:

- Remove one feature family at a time.
- Compare baseline features versus advanced features.
- Compare with and without text, geospatial, behavioral, or historical aggregates.
- Compare simple preprocessing versus complex preprocessing.
- Compare calibrated versus uncalibrated scores.

Record both metric change and operational change. A small metric gain from a fragile feature may not be worth it.

## Error Analysis Tracking

For each serious model candidate, track:

- Worst residuals or highest-confidence errors.
- Error by time window.
- Error by segment, source, geography, or channel.
- Error by missingness or category.
- Calibration by score band.
- Threshold tradeoffs.
- Examples reviewed and conclusions.

Convert findings into experiment ideas or deployment warnings.

## Reproducibility

A run is reproducible when another analyst can recover:

- Input data.
- Code and environment.
- Split.
- Feature set.
- Model parameters.
- Output metrics.
- Artifact.

If using notebooks, restart and run all before treating the result as final.

## Decision Records

Create a short decision record when selecting a model or analysis path:

- Decision: selected [method/feature set/threshold].
- Rationale: [metric improvement, interpretability, stability, cost].
- Alternatives considered: [options].
- Rejected because: [reason].
- Risks: [known limitations].
- Review trigger: [date, drift, performance, business change].

This is especially important when choosing a simpler model over a higher-scoring complex model.

## When To Stop Experimenting

Stop when:

- The model meets the business requirement with acceptable risk.
- Further gains are within validation noise.
- Error analysis points to data or label limitations, not model class.
- Added complexity is not production-justified.
- The decision deadline has arrived and uncertainty is documented.
- A pilot or experiment is needed to learn more.

Continuing to tune after the conclusion is stable usually creates overfitting and muddier communication.

