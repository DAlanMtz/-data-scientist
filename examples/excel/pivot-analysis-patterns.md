# Excel Pivot Analysis Patterns

## Use Case

Use Excel or Sheets pivot tables for stakeholder-facing summaries, quick EDA, segment comparisons, and dashboard-like analysis on smaller datasets.

## Expected Inputs

- Clean table with headers and one row per entity/event.
- Date field, segment fields, numeric measures, and optional target.
- Clear metric definitions.

## Expected Outputs

- Pivot tables for counts, sums, averages, rates, and segment comparisons.
- Pivot charts and slicers.
- Interpretation notes and quality checks.

## Concise Workflow

1. Convert data range to a table.
2. Validate grain and required fields.
3. Build pivots with clear rows, columns, filters, and values.
4. Add calculated fields/rates carefully.
5. Use slicers and charts for stakeholder review.
6. Reconcile totals to source data.

## Pivot Patterns

### Setup

- Excel: select data, use `Insert > Table`, then `Insert > PivotTable`.
- Sheets: use `Data > Pivot table`.
- Name the source table, such as `orders_clean`.
- Refresh pivots after source changes.

### Count By Segment

Rows:

- `region`
- `plan`

Values:

- Count of `customer_id`
- Sum of `revenue`
- Average of `revenue`

Interpretation:

- Always show counts next to averages so small segments are visible.

### Conversion Or Churn Rate

If target is 0/1:

Values:

- Average of `converted` gives conversion rate.
- Average of `churned` gives churn rate.

Format as percentage and include count of records.

### Time Grouping

Rows:

- `order_date`, grouped by month or quarter.

Columns:

- `region` or `channel`.

Values:

- Sum of `revenue`.
- Count of `order_id`.

Use line charts for time trends.

### Calculated Field Pattern

For revenue per order:

```text
revenue_per_order = revenue / orders
```

Prefer calculating ratios from aggregated numerator and denominator, not averaging row-level ratios unless that is the intended metric.

### Slicers

Use slicers for:

- Date range.
- Region.
- Product category.
- Customer segment.
- Channel.

Document default filter settings.

## Charting Patterns

- Use sorted bar charts for segment comparison.
- Use line charts for trends.
- Use stacked bars only for a few categories.
- Avoid pie charts for complex comparisons.
- Add data labels only when they improve readability.

## Validation And Quality Checks

- Reconcile pivot grand totals to source totals.
- Check filters and slicers before interpreting.
- Confirm blank categories are not hidden.
- Confirm grouped dates cover the expected period.
- Check denominator size for rates.
- Refresh pivot cache after data changes.

## Interpretation Notes

- Pivot tables are excellent for exploration and stakeholder discussion.
- They do not replace reproducible pipelines for recurring or high-risk reporting.
- Rates should always include denominators.
- Segment differences are descriptive unless causal design exists.

## Common Mistakes To Avoid

- Averaging percentages incorrectly.
- Forgetting active filters.
- Interpreting small segment rates as stable.
- Using calculated fields without checking numerator/denominator logic.
- Copying pivot outputs without preserving definitions.

