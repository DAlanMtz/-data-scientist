# SQL Analytical Query Patterns

## Use Case

Build reproducible analytical tables for EDA, dashboards, funnels, rankings, rolling metrics, and cohort-style analysis. Syntax may vary by database.

## Expected Inputs

- Fact tables with timestamps and entity IDs.
- Dimension tables for attributes.
- Business definitions for metrics and filters.

## Expected Outputs

- Aggregated metric tables.
- Window-function outputs.
- Funnel/cohort/ranking summaries.
- Quality-aware query patterns.

## Concise Workflow

1. Define grain and filters.
2. Build base CTE with clean population.
3. Aggregate metrics.
4. Add windows/ranks/cohorts where needed.
5. Validate row counts and denominators.

## Query Patterns

### Group By Summary

```sql
select
  date_trunc('month', order_date) as order_month,
  region,
  count(*) as orders,
  count(distinct customer_id) as customers,
  sum(amount) as revenue,
  avg(amount) as avg_order_value
from fact_orders
where order_date >= date '2025-01-01'
group by 1, 2
order by 1, 2;
```

### Safe Join Pattern

```sql
with orders as (
  select order_id, customer_id, order_date, amount
  from fact_orders
),
customers as (
  select customer_id, region, segment
  from dim_customer
)
select o.*, c.region, c.segment
from orders o
left join customers c
  on o.customer_id = c.customer_id;
```

### Window Ranking

```sql
select
  customer_id,
  order_id,
  order_date,
  amount,
  row_number() over (partition by customer_id order by order_date) as order_number,
  rank() over (partition by customer_id order by amount desc) as amount_rank
from fact_orders;
```

### Rolling Metrics

```sql
select
  order_date,
  sum(amount) as daily_revenue,
  avg(sum(amount)) over (
    order by order_date
    rows between 6 preceding and current row
  ) as revenue_7d_avg
from fact_orders
group by order_date
order by order_date;
```

### Funnel Counts

```sql
with user_steps as (
  select
    user_id,
    max(case when event_name = 'viewed_product' then 1 else 0 end) as viewed,
    max(case when event_name = 'added_to_cart' then 1 else 0 end) as carted,
    max(case when event_name = 'purchased' then 1 else 0 end) as purchased
  from fact_events
  where event_time >= timestamp '2025-01-01'
  group by user_id
)
select
  count(*) as users,
  sum(viewed) as viewed,
  sum(carted) as carted,
  sum(purchased) as purchased,
  sum(purchased) * 1.0 / nullif(sum(viewed), 0) as purchase_per_view
from user_steps;
```

## Validation And Quality Checks

- Validate denominator definitions.
- Check row counts before and after joins.
- Use `left join` during QA to reveal missing dimensions.
- Review whether filters change the intended population.
- Use `nullif` to avoid divide-by-zero in ratios.

## Interpretation Notes

- Window functions preserve row grain while adding context.
- Funnel conversion depends heavily on time window and event definitions.
- Ranking ties should be handled deliberately.

## Common Mistakes To Avoid

- Mixing event grain and user grain in one metric.
- Using inner joins that silently drop records.
- Reporting rates without denominators.
- Building rolling windows without date completeness checks.
- Treating funnel steps as ordered when query only checks existence.

