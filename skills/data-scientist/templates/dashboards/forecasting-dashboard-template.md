# Forecasting Dashboard Template

Use this for time-series planning, forecast monitoring, and forecast accuracy review.

## Forecast Context

- Business decision:
- Forecasted metric:
- Forecast grain:
- Forecast horizon:
- Forecast generation cadence:
- Model/version:
- Owner:

## Actual Vs Forecast

- Actual metric:
- Forecast value:
- Forecast generation timestamp:
- Horizon:
- Date range:

Recommended visual: line chart with actuals, forecast, and forecast generation marker.

## Prediction Intervals

- Lower bound:
- Upper bound:
- Confidence/coverage level:
- Interval coverage review:

Recommended visual: forecast band chart.

## Error Metrics

| Metric | Current | Target/baseline | Notes |
| --- | ---: | ---: | --- |
| MAE | `[value]` | `[target]` | `[notes]` |
| RMSE | `[value]` | `[target]` | `[notes]` |
| MAPE/sMAPE/WAPE | `[value]` | `[target]` | `[use only when appropriate]` |
| Bias | `[value]` | `[target]` | `[over/under forecasting]` |

## Error By Segment / Time

- Error by horizon:
- Error by product/location/channel:
- Error by season/event period:
- Top exceptions:

Recommended visuals: heatmap, ranked error table, small multiples.

## Trend / Seasonality

- Trend component:
- Seasonal pattern:
- Holiday/event effects:
- Structural breaks:
- Missing periods:

## Forecast Bias

- Systematic overforecasting:
- Systematic underforecasting:
- Bias by segment:
- Decision impact:

## Exceptions

| Entity/segment | Period | Forecast | Actual | Error | Severity | Action |
| --- | --- | ---: | ---: | ---: | --- | --- |
| `[entity]` | `[period]` | `[forecast]` | `[actual]` | `[error]` | `[severity]` | `[action]` |

## Data Freshness

- Latest actual timestamp:
- Latest forecast run:
- Missing/late data:
- Stale threshold:

## Decision / Action Section

- Planning decision:
- Recommended action:
- Capacity/inventory/budget implication:
- Owner:
- Review date:

## QA Checks

- [ ] Forecasts are evaluated using values generated before actuals were known.
- [ ] Horizon is clear.
- [ ] Intervals are shown where uncertainty matters.
- [ ] Error metrics match the business loss.
- [ ] Incomplete periods and missing data are labeled.
