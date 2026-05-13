# SQL Data Quality Checks

## Use Case

Audit source tables, analytical extracts, feature tables, or dashboard inputs with portable SQL patterns. Syntax varies by database, so adapt date functions and percentile functions as needed.

## Expected Inputs

- Table name and expected grain.
- Primary key or composite key.
- Required columns, valid ranges, freshness SLA, allowed categories.
- Reference/dimension tables for integrity checks.

## Expected Outputs

- Row counts, freshness, missingness, duplicate checks.
- Range/category/integrity violations.
- Data quality issue table for reporting.

## Concise Workflow

1. Check row count and date coverage.
2. Validate required fields and keys.
3. Measure missingness and duplicates.
4. Check ranges, categories, and referential integrity.
5. Report severity and affected rows.

## Query Patterns

### Row Counts And Freshness

```sql
select
  count(*) as row_count,
  min(event_date) as min_event_date,
  max(event_date) as max_event_date,
  max(updated_at) as last_updated_at
from fact_events;
```

### Missingness

```sql
select
  count(*) as rows,
  sum(case when customer_id is null then 1 else 0 end) as missing_customer_id,
  avg(case when customer_id is null then 1.0 else 0.0 end) as missing_customer_id_rate,
  sum(case when amount is null then 1 else 0 end) as missing_amount
from fact_orders;
```

### Duplicate Keys

```sql
select order_id, count(*) as n
from fact_orders
group by order_id
having count(*) > 1
order by n desc;
```

### Valid Ranges

```sql
select *
from fact_orders
where amount < 0
   or discount_rate < 0
   or discount_rate > 1
   or order_date > current_date;
```

### Category Consistency

```sql
select status, count(*) as n
from fact_orders
group by status
order by n desc;
```

```sql
select status, count(*) as n
from fact_orders
where status not in ('created', 'paid', 'shipped', 'cancelled', 'returned')
group by status;
```

### Referential Integrity

```sql
select
  count(*) as orders,
  sum(case when c.customer_id is null then 1 else 0 end) as missing_customer_dim
from fact_orders o
left join dim_customer c
  on o.customer_id = c.customer_id;
```

### Join Row Count Reconciliation

```sql
with before_join as (
  select count(*) as n from fact_orders
),
after_join as (
  select count(*) as n
  from fact_orders o
  left join dim_customer c
    on o.customer_id = c.customer_id
)
select
  before_join.n as rows_before,
  after_join.n as rows_after,
  after_join.n - before_join.n as row_delta
from before_join cross join after_join;
```

## Validation And Quality Checks

- Run checks by source, date partition, and core segment when possible.
- Confirm missing periods are not silently hidden by filters.
- Treat row multiplication after joins as a serious issue.
- Turn critical checks into scheduled tests for production inputs.

## Interpretation Notes

- A failed check should state affected rows, impact, and owner.
- Unexpected categories may be legitimate product changes or upstream defects.
- Freshness failures can invalidate otherwise correct dashboards or scores.

## Common Mistakes To Avoid

- Checking only total row count.
- Ignoring grain and duplicate keys.
- Using inner joins that hide missing reference data.
- Treating null, blank, zero, and unknown as equivalent.
- Not tracking check results over time.

