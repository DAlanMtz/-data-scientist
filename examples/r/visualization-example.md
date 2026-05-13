# R Visualization Example

## Use Case

Use tidyverse and ggplot2 to create practical EDA, data quality, relationship, time-series, and model diagnostic visuals.

## Expected Inputs

- R data frame or tibble.
- Date column, segment columns, numeric metrics, and optional model outputs.
- Clear question for each chart.

## Expected Outputs

- Missingness and distribution visuals.
- Relationship and grouped comparison visuals.
- Time-series visuals.
- Model diagnostic visuals.
- Interpretation captions.

## Concise Workflow

1. Prepare chart-ready data with dplyr.
2. Use ggplot2 chart type matched to question.
3. Add clear labels, units, and time window.
4. Write caption that states the decision-relevant takeaway.
5. Validate denominators and filters.

## Representative Pattern

```r
library(tidyverse)
library(lubridate)

df <- df %>% mutate(order_date = ymd(order_date))

# Row count over time
df %>%
  count(month = floor_date(order_date, "month")) %>%
  ggplot(aes(month, n)) +
  geom_line() +
  labs(title = "Rows by month", x = "Month", y = "Rows")

# Missingness summary
missing <- df %>%
  summarise(across(everything(), ~ mean(is.na(.x)))) %>%
  pivot_longer(everything(), names_to = "column", values_to = "missing_rate") %>%
  arrange(missing_rate)

missing %>%
  slice_tail(n = 20) %>%
  ggplot(aes(missing_rate, reorder(column, missing_rate))) +
  geom_col() +
  labs(title = "Highest missingness rates", x = "Missing rate", y = NULL)

# Histogram
ggplot(df, aes(amount)) +
  geom_histogram(bins = 40) +
  labs(title = "Order amount distribution", x = "Order amount", y = "Orders")

# Boxplot by segment
ggplot(df, aes(region, amount)) +
  geom_boxplot() +
  labs(title = "Order amount by region", x = "Region", y = "Order amount")

# Scatter plot
df %>%
  slice_sample(n = min(nrow(df), 5000)) %>%
  ggplot(aes(tenure_days, amount)) +
  geom_point(alpha = 0.25) +
  labs(title = "Amount versus customer tenure", x = "Tenure days", y = "Order amount")

# Grouped bar chart
df %>%
  group_by(region) %>%
  summarise(conversion_rate = mean(converted, na.rm = TRUE), n = n(), .groups = "drop") %>%
  ggplot(aes(reorder(region, conversion_rate), conversion_rate)) +
  geom_col() +
  coord_flip() +
  labs(title = "Conversion rate by region", x = NULL, y = "Conversion rate")

# Time-series line chart
df %>%
  group_by(month = floor_date(order_date, "month")) %>%
  summarise(revenue = sum(amount, na.rm = TRUE), .groups = "drop") %>%
  ggplot(aes(month, revenue)) +
  geom_line() +
  labs(title = "Monthly revenue", x = "Month", y = "Revenue")
```

## Correlation Visualization Concept

```r
corr <- df %>%
  select(where(is.numeric)) %>%
  cor(use = "pairwise.complete.obs") %>%
  as.data.frame() %>%
  rownames_to_column("var1") %>%
  pivot_longer(-var1, names_to = "var2", values_to = "correlation")

ggplot(corr, aes(var1, var2, fill = correlation)) +
  geom_tile() +
  scale_fill_gradient2(limits = c(-1, 1)) +
  labs(title = "Numeric feature correlation", x = NULL, y = NULL) +
  theme(axis.text.x = element_text(angle = 90, hjust = 1))
```

## Model Diagnostic Visuals

```r
# Regression diagnostics
diag <- tibble(actual = y_test, predicted = y_pred) %>%
  mutate(residual = actual - predicted)

ggplot(diag, aes(predicted, residual)) +
  geom_point(alpha = 0.3) +
  geom_hline(yintercept = 0) +
  labs(title = "Residuals versus predicted", x = "Predicted", y = "Residual")

# Classification score distribution
score_df <- tibble(actual = factor(y_test), score = y_score)

ggplot(score_df, aes(actual, score)) +
  geom_boxplot() +
  labs(title = "Predicted score by actual class", x = "Actual class", y = "Predicted score")
```

## Caption Pattern

Use:

> Revenue rose after [event], but the chart is descriptive; confirm with a controlled design before attributing the increase to the event.

## Validation And Quality Checks

- Check active filters and row counts before plotting.
- Include denominators for rates.
- Use facets or small multiples instead of unreadable overplotting.
- Confirm recent periods are complete.
- Label train/test/model version in diagnostic charts.

## Common Mistakes

- Using default chart titles that name columns but not findings.
- Showing too many categories.
- Treating correlation as causation.
- Omitting units.
- Hiding small denominators.
- Dropping missing values without mentioning it.

