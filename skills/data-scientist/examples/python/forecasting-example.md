# Python Forecasting Example

## Use Case

Forecast a numeric time-indexed outcome such as demand, tickets, revenue, traffic, or staffing load.

## Expected Inputs

- Time-indexed data with target.
- Forecast horizon and frequency.
- Known future covariates, if any.
- Business cost of forecast error.

## Expected Outputs

- Time-index validation.
- Naive baseline.
- Lag/rolling feature model.
- Time-aware error metrics.
- Drift and retraining notes.

## Concise Workflow

1. Validate time index and frequency.
2. Create complete time grid.
3. Build naive baseline.
4. Create lag and rolling features using past data only.
5. Split by time.
6. Evaluate by horizon or holdout period.

## Representative Pattern

```python
import pandas as pd
import numpy as np
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_absolute_error, mean_squared_error

ts = (
    df.assign(date=pd.to_datetime(df["date"]))
      .groupby("date", as_index=False)["orders"].sum()
      .sort_values("date")
)

# Complete daily grid
idx = pd.date_range(ts["date"].min(), ts["date"].max(), freq="D")
ts = ts.set_index("date").reindex(idx).rename_axis("date").reset_index()
ts["orders"] = ts["orders"].fillna(0)  # only valid if missing means zero activity

ts["lag_1"] = ts["orders"].shift(1)
ts["lag_7"] = ts["orders"].shift(7)
ts["roll_7_mean"] = ts["orders"].shift(1).rolling(7).mean()
ts["dow"] = ts["date"].dt.dayofweek
ts["month"] = ts["date"].dt.month
ts = ts.dropna()

cutoff = ts["date"].max() - pd.Timedelta(days=30)
train = ts[ts["date"] <= cutoff]
test = ts[ts["date"] > cutoff]

features = ["lag_1", "lag_7", "roll_7_mean", "dow", "month"]
baseline_pred = test["lag_7"]  # seasonal naive weekly baseline

model = RandomForestRegressor(n_estimators=300, random_state=42)
model.fit(train[features], train["orders"])
pred = model.predict(test[features])

def metrics(y, yhat):
    return {
        "mae": mean_absolute_error(y, yhat),
        "rmse": np.sqrt(mean_squared_error(y, yhat)),
        "bias": float(np.mean(yhat - y)),
    }

print("baseline:", metrics(test["orders"], baseline_pred))
print("model:", metrics(test["orders"], pred))
```

## Validation And Quality Checks

- Use rolling-origin validation for final model comparisons.
- Avoid random splits.
- Use only trailing rolling windows.
- Confirm missing periods are truly zero before filling.
- Evaluate horizon-specific error for multi-step forecasts.
- Compare against naive and seasonal naive baselines.

## Interpretation Notes

- Bias indicates systematic over- or under-forecasting.
- RMSE exposes large misses; MAE reflects typical miss.
- Forecasts need intervals or scenario ranges when used for planning.

## Common Mistakes To Avoid

- Using centered rolling windows.
- Letting future covariates leak into training.
- Filling outages as zero demand.
- Reporting aggregate accuracy while key segments fail.
- Using MAPE with zero-heavy series.
