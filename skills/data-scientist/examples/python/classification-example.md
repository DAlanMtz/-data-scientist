# Python Classification Example

## Use Case

Build a leakage-safe binary classification baseline and model for a decision such as churn risk, lead conversion, fraud review, or defect detection.

## Expected Inputs

- Tabular dataset with a binary or multiclass target.
- Feature list, target definition, prediction timestamp, and split strategy.
- Business cost or capacity constraint for threshold choice.

## Expected Outputs

- Baseline comparison.
- Preprocessing/model pipeline.
- Validation metrics and confusion matrix.
- Threshold discussion and error analysis.

## Concise Workflow

1. Define target and remove unavailable/leaky fields.
2. Split data before preprocessing.
3. Build `ColumnTransformer` and `Pipeline`.
4. Compare baseline and model.
5. Evaluate ROC-AUC/PR-AUC, confusion matrix, precision, recall, F1.
6. Choose threshold from business cost/capacity, not default habit.

## Representative Pattern

```python
import numpy as np
import pandas as pd
from sklearn.compose import ColumnTransformer
from sklearn.dummy import DummyClassifier
from sklearn.impute import SimpleImputer
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import (
    average_precision_score, classification_report, confusion_matrix,
    precision_recall_curve, roc_auc_score
)
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import OneHotEncoder, StandardScaler

target = "churned"
leaky_or_ids = ["customer_id", "cancelled_at", "final_status"]
X = df.drop(columns=[target] + [c for c in leaky_or_ids if c in df])
y = df[target].astype(int)

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, stratify=y, random_state=42
)

num_cols = X_train.select_dtypes(include=np.number).columns
cat_cols = X_train.select_dtypes(exclude=np.number).columns

preprocess = ColumnTransformer(
    transformers=[
        ("num", Pipeline([
            ("imputer", SimpleImputer(strategy="median")),
            ("scaler", StandardScaler())
        ]), num_cols),
        ("cat", Pipeline([
            ("imputer", SimpleImputer(strategy="most_frequent")),
            ("onehot", OneHotEncoder(handle_unknown="ignore"))
        ]), cat_cols),
    ]
)

baseline = DummyClassifier(strategy="most_frequent")
baseline.fit(X_train, y_train)
print("baseline accuracy:", baseline.score(X_test, y_test))

model = Pipeline([
    ("prep", preprocess),
    ("clf", LogisticRegression(max_iter=1000, class_weight="balanced"))
])

cv_auc = cross_val_score(model, X_train, y_train, cv=5, scoring="roc_auc")
print("cv roc auc:", cv_auc.mean(), cv_auc.std())

model.fit(X_train, y_train)
proba = model.predict_proba(X_test)[:, 1]

print("roc_auc:", roc_auc_score(y_test, proba))
print("pr_auc:", average_precision_score(y_test, proba))

threshold = 0.35
pred = (proba >= threshold).astype(int)
print(confusion_matrix(y_test, pred))
print(classification_report(y_test, pred))

precision, recall, thresholds = precision_recall_curve(y_test, proba)
```

## Validation And Quality Checks

- Use time-aware or group-aware split if rows are temporal or repeated by entity.
- Fit imputers, encoders, scalers, feature selectors, and resampling only inside training/folds.
- Check class balance by split.
- Use PR-AUC, precision@k, or recall@k for rare positives.
- Check calibration before using scores as probabilities.

## Interpretation Notes

- ROC-AUC measures ranking, not operational threshold quality.
- Precision answers review yield; recall answers event capture.
- Coefficients from logistic regression are associations, not causal effects.
- Threshold should reflect business costs, reviewer capacity, or required service level.

## Common Mistakes To Avoid

- Reporting accuracy for rare events.
- Choosing threshold on the test set after repeated attempts.
- Oversampling before splitting.
- Leaving post-outcome status fields in the feature matrix.
- Treating uncalibrated scores as exact probabilities.

