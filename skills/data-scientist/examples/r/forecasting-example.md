# R Forecasting Example

## Use Case

Forecast a regular time series with baseline and simple smoothing-style methods.

## Expected Inputs

- Date column and numeric target.
- Forecast frequency and horizon.
- Business context for over/under forecast cost.

## Expected Outputs

- Time-index checks.
- Naive or moving average baseline.
- Simple forecast comparison.
- Error metrics and bias.
- Monitoring notes.

## Concise Workflow

1. Aggregate to the decision frequency.
2. Check missing periods and seasonality.
3. Create train/test split by time.
4. Fit naive and simple smoothing methods.
5. Compare forecast errors.
6. Communicate uncertainty and drift risks.

## Representative Pattern

```r
library(tidyverse)
library(lubridate)
library(forecast)

daily <- df %>%
  mutate(date = ymd(date)) %>%
  group_by(date) %>%
  summarise(orders = sum(orders), .groups = "drop") %>%
  arrange(date)

full_dates <- tibble(date = seq(min(daily$date), max(daily$date), by = "day"))
daily <- full_dates %>%
  left_join(daily, by = "date") %>%
  mutate(orders = replace_na(orders, 0)) # only if missing means true zero

h <- 30
train <- head(daily$orders, -h)
test <- tail(daily$orders, h)

train_ts <- ts(train, frequency = 7)

naive_fc <- snaive(train_ts, h = h)
ets_fc <- ets(train_ts) %>% forecast(h = h)

accuracy(naive_fc, test)
accuracy(ets_fc, test)

autoplot(ets_fc) +
  autolayer(ts(test, start = length(train) + 1, frequency = 7), series = "Actual")
```

## Validation And Quality Checks

- Do not use random splits.
- Confirm missing periods are not outages or missing data before filling.
- Compare to naive/seasonal naive.
- Use rolling-origin validation for final claims.
- Report horizon-specific error when horizon varies.

## Interpretation Notes

- Forecasts are planning estimates, not guarantees.
- Bias matters when systematic over/under planning is costly.
- Prediction intervals should guide risk-sensitive planning.

## Common Mistakes To Avoid

- Treating all missing periods as zero.
- Ignoring holidays/promotions/outages.
- Reporting MAPE with zeros.
- Comparing models on one lucky holdout window only.

