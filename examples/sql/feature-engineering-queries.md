# SQL Feature Engineering Queries

## Use Case

Create leakage-safe tabular features in SQL for modeling, scoring, dashboards, or analysis.

## Expected Inputs

- Entity table or prediction points.
- Event/transaction/activity tables.
- Prediction timestamp and feature windows.
- Target timing and leakage constraints.

## Expected Outputs

- Entity-level feature table.
- Aggregates, ratios, flags, lags, and rolling-window features.
- Validation queries for feature coverage and leakage risk.

## Concise Workflow

1. Define prediction points.
2. Join only historical data before prediction timestamp.
3. Aggregate features over fixed lookback windows.
4. Create recency, frequency, monetary, ratios, and flags.
5. Validate feature coverage and nulls.

## Query Patterns

### Prediction Point Table

```sql
with prediction_points as (
  select
    customer_id,
    snapshot_date as prediction_date
  from customer_snapshots
  where snapshot_date = date '2025-03-01'
)
select * from prediction_points;
```

### Recency, Frequency, Monetary Features

```sql
with pp as (
  select customer_id, snapshot_date as prediction_date
  from customer_snapshots
),
orders as (
  select customer_id, order_date, amount
  from fact_orders
)
select
  pp.customer_id,
  pp.prediction_date,
  count(o.order_date) as orders_90d,
  sum(o.amount) as spend_90d,
  avg(o.amount) as avg_order_value_90d,
  max(o.order_date) as last_order_date,
  datediff(day, max(o.order_date), pp.prediction_date) as days_since_last_order
from pp
left join orders o
  on pp.customer_id = o.customer_id
 and o.order_date < pp.prediction_date
 and o.order_date >= pp.prediction_date - interval '90 day'
group by pp.customer_id, pp.prediction_date;
```

Adapt `datediff` and interval syntax to the database.

### Flags And Ratios

```sql
select
  customer_id,
  prediction_date,
  orders_90d,
  spend_90d,
  case when orders_90d > 0 then 1 else 0 end as active_90d,
  spend_90d / nullif(orders_90d, 0) as spend_per_order_90d,
  refunds_90d * 1.0 / nullif(orders_90d, 0) as refund_rate_90d
from customer_features_base;
```

### Lag Features

```sql
select
  customer_id,
  month,
  revenue,
  lag(revenue, 1) over (partition by customer_id order by month) as revenue_lag_1,
  lag(revenue, 3) over (partition by customer_id order by month) as revenue_lag_3
from customer_monthly_revenue;
```

### Rolling Window Features

```sql
select
  customer_id,
  month,
  revenue,
  avg(revenue) over (
    partition by customer_id
    order by month
    rows between 3 preceding and 1 preceding
  ) as avg_revenue_prior_3_months
from customer_monthly_revenue;
```

## Validation And Quality Checks

- Ensure all feature joins use `< prediction_date` or an equivalent cutoff.
- Check feature null rates and default logic.
- Verify row count equals prediction point count.
- Compare feature distributions between train and scoring populations.
- Confirm aggregate windows match business definitions.

## Interpretation Notes

- Recency/frequency/monetary features are usually strong and explainable.
- Ratios need denominator checks and often should keep denominator as a feature.
- Rolling windows should be trailing, not centered.

## Common Mistakes To Avoid

- Aggregating over the full customer lifetime when predicting at a historical point.
- Joining on target-period outcomes.
- Letting many-to-many joins inflate counts.
- Computing target encodings in SQL without fold logic.
- Filling all nulls with zero when null means unknown.

