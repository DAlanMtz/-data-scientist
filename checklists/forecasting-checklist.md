# Forecasting Checklist

Use for time-series or panel forecasting review before accepting forecast accuracy or operationalizing forecasts.

## Time Index And Grain

- [ ] Time index is present, parsed, and timezone-consistent.
- [ ] Frequency is defined: hourly, daily, weekly, monthly, etc.
- [ ] Forecast grain matches decision grain.
- [ ] Duplicate timestamps are handled.
- [ ] Missing periods are identified.
- [ ] Calendar/fiscal definitions are documented.
- [ ] Data latency and late-arriving records are understood.

## Forecast Objective

- [ ] Forecast horizon is defined.
- [ ] Forecast update cadence is defined.
- [ ] Target units are clear.
- [ ] Over-forecast and under-forecast costs are understood.
- [ ] Forecast consumers and decisions are identified.
- [ ] Required prediction interval or service level is known.

## Data Preparation

- [ ] Missing periods are classified as zero, missing, outage, or not applicable.
- [ ] Outliers are reviewed with business context.
- [ ] Stockouts, censored demand, or capacity constraints are flagged.
- [ ] External drivers are known at forecast time.
- [ ] Aggregation level is consistent.
- [ ] Backfills and revisions are documented.

## Trend, Seasonality, And Events

- [ ] Trend is inspected.
- [ ] Weekly/monthly/annual seasonality is inspected.
- [ ] Holidays and calendar effects are considered.
- [ ] Promotions, launches, outages, and policy changes are annotated.
- [ ] Regime shifts or structural breaks are reviewed.
- [ ] Seasonal patterns are checked by segment or series.

## Baselines And Methods

- [ ] Naive baseline is included.
- [ ] Seasonal naive baseline is included when seasonality exists.
- [ ] Moving average baseline is considered.
- [ ] Exponential smoothing is considered.
- [ ] ARIMA/SARIMA-style methods are considered where appropriate.
- [ ] ML forecasting with lag/rolling features is leakage-safe.
- [ ] Model complexity is justified by backtest improvement.

## Leakage Checks

- [ ] Rolling features use trailing windows only.
- [ ] Future target values are not used in features.
- [ ] Future external variables are included only if truly known at forecast time.
- [ ] Scaling or transformations are fit within training windows.
- [ ] Backtest feature generation mimics production timing.
- [ ] Random split is not used for time-dependent forecasts.

## Validation And Backtesting

- [ ] Rolling-origin validation is used.
- [ ] Multiple cutoffs are evaluated.
- [ ] Horizon-specific error is reported.
- [ ] Backtest windows reflect operational retraining cadence.
- [ ] Final holdout period is preserved if possible.
- [ ] Sparse or short-history series are handled separately.

## Metrics

- [ ] MAE and/or RMSE are reported.
- [ ] WAPE or MASE is considered for scale-aware comparison.
- [ ] MAPE is avoided when actuals include zeros or tiny values.
- [ ] Bias/mean error is reported.
- [ ] Prediction interval coverage is checked when intervals are used.
- [ ] Metrics are translated into business impact.

## Monitoring And Retraining

- [ ] Data freshness is monitored.
- [ ] Forecast bias is monitored.
- [ ] Error by horizon is monitored.
- [ ] Prediction interval coverage is monitored.
- [ ] Drift in external drivers is monitored.
- [ ] Retraining cadence or trigger is defined.
- [ ] Forecast owner is identified.

## Minimum Acceptable Standard

- [ ] Time index is valid, naive baseline exists, rolling-origin backtest is used, leakage checks pass, and horizon-specific metrics are reported.

## Strong Practice

- [ ] Forecast intervals are included for planning decisions.
- [ ] Backtests span multiple seasons or business cycles where available.
- [ ] Forecast monitoring includes both model error and business guardrails.

## Red Flags

- [ ] Random train/test split.
- [ ] Centered rolling windows.
- [ ] Missing periods silently filled as zero.
- [ ] MAPE headline with zero-heavy data.
- [ ] Aggregate forecast accuracy hides poor item/location performance.
- [ ] Forecast is used for planning without uncertainty.

