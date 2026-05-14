# Python Anomaly Detection Example

## Use Case

Flag unusual records or time periods for investigation, such as transaction spikes, quality defects, fraud candidates, or system incidents.

## Expected Inputs

- Feature table at entity/event/time grain.
- Anomaly definition and investigation capacity.
- Known incident labels if available.

## Expected Outputs

- Rule-based or model-based anomaly scores.
- Threshold and alert volume.
- False-positive review table.
- Monitoring and escalation notes.

## Concise Workflow

1. Define what kind of anomaly matters.
2. Build interpretable baseline using robust statistics.
3. Optionally fit isolation forest for multivariate anomalies.
4. Choose threshold using capacity and review yield.
5. Create reason columns for investigation.
6. Monitor alert volume and drift.

## Representative Pattern

```python
import numpy as np
import pandas as pd
from sklearn.ensemble import IsolationForest
from sklearn.impute import SimpleImputer
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler

feature_cols = ["amount", "events_1h", "failed_attempts", "account_age_days"]
X = df[feature_cols]

# Robust z-score baseline for one important field
median = df["amount"].median()
mad = np.median(np.abs(df["amount"] - median))
df["amount_robust_z"] = 0.6745 * (df["amount"] - median) / max(mad, 1e-9)
df["amount_rule_alert"] = df["amount_robust_z"].abs() >= 4

# Multivariate anomaly score
pipe = Pipeline([
    ("imputer", SimpleImputer(strategy="median")),
    ("scaler", StandardScaler()),
    ("iso", IsolationForest(contamination=0.02, random_state=42))
])

pipe.fit(X)
df["anomaly_score"] = -pipe.named_steps["iso"].score_samples(
    pipe.named_steps["scaler"].transform(
        pipe.named_steps["imputer"].transform(X)
    )
)
threshold = df["anomaly_score"].quantile(0.98)
df["model_alert"] = df["anomaly_score"] >= threshold

alerts = df[df["model_alert"]].sort_values("anomaly_score", ascending=False)
display(alerts[["anomaly_score"] + feature_cols].head(50))
print("alert volume:", len(alerts), "of", len(df))
```

## Validation And Quality Checks

- Backtest known incidents when labels exist.
- Review top alerts manually for false-positive themes.
- Check alert volume by day/source/segment.
- Account for seasonality and peer groups.
- Exclude known incident periods from normal training when appropriate.

## Interpretation Notes

- Anomaly score means unusualness, not confirmed wrongdoing or failure.
- Provide reason columns: which feature was extreme, compared to what baseline.
- Threshold should reflect investigation capacity, not only statistical rarity.

## Common Mistakes To Avoid

- Deploying alerts with no reviewer workflow.
- Treating seasonal peaks as anomalies.
- Training normal behavior on known incident periods.
- Creating too many duplicate alerts.
- Using a black-box score with no explanation path.

