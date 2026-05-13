# Excel Forecasting And What-If Analysis

## Use Case

Use Excel or Sheets for lightweight forecasting, scenario analysis, and stakeholder-facing what-if models.

## Expected Inputs

- Time-indexed data with consistent frequency.
- Numeric target.
- Forecast horizon.
- Scenario assumptions such as growth, conversion, price, cost, capacity, or budget.

## Expected Outputs

- Baseline forecast.
- Moving average or smoothing-style forecast.
- Forecast error checks.
- Scenario table.
- Sensitivity or goal-seek notes.

## Concise Workflow

1. Validate date frequency and missing periods.
2. Create naive and moving-average baselines.
3. Calculate forecast errors on a holdout period.
4. Build scenario inputs in dedicated cells.
5. Use data tables, Goal Seek, or Solver for what-if questions.
6. Document assumptions and limitations.

## Forecasting Patterns

### Date Frequency Check

If dates are in column `A`:

```text
=A3-A2
```

Scan for unexpected gaps. For monthly data, use month differences rather than day differences.

### Naive Forecast

Forecast next period as last actual:

```text
=B2
```

For seasonal naive with weekly daily data:

```text
=B2-7_rows_back
```

Use an actual cell reference, such as `=B2` for lag 1 or `=B2` copied from the same weekday last week depending on layout.

### Moving Average

Seven-period moving average:

```text
=AVERAGE(B2:B8)
```

For forecasting row 9 from prior seven actuals:

```text
=AVERAGE(B2:B8)
```

Do not include the current/future actual in the forecast formula.

### Weighted Average

```text
=SUMPRODUCT(B2:B4,{0.2,0.3,0.5})
```

Put weights in cells for transparency instead of hard-coding when sharing.

### Exponential Smoothing Concept

With actual in `B`, forecast in `C`, and alpha in `$F$1`:

```text
=($F$1*B2)+((1-$F$1)*C2)
```

Test multiple alpha values on historical holdout error.

### Forecast Error Checks

```text
Error = Actual - Forecast
Absolute Error = ABS(Actual - Forecast)
Squared Error = (Actual - Forecast)^2
Percent Error = IF(Actual=0,"",ABS(Actual-Forecast)/Actual)
```

Summary metrics:

```text
MAE = AVERAGE(absolute_error_range)
RMSE = SQRT(AVERAGE(squared_error_range))
Bias = AVERAGE(forecast_range - actual_range)
```

## What-If Analysis Patterns

### Scenario Inputs

Create named input cells:

- Growth rate.
- Conversion rate.
- Average order value.
- Cost per unit.
- Capacity.
- Churn rate.

Keep assumptions separate from calculations.

### One-Way Data Table

Use for one assumption:

- Rows: candidate growth rates.
- Output: revenue, profit, staffing need, or break-even.

Excel: `Data > What-If Analysis > Data Table`.

### Goal Seek

Use when solving one input for one output:

- "What conversion rate is needed to hit revenue target?"
- "What price reaches target margin?"

Excel: `Data > What-If Analysis > Goal Seek`.

### Solver Notes

Use Solver for constrained optimization:

- Maximize profit.
- Minimize cost.
- Subject to capacity, budget, service level, or inventory constraints.

Validate Solver output with business rules; optimal does not always mean usable.

## Validation And Quality Checks

- Check missing time periods before forecasting.
- Hold out recent periods for forecast error.
- Compare against naive baseline.
- Keep formulas auditable and avoid hidden assumptions.
- Use cell protection for assumptions and formulas in shared workbooks.
- Reconcile totals to source data.

## Interpretation Notes

- Spreadsheet forecasts are useful for transparent planning and scenarios.
- Show forecast error and bias, not just future values.
- Scenario outputs are only as good as assumptions; include best/base/worst cases.

## Common Mistakes To Avoid

- Including actual future values in moving-average formulas.
- Using MAPE when actuals are zero.
- Hard-coding assumptions inside formulas.
- Forgetting filters or hidden rows.
- Presenting a single scenario as certain.
- Treating Goal Seek/Solver output as valid without constraint review.

