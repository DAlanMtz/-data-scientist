# Python Visualization Example

## Use Case

Use pandas and matplotlib to inspect data quality, understand distributions and relationships, and create model diagnostic visuals in a notebook or report.

## Expected Inputs

- pandas dataframe.
- Date column, segment columns, numeric metrics, and optional target/model predictions.
- Business question for each chart.

## Expected Outputs

- Data inspection visuals.
- Missingness and distribution charts.
- Relationship and time-series charts.
- Model diagnostic visuals.
- Captions that state takeaways.

## Concise Workflow

1. Shape data with pandas.
2. Create one chart per question.
3. Label axes, units, time window, and denominator.
4. Write a one-sentence interpretation under each chart.
5. Save or export only decision-relevant visuals.

## Representative Pattern

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

df["order_date"] = pd.to_datetime(df["order_date"])

# Row count over time: data coverage
monthly = df.set_index("order_date").resample("M").size()
monthly.plot(figsize=(8, 4), title="Rows by month")
plt.ylabel("Rows")
plt.tight_layout()
plt.show()

# Missingness summary
missing = df.isna().mean().sort_values(ascending=True)
missing.tail(20).plot(kind="barh", figsize=(8, 5), title="Highest missingness rates")
plt.xlabel("Missing rate")
plt.tight_layout()
plt.show()

# Histogram
df["amount"].dropna().hist(bins=40, figsize=(7, 4))
plt.title("Order amount distribution")
plt.xlabel("Order amount")
plt.ylabel("Orders")
plt.tight_layout()
plt.show()

# Boxplot by segment
df.boxplot(column="amount", by="region", figsize=(8, 4))
plt.title("Order amount by region")
plt.suptitle("")
plt.ylabel("Order amount")
plt.tight_layout()
plt.show()

# Scatter plot
sample = df.sample(min(len(df), 5000), random_state=42)
plt.scatter(sample["tenure_days"], sample["amount"], alpha=0.25)
plt.title("Amount versus customer tenure")
plt.xlabel("Tenure days")
plt.ylabel("Order amount")
plt.tight_layout()
plt.show()

# Grouped bar chart
summary = df.groupby("region")["converted"].mean().sort_values()
summary.plot(kind="bar", figsize=(7, 4), title="Conversion rate by region")
plt.ylabel("Conversion rate")
plt.tight_layout()
plt.show()

# Time-series line chart
revenue = df.groupby(pd.Grouper(key="order_date", freq="M"))["amount"].sum()
revenue.plot(figsize=(8, 4), title="Monthly revenue")
plt.ylabel("Revenue")
plt.tight_layout()
plt.show()

# Correlation heatmap concept with matplotlib
num = df.select_dtypes(include=np.number)
corr = num.corr(numeric_only=True)
fig, ax = plt.subplots(figsize=(8, 6))
im = ax.imshow(corr, vmin=-1, vmax=1, cmap="coolwarm")
ax.set_xticks(range(len(corr.columns)), labels=corr.columns, rotation=90)
ax.set_yticks(range(len(corr.columns)), labels=corr.columns)
fig.colorbar(im, ax=ax, label="Correlation")
plt.title("Numeric feature correlation")
plt.tight_layout()
plt.show()
```

## Model Diagnostic Visuals

```python
# Regression diagnostics: requires actual and predicted columns
diag = pd.DataFrame({"actual": y_test, "predicted": y_pred})
diag["residual"] = diag["actual"] - diag["predicted"]

plt.scatter(diag["predicted"], diag["residual"], alpha=0.3)
plt.axhline(0, color="black", linewidth=1)
plt.title("Residuals versus predicted")
plt.xlabel("Predicted")
plt.ylabel("Residual")
plt.tight_layout()
plt.show()

# Classification score distribution: requires y_test and predicted probabilities
scores = pd.DataFrame({"actual": y_test, "score": y_score})
scores.boxplot(column="score", by="actual")
plt.title("Predicted score by actual class")
plt.suptitle("")
plt.ylabel("Predicted score")
plt.tight_layout()
plt.show()
```

## House Style And Chart Quality

For stakeholder-facing charts, apply the house style before any plotting to replace matplotlib defaults (DejaVu Sans font, tab10 color cycle, box spines, dense grid):

```python
# At the top of the notebook or script
import matplotlib as mpl
# Paste HOUSE_RCPARAMS and CHART_COLORS from references/chart-style-system.md
mpl.rcParams.update(HOUSE_RCPARAMS)
```

See `references/chart-style-system.md` for the full rcParams dict, color palette constants, helper functions (`clean_axes`, `direct_label`, `annotate_event`, `save_chart`), and standard figure sizes.
See `references/design-craft-guide.md` for the craft principles: what makes a chart look AI-generated and how to fix it.

## Optional Library Notes

- seaborn can simplify boxplots, pairplots, heatmaps, and faceted charts — use `use_seaborn_house_style()` from `references/chart-style-system.md` to override seaborn defaults before plotting.
- plotly can help with interactive stakeholder exploration — use `PLOTLY_HOUSE_TEMPLATE` from `references/chart-style-system.md`.
- Keep matplotlib examples as the portable baseline when seaborn or plotly are unavailable.

## Caption Pattern

Use:

> Conversion rate is highest in [region], but [region] has only [n] records, so treat the difference as directional until validated.

Each caption should include the metric, population/time window, implication, and caveat.

## Validation And Quality Checks

- Confirm denominators before plotting rates.
- Check missing values dropped by plotting functions.
- Use consistent filters across related visuals.
- Sample large scatter plots to avoid overplotting.
- Label train/validation/test data separately in diagnostics.

## Common Mistakes

- Charts with no written takeaway.
- Percentages without counts.
- Correlation heatmap described causally.
- Too many categories in one bar chart.
- Incomplete recent periods plotted as real declines.
- Visualizing post-outcome features as if they were available predictors.

