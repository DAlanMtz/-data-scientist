# Methodology Guide

This guide defines the senior data science lifecycle. Use it to keep analysis anchored in a decision, validated against reality, and ready for professional use.

## 1. Business Problem Framing

Before touching data, write:

- Decision: what action will change if the analysis succeeds?
- Stakeholder: who owns the action?
- Population: which users, accounts, products, stores, transactions, or time periods are in scope?
- Unit of analysis: one row represents what?
- Timing: when is the prediction or decision made?
- Cost of error: what happens with false positives, false negatives, overestimates, underestimates, or delayed decisions?
- Success metric: statistical metric, business KPI, and minimum useful lift.
- Constraints: latency, interpretability, regulation, budget, tooling, data availability, and operational capacity.

Deliverable: a one-paragraph problem statement plus a target definition.

## 2. Data Sourcing

Create a source inventory:

- Tables, files, APIs, spreadsheets, logs, surveys, third-party data, or manual extracts.
- Owner and refresh cadence.
- Primary keys and join keys.
- Event timestamps and effective dates.
- Known missingness, sampling, backfills, schema changes, and data retention limits.
- Permission, privacy, and compliance constraints.

Do not join everything blindly. Start with the minimum sources needed for the target, baseline features, and evaluation.

## 3. Data Understanding

Profile each source at the correct grain:

- Row counts by date, group, and source.
- Key uniqueness and duplicate rates.
- Missingness by field and segment.
- Distinct values for categorical fields.
- Numeric ranges, units, impossible values, and outliers.
- Timestamp coverage, time zones, late-arriving data, and gaps.
- Label coverage and delay between event and outcome.

Write down data assumptions as testable checks. If an assumption matters to validity, implement a query or code assertion for it.

## 4. EDA

EDA should answer specific questions:

- What is the base rate or baseline distribution?
- How does the target vary over time and across major segments?
- Which features are plausibly available at decision time?
- Which relationships look nonlinear, monotonic, sparse, or unstable?
- Where are outliers, missingness, data entry artifacts, or sampling artifacts?
- Are there confounders or operational policies that explain apparent patterns?

Use visuals for structure, not decoration:

- Histograms and density plots for distributions.
- Box/violin plots for segment comparisons.
- Scatter/hexbin plots for numeric relationships.
- Time series plots for trend, seasonality, and breaks.
- Heatmaps for missingness, correlation, and confusion patterns.
- Cohort tables for retention, conversion, or lifecycle questions.

End EDA with modeling implications, not a gallery of charts.

## 5. Data Cleaning

Cleaning rules must be reproducible and justified:

- Standardize types, units, categories, timestamps, and time zones.
- Remove or resolve exact duplicates and invalid records.
- Treat impossible values explicitly instead of silently coercing.
- Define imputation policy by feature type and modeling method.
- Preserve missingness indicators when missingness may be informative.
- Document exclusions and quantify how much data they remove.
- Keep raw data immutable; write cleaned or modeled views separately.

Avoid cleaning the test set using information learned from the full dataset. Fit cleaning parameters on training data where they are learned parameters.

## 6. Feature Engineering

Feature engineering starts with the prediction point:

- Only use information available before or at the decision time.
- Use rolling windows rather than full-history aggregates when predicting future outcomes.
- Respect entity boundaries: customer, account, product, store, patient, device, or session.
- Encode categorical variables using methods compatible with cardinality and sample size.
- Consider interactions only when they are plausible and validated.
- For text, define preprocessing, tokenization, embeddings, and truncation rules.
- For time series, include lag features, rolling statistics, seasonality, holidays, and external drivers only when available at forecast time.

Feature definitions should be stable enough to implement in SQL, code, or a feature store if the model is production-facing.

## 7. Baseline Modeling

Always build a baseline:

- Regression: mean, median, seasonal naive, last value, or simple linear model.
- Classification: majority class, stratified random, current rule, logistic regression.
- Ranking/recommendation: popularity, recency, business rule, or collaborative baseline.
- Clustering: simple segmentation by business rules or k-means with basic features.
- Forecasting: naive, seasonal naive, moving average, or exponential smoothing.

The baseline sets the minimum bar and often exposes target or validation mistakes.

## 8. Model Selection

Choose methods based on:

- Problem type and target structure.
- Data size, sparsity, dimensionality, and feature types.
- Need for interpretation, calibration, uncertainty, or causal claims.
- Deployment constraints: latency, dependencies, maintainability, retraining.
- Business cost of error and tolerance for false alarms.

Start simple. Add complexity only when it provides validated gain and the organization can operate it.

## 9. Validation

Validation must match the future use case:

- Random split: only for independent observations with no time or group leakage.
- Time split: for forecasting and any model deployed on future data.
- Group split: when repeated observations share an entity.
- Nested CV: when tuning and unbiased performance estimation both matter.
- Backtesting: for time series and policy simulations.
- A/B test or quasi-experiment: for causal effect of an intervention.

Keep a final holdout untouched until the end. Report variance across folds or windows when possible.

## 10. Error Analysis

After aggregate metrics, inspect failure modes:

- Largest residuals or most confident wrong predictions.
- Error by time, geography, channel, segment, product, cohort, and data source.
- Performance at operational thresholds.
- False positive and false negative examples.
- Missingness and outlier patterns in errors.
- Calibration by score band.
- Stability across validation folds or backtest windows.

Turn error analysis into action: feature fixes, data fixes, threshold changes, exclusion rules, human review, or no-go decisions.

## 11. Interpretation

Interpretation should answer:

- What are the strongest drivers?
- Are they stable across time and segments?
- Are they available and legitimate at decision time?
- Do explanations match domain knowledge?
- Are important features proxies for sensitive or disallowed attributes?
- Does the model support action, or only describe association?

Use coefficients, partial dependence, permutation importance, SHAP-style explanations, rule summaries, cluster profiles, or example-based explanation depending on the model and audience.

## 12. Decision Support

Convert analysis into decisions:

- Recommend thresholds using cost, capacity, and risk tolerance.
- Show tradeoff curves instead of a single operating point when the choice is subjective.
- Estimate expected impact with realistic adoption and constraint assumptions.
- Identify who acts on the output and what they do next.
- Provide a measurement plan: dashboard, experiment, holdout, or post-deployment review.

If the model cannot change a decision, say so and recommend a better question.

## 13. Reporting

A professional report includes:

- Executive answer and recommended action.
- Data scope, time window, population, and exclusions.
- Method summary and baseline.
- Validation design and key metrics.
- Main findings and uncertainty.
- Error modes, limitations, and responsible AI considerations.
- Decision implications and next steps.
- Reproducibility details: data version, code path, parameters, and owner.

Keep technical detail available, but do not bury the decision under implementation notes.

## 14. Deployment Readiness

Before deployment, define:

- Input schema, freshness, null behavior, ranges, and source ownership.
- Output schema, score meaning, threshold, consumer, and latency.
- Training code, scoring code, environment, dependencies, and artifact storage.
- Monitoring for data quality, drift, calibration, model performance, business KPI, and system health.
- Retraining trigger, rollback plan, manual override, and incident owner.

Notebook-only delivery is not production readiness.

## 15. Monitoring And Retraining

Monitor:

- Input volume, schema, missingness, category changes, and range shifts.
- Feature drift and prediction drift.
- Delayed label performance once outcomes arrive.
- Calibration, ranking quality, and threshold performance.
- Business KPI movement and unintended side effects.
- Latency, errors, failed jobs, and data freshness.

Retrain only when there is evidence of degradation, new policy, new data distribution, or planned refresh cadence. Validate retrained models against the incumbent before replacement.

