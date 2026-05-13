# Python Regression Example

## Use Case

Predict a numeric outcome such as spend, demand, revenue, cost, time-to-complete, or lifetime value.

## Expected Inputs

- Tabular dataset with numeric target.
- Prediction timestamp and feature availability rules.
- Business meaning of overprediction and underprediction.

## Expected Outputs

- Baseline error.
- Regression pipeline.
- RMSE, MAE, R-squared.
- Residual and error-slice review.
- Business interpretation of error.

## Concise Workflow

1. Define target units and valid range.
2. Split before preprocessing.
3. Build baseline using mean/median.
4. Train leakage-safe pipeline.
5. Evaluate aggregate and segment errors.
6. Inspect residuals and outliers.

## Representative Pattern

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.compose import ColumnTransformer
from sklearn.dummy import DummyRegressor
from sklearn.ensemble import RandomForestRegressor
from sklearn.impute import SimpleImputer
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score
from sklearn.model_selection import train_test_split
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import OneHotEncoder

target = "monthly_revenue"
X = df.drop(columns=[target, "customer_id"], errors="ignore")
y = df[target]

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

num_cols = X_train.select_dtypes(include=np.number).columns
cat_cols = X_train.select_dtypes(exclude=np.number).columns

prep = ColumnTransformer([
    ("num", SimpleImputer(strategy="median"), num_cols),
    ("cat", Pipeline([
        ("imputer", SimpleImputer(strategy="most_frequent")),
        ("onehot", OneHotEncoder(handle_unknown="ignore"))
    ]), cat_cols),
])

baseline = DummyRegressor(strategy="median").fit(X_train, y_train)
base_pred = baseline.predict(X_test)

model = Pipeline([
    ("prep", prep),
    ("reg", RandomForestRegressor(n_estimators=300, random_state=42, n_jobs=-1))
])
model.fit(X_train, y_train)
pred = model.predict(X_test)

def report(y_true, y_pred, label):
    rmse = np.sqrt(mean_squared_error(y_true, y_pred))
    mae = mean_absolute_error(y_true, y_pred)
    r2 = r2_score(y_true, y_pred)
    print(label, {"rmse": rmse, "mae": mae, "r2": r2})

report(y_test, base_pred, "baseline")
report(y_test, pred, "model")

resid = y_test - pred
plt.scatter(pred, resid, alpha=0.3)
plt.axhline(0, color="black", linewidth=1)
plt.xlabel("Predicted")
plt.ylabel("Residual")
plt.title("Residuals vs predicted")
plt.show()

errors = X_test.assign(actual=y_test, predicted=pred, error=resid, abs_error=np.abs(resid))
display(errors.sort_values("abs_error", ascending=False).head(20))
```

## Validation And Quality Checks

- Use time-aware validation for future prediction.
- Check target skew, zeros, negative values, censoring, and revisions.
- Compare model to median/mean/current-process baseline.
- Review residual bias by segment, time, and prediction range.
- Consider prediction intervals for planning decisions.

## Interpretation Notes

- MAE is typical absolute miss in target units.
- RMSE penalizes large misses.
- R-squared is context, not business value.
- Residual patterns often reveal missing features or wrong model form.

## Common Mistakes To Avoid

- Reporting only R-squared.
- Using MAPE when actuals can be zero.
- Removing real high-value outliers because they hurt metrics.
- Ignoring systematic overprediction for a key segment.
- Fitting preprocessing on full data before splitting.
