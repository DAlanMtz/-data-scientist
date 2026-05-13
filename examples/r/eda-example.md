# R EDA Example

## Use Case

Explore a dataset in R before modeling, reporting, or dashboarding.

## Expected Inputs

- CSV/database extract/data frame.
- Business objective, grain, date fields, and target if known.

## Expected Outputs

- Schema and missingness summary.
- Duplicate/key review.
- Descriptive stats and plots.
- Target readiness notes.

## Concise Workflow

1. Read data and inspect structure.
2. Check grain, keys, missingness, duplicates, and dates.
3. Summarize numeric and categorical fields.
4. Plot distributions and relationships.
5. Review target and leakage candidates.

## Representative Pattern

```r
library(tidyverse)
library(lubridate)

df <- readr::read_csv("data.csv") %>%
  mutate(created_at = ymd(created_at))

glimpse(df)
summary(df)

# Row count and key uniqueness
df %>% summarise(rows = n(), customers = n_distinct(customer_id))

# Missingness
missing <- df %>%
  summarise(across(everything(), ~ mean(is.na(.x)))) %>%
  pivot_longer(everything(), names_to = "column", values_to = "missing_rate") %>%
  arrange(desc(missing_rate))
print(missing)

# Duplicates
df %>% count(customer_id) %>% filter(n > 1) %>% arrange(desc(n))

# Date coverage
df %>% summarise(min_date = min(created_at, na.rm = TRUE),
                 max_date = max(created_at, na.rm = TRUE))

df %>%
  count(month = floor_date(created_at, "month")) %>%
  ggplot(aes(month, n)) +
  geom_line() +
  labs(title = "Rows by month")

# Target review
df %>%
  count(churned) %>%
  mutate(rate = n / sum(n))
```

## Validation And Quality Checks

- Confirm grain before summarizing.
- Check row counts before and after joins.
- Review missingness by time/source/segment.
- Verify target timing before feature suggestions.
- Keep raw data separate from cleaned data.

## Interpretation Notes

- Use `glimpse()` and summaries to find structural risks, not just describe columns.
- EDA findings should become decisions: fix data, engineer feature, change target, or pause modeling.
- Avoid causal language for observational patterns.

## Common Mistakes To Avoid

- Grouping at the wrong grain.
- Treating `NA`, zero, and "unknown" as the same.
- Dropping duplicates without understanding lifecycle records.
- Producing plots with no written implication.

