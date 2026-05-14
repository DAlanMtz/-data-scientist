# Dashboard QA Checklist Template

Use this as a pre-publish QA artifact for dashboards, BI reports, spreadsheet dashboards, notebook dashboards, or app-based analytics views.

## Dashboard Metadata

- Dashboard name:
- Environment/link:
- Owner:
- Reviewer:
- Review date:
- Data freshness at review:
- Version/status:

## Data Freshness Checks

- [ ] Refresh timestamp is visible to users.
- [ ] Latest data timestamp matches source system expectation.
- [ ] Scheduled refresh completed successfully.
- [ ] Partial refresh or stale source behavior is documented.
- [ ] Freshness lag is acceptable for the decision cadence.

## Metric Definition Checks

- [ ] Primary KPIs match approved definitions.
- [ ] Numerators and denominators are documented.
- [ ] Filters do not silently change metric meaning.
- [ ] Date windows are consistent across related metrics.
- [ ] Calculated fields reconcile to source or trusted reference.
- [ ] Units and currency are shown where needed.

## Filter Behavior

- [ ] Default filters match the intended user workflow.
- [ ] Active filters are visible.
- [ ] Reset behavior is clear.
- [ ] Multi-select behavior is tested.
- [ ] Empty filter states produce clear messages.
- [ ] Filters apply consistently across intended visuals.

## Aggregation And Grain Checks

- [ ] Dashboard grain is documented.
- [ ] Row-level tables reconcile to aggregate totals.
- [ ] Distinct counts are not double-counted across joins.
- [ ] Ratios are calculated from summed numerators/denominators where appropriate.
- [ ] Mixed grains are labeled and intentionally separated.

## Total / Subtotal Checks

- [ ] Totals match source-of-truth query or export.
- [ ] Subtotals reconcile to totals.
- [ ] Percentages sum as expected or explain why not.
- [ ] Weighted averages are not incorrectly averaged.

## Date Range Checks

- [ ] Default date range is correct.
- [ ] Date filters include/exclude boundaries correctly.
- [ ] Incomplete current periods are labeled or excluded.
- [ ] Time zones are handled consistently.
- [ ] Fiscal/calendar definitions are clear.

## Cross-Visual Consistency

- [ ] Same metric has same value across visuals for same filters.
- [ ] Category colors are consistent.
- [ ] Labels and names are consistent.
- [ ] Sorting rules are consistent or intentionally different.
- [ ] Drilldowns preserve context.

## Performance

- [ ] Initial load time is acceptable.
- [ ] Filter changes respond within expected limits.
- [ ] Heavy visuals or queries are optimized.
- [ ] Export/download operations complete reliably.

## Accessibility And Readability

- [ ] Text is readable at expected screen size.
- [ ] Color contrast is sufficient.
- [ ] Color is not the only status cue.
- [ ] Legends, axes, and labels are clear.
- [ ] Tooltips clarify definitions rather than hiding essential meaning.

## Mobile / Screen-Size Review

Use when the dashboard will be viewed on multiple screen sizes.

- [ ] Layout remains readable on expected devices.
- [ ] KPI cards do not wrap into confusing order.
- [ ] Filters remain usable.
- [ ] Tables are not the primary mobile interaction unless required.

## Permissions / Privacy

- [ ] Row-level/security rules work for each user group.
- [ ] Sensitive fields are hidden or masked.
- [ ] Export permissions are appropriate.
- [ ] Shared links do not bypass access controls.
- [ ] Privacy or compliance review is complete when required.

## Export / Share Behavior

- [ ] PDF/image export is readable.
- [ ] Exported tables preserve column names and filters.
- [ ] Shared views preserve intended filters.
- [ ] Snapshot/report subscriptions include refresh date.

## Stakeholder Signoff

| Reviewer | Role | Decision | Notes | Date |
| --- | --- | --- | --- | --- |
| `[name]` | `[role]` | `[approve / approve with conditions / reject]` | `[notes]` | `[date]` |

## Red Flags

- [ ] Dashboard shows stale data without warning.
- [ ] Primary KPI cannot be reconciled.
- [ ] Filters change denominators invisibly.
- [ ] Totals do not match detail rows.
- [ ] Sensitive data visible to unauthorized users.
- [ ] Users cannot identify what action to take.
- [ ] Dashboard has no named owner.

## QA Decision

- Publish decision: `[approve / approve with conditions / reject]`
- Blocking issues:
- Follow-up actions:
- Owner:
- Target date:

## Related References And Checklists

- `checklists/dashboard-qa-checklist.md`
- `references/visual-report-design-system.md`
- `templates/dashboard-design-brief-template.md`
