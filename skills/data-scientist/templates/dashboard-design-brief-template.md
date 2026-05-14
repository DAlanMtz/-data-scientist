# Dashboard Design Brief Template

Use this template before building or redesigning a dashboard. A dashboard is not a chart collection. It is an operating surface for repeated decisions.

## Dashboard Name

- Name:
- Owner:
- Status: `[Draft / reviewed / approved / active]`
- Last updated:

## Audience / Users

| User group | Primary questions | Decisions/actions | Cadence |
| --- | --- | --- | --- |
| `[group]` | `[questions]` | `[actions]` | `[daily/weekly/monthly]` |

## Decisions Supported

- Primary decision:
- Secondary decisions:
- Decisions explicitly not supported:
- Escalation or handoff actions:

## Primary KPIs

| KPI | Definition | Grain | Target/baseline | Refresh | Owner |
| --- | --- | --- | --- | --- | --- |
| `[metric]` | `[definition]` | `[grain]` | `[target]` | `[cadence]` | `[owner]` |

Primary KPIs must appear first and use consistent date windows.

## Secondary Metrics

- Diagnostic metrics:
- Segment metrics:
- Data quality metrics:
- Model or pipeline health metrics, if relevant:

## Data Sources

| Source | Table/file/API | Grain | Refresh cadence | Known quality dependency |
| --- | --- | --- | --- | --- |
| `[source]` | `[location]` | `[grain]` | `[cadence]` | `[dependency]` |

## Grain

- Primary dashboard grain:
- Supported rollups:
- Unsupported rollups:
- Entity keys:
- Date/time fields:

## Refresh Cadence

- Expected refresh frequency:
- Data freshness indicator location:
- Manual refresh process, if any:
- Failure behavior:

## Filters / Slicers

| Filter | Default | Allowed values | Required? | Notes |
| --- | --- | --- | --- | --- |
| `[filter]` | `[default]` | `[values]` | `[yes/no]` | `[notes]` |

Rules:

- Filters must not silently change metric definitions.
- Defaults should match the most common decision workflow.
- Show active filters clearly.

## User Workflows

For each major workflow:

1. User opens dashboard to answer:
2. They check:
3. They drill into:
4. They take action:
5. They export/share:

## Page / Layout Plan

### Page 1: `[Overview / operating view]`

- Header: purpose, refresh status, active filters.
- KPI strip: primary KPIs with target/baseline.
- Main decision visual:
- Supporting segment/trend view:
- Detail or action table:

### Page 2: `[Diagnostics / drilldown / monitoring]`

- Diagnostic purpose:
- Visuals:
- Tables:
- Alerts:

## Visual Hierarchy

- Most important metric:
- Most important chart:
- Default reading path:
- Items that should be visually muted:
- Items that require alert styling:

## Drill-Down Needs

- Required drilldowns:
- Fields users need in detail tables:
- Export requirements:
- Row-level access restrictions:

## Alerts / Thresholds

| Metric | Threshold | Status meaning | Action | Owner |
| --- | --- | --- | --- | --- |
| `[metric]` | `[threshold]` | `[meaning]` | `[action]` | `[owner]` |

## Access / Privacy

- Audience access level:
- Sensitive fields:
- Row-level/security rules:
- Export restrictions:
- Privacy review needed:

## Data Quality Dependencies

- Required fields:
- Freshness requirement:
- Join/key integrity requirement:
- Known upstream risks:
- Data quality checks displayed in dashboard:

## Success Criteria

- Adoption/usage measure:
- Decision quality measure:
- Operational outcome:
- Reduction in manual work:
- Stakeholder acceptance criteria:

## Maintenance Owner

- Business owner:
- Data owner:
- Technical owner:
- Review cadence:
- Change request process:

## Common Mistakes To Avoid

- Building before defining decisions and users.
- Showing too many pages or filters.
- Using inconsistent metric definitions across visuals.
- Hiding data freshness and active filters.
- Mixing grains without clear labels.
- Designing for executives and operators in the same overloaded view.
- Adding drilldowns that do not support action.

## Related References And Checklists

- `references/visual-report-design-system.md`
- `references/visual-storytelling-guide.md`
- `templates/dashboard-qa-checklist-template.md`
- `checklists/dashboard-qa-checklist.md`
