# SQL Cohort Retention Analysis

## Use Case

Measure retention by cohort, such as signup month, first purchase month, subscription start month, or first active month.

## Expected Inputs

- User/customer table or event table.
- Cohort-defining event.
- Activity event that counts as retained.
- Time grain: week or month.

## Expected Outputs

- Cohort table.
- Period index since cohort start.
- Retention counts and rates.
- Retention matrix for visualization.

## Concise Workflow

1. Define cohort start per entity.
2. Define activity periods.
3. Join activity to cohorts.
4. Compute period number.
5. Aggregate retained users and divide by cohort size.
6. Interpret differences with acquisition/source mix and maturity in mind.

## Query Pattern

```sql
with cohorts as (
  select
    user_id,
    date_trunc('month', min(signup_date)) as cohort_month
  from dim_user
  group by user_id
),
activity as (
  select distinct
    user_id,
    date_trunc('month', event_time) as activity_month
  from fact_events
  where event_name in ('login', 'purchase', 'active_session')
),
cohort_activity as (
  select
    c.user_id,
    c.cohort_month,
    a.activity_month,
    (
      extract(year from a.activity_month) * 12 + extract(month from a.activity_month)
      - extract(year from c.cohort_month) * 12 - extract(month from c.cohort_month)
    ) as months_since_cohort
  from cohorts c
  join activity a
    on c.user_id = a.user_id
   and a.activity_month >= c.cohort_month
),
cohort_sizes as (
  select cohort_month, count(distinct user_id) as cohort_size
  from cohorts
  group by cohort_month
)
select
  ca.cohort_month,
  ca.months_since_cohort,
  cs.cohort_size,
  count(distinct ca.user_id) as retained_users,
  count(distinct ca.user_id) * 1.0 / nullif(cs.cohort_size, 0) as retention_rate
from cohort_activity ca
join cohort_sizes cs
  on ca.cohort_month = cs.cohort_month
group by ca.cohort_month, ca.months_since_cohort, cs.cohort_size
order by ca.cohort_month, ca.months_since_cohort;
```

Adapt date arithmetic to the database.

## Validation And Quality Checks

- Confirm cohort event is correct and not overwritten by later events.
- Confirm activity definition reflects meaningful retention.
- Use distinct users to avoid multiple events inflating retention.
- Check cohort sizes and exclude incomplete current periods where needed.
- Segment by acquisition source or plan when mix changes over time.

## Interpretation Notes

- Compare cohorts at the same age, not newest month at month 0 versus older month at month 12.
- Low retention may reflect acquisition quality, product changes, seasonality, or measurement changes.
- Retention rate needs cohort size shown alongside it.

## Common Mistakes To Avoid

- Counting events instead of retained users.
- Including activity before cohort start.
- Comparing incomplete recent periods to complete older periods.
- Changing retention definition mid-analysis.
- Ignoring reactivation rules.

