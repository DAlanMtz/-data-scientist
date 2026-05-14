# Regression Workflow

Use this workflow for numeric prediction: revenue, demand, cost, price, duration, risk amount, usage, lifetime value, or any continuous target.

## Required Inputs

- Business question and decision supported by the prediction.
- Numeric target definition and prediction timestamp.
- Population, grain, and outcome window.
- Candidate features available at prediction time.
- Error cost: overprediction versus underprediction.
- Data source and validation constraints.

## Expected Outputs

- Baseline prediction and candidate model comparison.
- Validation metrics: MAE, RMSE, R-squared, and MAPE only when appropriate.
- Residual diagnostics and error analysis.
- Prediction intervals if uncertainty matters.
- Business interpretation and recommendation.

## Step-By-Step Workflow

### 1. Define Target

Specify:

- Target variable and units.
- Outcome window.
- Whether zeros or negatives are valid.
- Whether target is censored, capped, delayed, or revised.
- Prediction timestamp.
- Business meaning of over- and under-prediction.

Do not model a numeric target until units and timing are clear.

### 2. Build Baseline Prediction

Use:

- Mean or median.
- Last value.
- Seasonal naive for time-indexed targets.
- Simple business rule.
- Linear regression baseline.

The baseline establishes whether advanced modeling adds value.

### 3. Split Data

Choose:

- Random split for independent observations.
- Time split for future prediction.
- Group split for repeated entities.
- Rolling validation for temporal or panel data.

Record split logic, row counts, target distribution, and date coverage.

### 4. Feature Preprocessing

Inside validation:

- Impute missing values.
- Encode categoricals.
- Scale for distance-based, regularized, or linear models when needed.
- Transform skewed features when helpful.
- Consider target transformation for skew, but preserve inverse-transform reporting.
- Handle outliers deliberately.

Avoid full-dataset scaling, imputation, or feature selection.

### 5. Candidate Models

Consider:

- Linear regression.
- Ridge, lasso, elastic net.
- Generalized additive models.
- Regression trees.
- Random forests.
- Gradient boosting.
- Quantile regression.
- Hierarchical or mixed models when grouped structure matters.

Choose the simplest model that meets performance, interpretation, and production needs.

### Variable Selection (If Applicable)

For interpretable statistical regression, classical variable selection methods may be appropriate:

- **Backward elimination / forward selection / stepwise**: use for transparent, step-by-step variable selection in explanatory models. Treat as exploratory. For predictive performance estimation, the entire selection process must be nested inside the validation loop.
- **Best subsets**: feasible for small predictor sets; evaluate by AIC, BIC, or adjusted R-squared.
- **LASSO / elastic net**: preferred when the goal is predictive performance. The selection mechanism is nestable inside training folds and does not require pre-selecting variables.
- **Domain-driven selection**: choose predictors based on subject matter expertise first, then validate computationally.

**Guardrail**: do not run any data-driven variable selection on the full dataset and then report test-set performance as unbiased. This inflates apparent performance.

### 6. Cross-Validation

Use:

- K-fold CV for independent rows.
- Group CV for repeated entities.
- Time-aware CV or rolling origin for time-dependent data.

Report metric mean and variability.

### 7. Metrics

Use:

- MAE for typical absolute error.
- RMSE when large misses are especially costly.
- R-squared as explanatory context, not the sole success metric.
- MAPE only when actuals are positive and not near zero.
- WAPE or MASE for forecasting-style comparisons.
- Quantile loss for percentile predictions.

Translate metrics into business units.

### 8. Residual Diagnostics

Check:

- Actual versus predicted.
- Residuals versus fitted values.
- Residual distribution.
- Residuals by time, segment, and source.
- Bias overall and by group.
- Heteroscedasticity.
- Nonlinear patterns.

Residual structure indicates missing features, wrong model form, outliers, or population differences.

### 9. Outlier And Influential Point Checks

Inspect:

- Largest absolute errors.
- High leverage points.
- High-value target tail.
- Data entry errors.
- Real but rare cases.

Decide whether to correct, cap, model separately, use robust loss, or keep with caveat.

### 10. Prediction Intervals

Use intervals when planning, risk, staffing, inventory, or financial exposure depends on uncertainty.

Options:

- Quantile regression.
- Bootstrapped intervals.
- Bayesian intervals.
- Forecast intervals.
- Empirical residual intervals by segment or horizon.

Check interval coverage on validation data.

### 11. Error Analysis

Slice error by:

- Time period.
- Segment.
- Target size bands.
- Product/geography/channel.
- Missingness.
- Feature availability.

Recommend fixes based on error concentration, not guesswork.

### 12. Business Interpretation

Report:

- Typical error in business units.
- Where the model is reliable.
- Where it should not be trusted.
- Whether errors are acceptable for the decision.
- Tradeoff between accuracy, interpretability, and maintenance.

## Validation And Evaluation Guidance

- Compare every model to baseline.
- Keep transformation fitting inside validation.
- Use time-aware validation for future-facing predictions.
- Report both aggregate and segment-level error.
- Check whether the metric matches business cost.

## Interpretation Guidance

- Coefficients are associations under model assumptions.
- Feature importance is not causal.
- Residual patterns are often more actionable than global metrics.
- Use prediction intervals when point estimates could create false precision.

## Common Failure Modes

- Optimizing RMSE when typical error or asymmetric cost matters more.
- Reporting R-squared as business value.
- Using MAPE with zeros or tiny actuals.
- Ignoring systematic residual bias.
- Removing high-value outliers that are real business cases.
- Target transformation reported without inverse-transform clarity.

## Tool-Flexible Notes

- Python/R: use pipelines/recipes and diagnostic plots.
- SQL: create leakage-safe numeric aggregates and target summaries.
- Excel/Sheets: useful for baseline, residual review, and scenario tables.
- Notebooks: show residual diagnostics near the metric table.
- Production pipelines: monitor error by segment and prediction drift once labels arrive.

