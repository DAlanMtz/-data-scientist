# Analytics Dashboard Template

Use this for general metric exploration, performance monitoring, and segment analysis. It should help users find what changed, where, and what to investigate next.

## Dashboard Purpose

- Business question:
- Decision cadence:
- Primary action supported:
- Out-of-scope decisions:

## Audience

- Primary users:
- Technical fluency:
- Expected usage: `[daily / weekly / monthly / ad hoc]`

## Decisions Supported

- Decide whether performance is on/off track.
- Identify segments, entities, or periods that need attention.
- Prioritize deeper analysis or operational follow-up.

## KPI Strip

| KPI | Definition | Current | Comparison | Target | Owner |
| --- | --- | ---: | ---: | ---: | --- |
| `[metric]` | `[formula/denominator]` | `[value]` | `[prior/target]` | `[target]` | `[owner]` |

Include delta badge, target/baseline, and data freshness.

## Trend Section

- Main trend metric:
- Frequency:
- Comparison period:
- Event annotations:
- Incomplete period handling:

Recommended visuals: line chart, small multiples, rolling average, target line.

## Segment Breakdown

- Primary segmentation:
- Secondary segmentation:
- Minimum sample threshold:

Recommended visuals: sorted bar/dot chart, heatmap, boxplot, ranked movers.

## Distribution / Relationship Section

Use only when it changes the analysis:

- Distribution of key metric:
- Relationship between two metrics:
- Outlier review:
- Candidate driver view:

Recommended visuals: histogram, boxplot, scatter/hexbin, correlation summary.

## Detail Table

Required columns:

- Entity/key
- Segment
- Primary metric
- Comparison metric
- Status/reason
- Last updated
- Suggested next action

## Filters

- Date range:
- Segment:
- Product/channel/region:
- Status:
- Metric selector, if needed:

## Data Freshness

- Latest source timestamp:
- Expected refresh:
- Stale-data threshold:
- Refresh failure behavior:

## Insight Cards

Use 1-3 cards:

- Key change:
- Driver or segment:
- Recommended follow-up:
- Caveat:

## QA Checks

- [ ] KPI totals reconcile to source.
- [ ] Filters apply consistently.
- [ ] Detail table reconciles to aggregate.
- [ ] Date range and freshness are visible.
- [ ] Charts have takeaway titles or nearby insight cards.
- [ ] No visual is included without a question.

## Recommended Implementation Options

- HTML/CSS or React/Tailwind: responsive grid, KPI cards, chart panels, detail table.
- Python Streamlit: metrics, tabs/columns, charts, filters, data table.
- R Shiny/flexdashboard: value boxes, plots, DT table, filters.
- Excel/Sheets: pivot charts, slicers, KPI cells, conditional formatting.
- Tableau/Power BI/BI tools: semantic model, measures, filters, drilldowns, row-level security.
