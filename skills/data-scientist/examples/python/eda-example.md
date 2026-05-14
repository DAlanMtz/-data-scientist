# Python EDA Example

## Use Case

Explore a tabular dataset before modeling or reporting: understand schema, data quality, distributions, relationships, and target readiness.

## Expected Inputs

- CSV/parquet/database extract or dataframe.
- Business objective, target column if known, entity grain, and date fields.
- Data dictionary if available.

## Expected Outputs

- Data quality summary.
- EDA tables and plots.
- Target review.
- Initial feature ideas.
- Modeling-readiness notes.

## Concise Workflow

1. Load data and record row/column counts.
2. Inspect schema and grain.
3. Check missingness, duplicates, ranges, and dates.
4. Summarize distributions and relationships.
5. Review target distribution and leakage candidates.
6. Write readiness assessment and next steps.

## Representative Pattern

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.read_csv("data.csv", parse_dates=["created_at"])

print(df.shape)
display(df.head())
display(df.dtypes)

# Schema and grain checks
key = "customer_id"
print("unique keys:", df[key].nunique(), "rows:", len(df))
display(df.duplicated().value_counts())
display(df[key].duplicated().value_counts())

# Missingness
missing = (
    df.isna().mean()
      .sort_values(ascending=False)
      .rename("missing_rate")
      .to_frame()
)
display(missing.head(20))

# Descriptive stats
display(df.describe(include="all", datetime_is_numeric=True).T)

# Date coverage
date_col = "created_at"
display(df[date_col].agg(["min", "max"]))
df.set_index(date_col).resample("M").size().plot(title="Rows by month")
plt.show()

# Numeric distributions
num_cols = df.select_dtypes(include=np.number).columns
df[num_cols].hist(figsize=(12, 8), bins=30)
plt.tight_layout()
plt.show()

# Target review
target = "churned"
if target in df:
    print(df[target].value_counts(dropna=False, normalize=True))
    df.groupby(pd.Grouper(key=date_col, freq="M"))[target].mean().plot(
        title=f"{target} rate over time"
    )
    plt.show()

# Relationship example
if {"monthly_spend", target}.issubset(df.columns):
    df.boxplot(column="monthly_spend", by=target)
    plt.title("Monthly spend by target")
    plt.suptitle("")
    plt.show()
```

## Validation And Quality Checks

- Confirm one row means what the project claims it means.
- Reconcile row counts after filters and joins.
- Check duplicate keys before aggregation or modeling.
- Review missingness by time/source/segment, not only globally.
- Verify target timing before proposing features.
- Flag columns with names like `status`, `resolved`, `cancelled`, `refund`, `final`, or `outcome`.

## Interpretation Notes

- Treat EDA patterns as hypotheses unless validation or experiment design supports stronger claims.
- Translate findings into decisions: data fix, feature candidate, exclusion rule, or modeling risk.
- Report denominators with all rates.

## Common Mistakes To Avoid

- Dropping outliers before understanding business meaning.
- Imputing missing values during EDA without documenting why.
- Creating features from full data before deciding validation strategy.
- Showing many charts without conclusions.
- Ignoring target drift over time.

