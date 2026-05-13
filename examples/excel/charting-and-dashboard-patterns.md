# Excel Charting And Dashboard Patterns

## Use Case

Use Excel or Google Sheets for smaller datasets, stakeholder-facing visuals, lightweight dashboards, scenario reviews, and quick operational summaries.

Excel/Sheets is appropriate when the data is small enough to inspect, refresh is controlled, and manual risk is acceptable. For recurring high-stakes reporting, prefer a governed dashboard or pipeline.

## Expected Inputs

- Clean source table with headers.
- Metric definitions and denominators.
- Date field, segment fields, and measures.
- Refresh process and owner.

## Expected Outputs

- Pivot charts and standard charts.
- KPI cards.
- Slicers/filters.
- Simple dashboard layout.
- Refresh and QA notes.

## Clean Source Table Setup

- Keep raw data on a separate protected sheet.
- Convert cleaned data into a named table.
- Use one row per entity/event/time period.
- Avoid merged cells in source data.
- Use consistent data types per column.
- Add a `last_refreshed` note on the dashboard.

## Pivot Charts

Use pivot charts for:

- Counts by segment.
- Revenue by month.
- Conversion/churn rate by group.
- Top products/customers/categories.

Rules:

- Always show denominators for rates.
- Refresh the pivot after source updates.
- Make active filters visible.

## Line Charts

Use for trends over time:

- Revenue by month.
- Orders by week.
- Forecast versus actual.
- Error or alert volume over time.

Avoid line charts for unordered categories.

## Bar And Column Charts

Use for comparisons:

- Segment size.
- Revenue by region.
- Missingness by field.
- Top categories.

Rules:

- Sort bars by value unless natural order matters.
- Use horizontal bars for long labels.
- Avoid too many categories.

## Scatter Plots

Use for numeric relationships:

- Spend versus tenure.
- Actual versus predicted.
- Price versus demand.

Rules:

- Add axis labels and units.
- Use transparency or sampling if overplotted.
- Do not imply causality from a scatter plot.

## Histograms

Use for distributions:

- Order amount.
- Customer tenure.
- Forecast error.
- Model scores.

Rules:

- Choose bins deliberately.
- Check spikes at zero and long tails.
- Consider boxplots for group comparisons.

## Combo Charts

Use sparingly:

- Revenue bars plus conversion-rate line.
- Actuals plus target line.

Rules:

- Avoid dual axes when possible.
- If using a secondary axis, label it clearly.
- Do not combine unrelated metrics just because they share time.

## Conditional Formatting

Use for:

- KPI thresholds.
- Data quality failures.
- Retention heatmaps.
- Missingness flags.
- Variance to target.

Rules:

- Use color scales with meaningful anchors.
- Avoid red/green-only palettes.
- Add labels so color is not the only signal.

## Slicers And Filters

Use for:

- Date range.
- Region.
- Product category.
- Customer segment.
- Channel.

Rules:

- Show selected filters on the dashboard.
- Document default filter settings.
- Check that charts share the intended slicers.

## Dashboard Layout

Recommended layout:

1. Header: title, owner, data source, last refreshed.
2. KPI cards: 3-6 decision-driving metrics.
3. Trend section: time-series charts.
4. Segment section: bars, pivots, or heatmaps.
5. Detail section: table for drilldown.
6. Quality note: data caveats and refresh status.

## KPI Cards

Each KPI should include:

- Current value.
- Prior period or target comparison.
- Unit.
- Time window.
- Directionality: good/bad/neutral.

Avoid KPI cards for vanity metrics that do not drive action.

## Refresh Process

Document:

- Data source.
- Refresh owner.
- Refresh frequency.
- Steps to refresh data, pivots, and charts.
- Control totals to reconcile.
- Known manual steps.

Use Power Query where possible for repeatable imports and transformations.

## Validation And Quality Checks

- Reconcile row count and totals to source.
- Confirm pivots are refreshed.
- Confirm filters and slicers are visible.
- Check formulas after inserting rows/columns.
- Validate rates use correct denominators.
- Check charts after data refresh for broken ranges.

## Interpretation Notes

- Dashboard visuals should support a recurring decision.
- Add short notes that explain what changed, why it matters, and what action is recommended.
- Use annotations for events, outages, launches, or definition changes.

## Common Spreadsheet Visualization Mistakes

- Editing raw data directly.
- Hidden filters change charts without warning.
- Pivot cache is stale.
- Chart ranges do not expand with new data.
- Percentages appear without denominators.
- Dual-axis combo charts mislead viewers.
- Conditional formatting exaggerates trivial differences.
- Manual copy-paste breaks reproducibility.

## Reproducibility Warnings

- Keep raw, cleaned, analysis, and dashboard sheets separate.
- Protect formulas and source tables.
- Log manual changes.
- Version shared workbooks.
- Promote recurring or high-risk dashboards into governed BI or pipeline workflows.

