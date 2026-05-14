# R Regression Example

## Use Case

Predict a numeric target and interpret model fit, residuals, and business error.

## Expected Inputs

- Data frame with numeric target.
- Feature list and prediction timing.
- Business meaning of error.

## Expected Outputs

- Baseline and regression model.
- RMSE, MAE, R-squared.
- Residual diagnostics.
- Coefficient or feature interpretation notes.

## Concise Workflow

1. Define target and units.
2. Split data.
3. Fit baseline and candidate regression.
4. Evaluate errors in business units.
5. Inspect residuals and influential points.

## Representative Pattern

```r
library(tidyverse)
library(caret)

set.seed(42)
idx <- createDataPartition(df$monthly_revenue, p = 0.8, list = FALSE)
train <- df[idx, ]
test <- df[-idx, ]

baseline_pred <- median(train$monthly_revenue, na.rm = TRUE)
base <- tibble(
  actual = test$monthly_revenue,
  predicted = baseline_pred
)

model <- lm(monthly_revenue ~ tenure_days + active_days_30d + plan + region, data = train)
pred <- predict(model, newdata = test)

results <- tibble(actual = test$monthly_revenue, predicted = pred) %>%
  mutate(residual = actual - predicted, abs_error = abs(residual))

metrics <- results %>%
  summarise(
    rmse = sqrt(mean(residual^2, na.rm = TRUE)),
    mae = mean(abs_error, na.rm = TRUE),
    r2 = cor(actual, predicted, use = "complete.obs")^2
  )
print(metrics)

summary(model)

ggplot(results, aes(predicted, residual)) +
  geom_point(alpha = 0.4) +
  geom_hline(yintercept = 0) +
  labs(title = "Residuals vs predicted")

results %>% arrange(desc(abs_error)) %>% head(20)
```

## Validation And Quality Checks

- Check target skew, outliers, and valid range.
- Use time/group splits when random split is invalid.
- Compare to median/mean baseline.
- Inspect residuals by segment and prediction range.
- Check assumptions before leaning on coefficient inference.

## Interpretation Notes

- Coefficients estimate association conditional on included variables.
- MAE is typical miss; RMSE emphasizes larger misses.
- Residual bias by segment can be more important than aggregate fit.

## Common Mistakes To Avoid

- Reporting R-squared as success without business error.
- Ignoring heteroscedastic residuals.
- Using `lm` coefficients causally without design support.
- Removing influential points without business review.

