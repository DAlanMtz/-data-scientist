# Forecasting Workflow

Use this workflow when predicting future values indexed by time: demand, revenue, traffic, staffing, inventory, capacity, risk volume, or operational workload.

## Required Inputs

- Forecast target and units.
- Time index, frequency, and granularity.
- Forecast horizon.
- Historical data and known future drivers.
- Business use: planning, staffing, inventory, finance, alerts, or capacity.
- Cost of over-forecasting and under-forecasting.

## Expected Outputs

- Clean time-indexed dataset.
- Baseline and candidate forecast comparison.
- Rolling-origin validation results.
- Forecasts with intervals when appropriate.
- Error analysis by horizon, time, and segment.
- Monitoring and refresh recommendation.

## Step-By-Step Workflow

### 1. Validate Time Index

Check:

- Timestamp column and time zone.
- Frequency: hourly, daily, weekly, monthly, etc.
- Duplicate timestamps.
- Missing periods.
- Late-arriving records.
- Calendar definitions: fiscal weeks, holidays, business days.

Do not forecast until time indexing is reliable.

### 2. Define Frequency And Granularity

Specify:

- Entity level: total, product, location, customer segment, SKU, queue.
- Time grain.
- Aggregation logic.
- Whether series are independent, hierarchical, or grouped.
- Minimum history required.

Forecast at the level where decisions are made, then reconcile if needed.

### 3. Handle Missing Time Periods

Classify missing periods:

- True zero.
- Missing observation.
- System outage.
- Not applicable.
- Late-arriving data.

Fill, interpolate, exclude, or flag based on meaning. Never treat missing as zero by default.

### 4. Explore Trend And Seasonality

Inspect:

- Long-term trend.
- Weekly/monthly/annual seasonality.
- Holiday effects.
- Promotions, launches, outages, policy changes.
- Level shifts and regime changes.
- Variance changes.

Use plots with event annotations.

### 5. Build Baselines

Use:

- Naive last value.
- Seasonal naive.
- Moving average.
- Historical average by season.
- Current planning process.

Candidate models must beat relevant baselines by horizon and business segment.

### 6. Candidate Methods

Consider:

- Moving average.
- Exponential smoothing.
- ARIMA/SARIMA-style methods.
- Dynamic regression with known future drivers.
- Decomposition-based approaches.
- Machine learning with lag and rolling features.
- Hierarchical or pooled models for many related series.

Choose based on history length, seasonality, exogenous data, interpretability, and maintenance.

### 7. Build Lag And Rolling Features

For ML forecasting:

- Lag values at relevant periods.
- Rolling mean/median/min/max/std.
- Calendar features.
- Holiday and event flags.
- Known future covariates.
- Recent trend features.

Use trailing windows only. Do not use centered windows or future-known actuals.

### 8. Rolling-Origin Validation

Set up backtests:

- Train through cutoff date.
- Forecast next horizon.
- Move cutoff forward.
- Repeat across multiple windows.

Record:

- Cutoff dates.
- Horizon.
- Training window.
- Series included.
- Metrics by cutoff and horizon.

### 9. Forecast Error Metrics

Use:

- MAE for typical error.
- RMSE for large miss penalty.
- WAPE for aggregate planning.
- MASE for scale-free comparison.
- MAPE/sMAPE only when actuals are positive and not near zero.
- Bias/mean error for systematic over- or under-forecasting.
- Pinball loss for quantile forecasts.

Report horizon-specific error.

### 10. Prediction Intervals

Use intervals when planning needs risk bounds.

Check:

- Interval coverage.
- Interval width.
- Coverage by horizon and segment.
- Whether intervals reflect uncertainty from sparse or volatile series.

Recommend whether users should plan to point forecast, upper bound, or lower bound.

### 11. Error Analysis

Slice by:

- Horizon.
- Season.
- Product/location/segment.
- Volume band.
- Promotion or event periods.
- Missing/outage periods.

Investigate large misses with business context.

### 12. Monitor Forecast Drift

Monitor:

- Data freshness.
- Actual volume shifts.
- Forecast bias.
- Error by horizon.
- Interval coverage.
- Feature drift for external drivers.
- Regime changes.

Define retraining or recalibration triggers.

## Validation And Evaluation Guidance

- Use time-aware backtesting, not random splits.
- Compare to seasonal naive.
- Evaluate across multiple cutoffs.
- Keep future exogenous variables honest: only use values known at forecast time.
- Report aggregate and granular accuracy separately.

## Interpretation Guidance

- Explain trend, seasonality, recent changes, and uncertainty.
- Avoid false precision in point forecasts.
- State where forecast is unreliable.
- Translate error into staffing, inventory, budget, or capacity impact.

## Common Failure Modes

- Missing periods treated as zero incorrectly.
- Random train/test split.
- Future values used in lag/rolling features.
- Forecast horizon not tied to decision timing.
- MAPE used with zeros.
- Aggregate accuracy hides item-level failure.
- Forecast intervals omitted for risk-sensitive planning.

## Tool-Flexible Notes

- Python/R: use forecasting libraries, but keep backtesting explicit.
- SQL: create time grids, lag features, and completeness checks.
- Excel/Sheets: useful for baseline forecasts and scenario planning.
- Notebooks: show backtest windows and forecast plots.
- Production pipelines: automate data freshness checks, forecast generation, monitoring, and refresh cadence.

