# Dashboard QA Checklist

Use this checklist before publishing, revising, or certifying a dashboard. It applies across BI tools, spreadsheet dashboards, notebooks, web apps, and custom internal tools.

## Data Freshness And Refresh

- [ ] Refresh timestamp is visible.
- [ ] Source data freshness matches the dashboard claim.
- [ ] Scheduled refresh has succeeded.
- [ ] Failed refresh behavior is visible or documented.
- [ ] Refresh cadence matches the decision cadence.

**Red flag:** Users cannot tell whether the dashboard is current.

## Metric Definitions

- [ ] Primary KPIs have approved definitions.
- [ ] Numerators, denominators, exclusions, and units are documented.
- [ ] Calculated metrics reconcile to source queries or trusted extracts.
- [ ] Date windows are consistent across related visuals.
- [ ] Targets, thresholds, and baselines are documented.

**Minimum acceptable standard:** Every primary KPI can be reproduced from source data.

## Filters And Slicers

- [ ] Default filters match the intended user workflow.
- [ ] Active filters are visible.
- [ ] Filters apply consistently across intended visuals.
- [ ] Reset behavior is clear.
- [ ] Empty states are understandable.
- [ ] Filters do not silently change metric definitions.

## Drilldowns

- [ ] Drilldowns answer a user workflow question.
- [ ] Drilldowns preserve selected context.
- [ ] Detail rows reconcile to aggregate values.
- [ ] Detail tables include only useful action fields.
- [ ] Exported drilldowns preserve filters and definitions.

## Row-Level Security / Privacy

- [ ] User groups have appropriate access.
- [ ] Row-level/security rules are tested.
- [ ] Sensitive fields are hidden, masked, or justified.
- [ ] Shared links do not bypass permissions.
- [ ] Export permissions match privacy requirements.

**Critical red flag:** Unauthorized users can view sensitive or restricted rows.

## Aggregation And Grain

- [ ] Primary grain is documented.
- [ ] Mixed grains are separated or clearly labeled.
- [ ] Distinct counts are not duplicated by joins.
- [ ] Totals/subtotals reconcile.
- [ ] Weighted averages and ratios are calculated correctly.
- [ ] Incomplete current periods are labeled or excluded.

## Cross-Visual Consistency

- [ ] Same metric returns same value across visuals under same filters.
- [ ] Category labels are consistent.
- [ ] Category colors are consistent.
- [ ] Sorting logic is stable.
- [ ] Tooltip definitions match visible labels.

## Performance

- [ ] Initial load time is acceptable for the audience.
- [ ] Filter interactions are responsive.
- [ ] Heavy queries are optimized or pre-aggregated.
- [ ] Large tables are paginated, filtered, or moved to export.
- [ ] Dashboard failure modes are understandable.

## Visual Design And Readability

- [ ] Most important information appears first.
- [ ] Dashboard does not overload users with chart dumps.
- [ ] Layout uses consistent groups, spacing, and labels.
- [ ] Captions or titles state takeaways where possible.
- [ ] Color is simple, consistent, and accessible.
- [ ] Mobile or screen-size behavior is reviewed when relevant.

## Stakeholder Acceptance

- [ ] Decision owner has reviewed the dashboard.
- [ ] Data owner has confirmed metric definitions.
- [ ] Users understand what actions the dashboard supports.
- [ ] Known limitations are documented.
- [ ] Open issues have severity, owner, and due date.

## Maintenance Ownership

- [ ] Business owner is named.
- [ ] Technical owner is named.
- [ ] Data owner is named.
- [ ] Review cadence is defined.
- [ ] Change request process is defined.
- [ ] Deprecation or replacement plan exists if the dashboard is temporary.

## Publish Decision

- [ ] Approve.
- [ ] Approve with conditions.
- [ ] Reject until blocking issues are fixed.

## Related Files

- `references/design-craft-guide.md` — craft principles and dashboard anti-patterns; apply before publishing
- `references/chart-style-system.md` — house palette and chart style; apply to embedded charts
- `references/visual-report-design-system.md` — design token reference (hex values, type scale, spacing, palette)
- `references/visual-storytelling-guide.md` — dashboard vs report storytelling; narrative decisions
- `references/dashboard-layout-patterns.md` — layout archetypes by decision type
- `references/dashboard-component-patterns.md` — KPI card, filter, trend, cohort, and table component patterns
- `templates/dashboard-design-brief-template.md` — design brief before building
- `templates/dashboard-qa-checklist-template.md` — QA template for structured review
