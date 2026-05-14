# Dashboard Layout Patterns

Use these layout patterns when designing analytics dashboards across BI tools, spreadsheets, notebooks, HTML/CSS, React, Streamlit, Shiny, or custom apps. Choose the pattern from the decision the dashboard supports, not from the chart type.

## Dashboard Layout Principles

- **Decision-first design:** Start with the decision, cadence, owner, and action path.
- **No chart dumps:** Every visual must answer a question, trigger action, or explain a risk.
- **Top-left / first-screen priority:** Put the most important answer, status, or exception first.
- **KPI strip before detail:** Show primary status before trends, breakdowns, and tables.
- **Overview before drilldown:** Let users understand current state before exploring details.
- **Consistent grid and spacing:** Reuse column widths, card sizes, chart styles, labels, and colors.
- **Freshness and date range visible:** Users must know what period and data version they are seeing.
- **Accessible colors and labels:** Use color as emphasis, not the only meaning carrier.
- **Responsive and export-aware:** Test expected screen sizes, print/PDF output, and shared screenshots.

## Executive KPI Overview

### When To Use
Leadership needs a fast status read across a small set of strategic metrics.

### Primary Decision Supported
Whether performance is on track, which risks need attention, and what action should be prioritized.

### Required Data Shape
Metric table with current period, comparison period, target/baseline, owner, status, and optional driver fields.

### Recommended Page Structure
1. Header with date range, freshness, and scope.
2. KPI strip with 4-8 primary metrics.
3. Status vs target summary.
4. Top drivers, risks, or opportunities.
5. Recommended actions and caveats.

### Recommended Chart/Card Types
KPI cards, delta badges, sparklines, ranked bars, compact trend panels, narrative insight cards.

### Filters/Slicers
Keep minimal: date range, business unit/region/product if leadership uses those views.

### Common Mistakes
- Too many KPIs.
- No target or baseline.
- Visuals require deep interpretation.
- Filters let executives accidentally change the story.

### Quality Checks
- Each KPI has definition, denominator, target/baseline, and owner.
- First screen answers "are we on track?"
- Caveats are visible when they affect action.

## Analytics Overview

### When To Use
Analysts or business partners need to explore performance, segments, and drivers.

### Primary Decision Supported
Where to investigate, optimize, or allocate follow-up analysis.

### Required Data Shape
Fact table or aggregate table with date, entity/segment dimensions, metrics, and optional target/outcome.

### Recommended Page Structure
1. KPI strip.
2. Trend panel.
3. Segment breakdown.
4. Distribution or relationship view.
5. Ranked detail table.
6. Insight/recommendation cards.

### Recommended Chart/Card Types
KPI cards, time-series lines, sorted bars, boxplots, scatter plots, heatmaps, ranked tables.

### Filters/Slicers
Date range, segment, geography, product, channel, cohort, status.

### Common Mistakes
- Too many filter combinations.
- Metric definitions differ across sections.
- Detail table becomes the main dashboard.

### Quality Checks
- KPI totals reconcile to detail.
- Filters apply consistently.
- Trends and breakdowns share date and denominator logic.

## Trend + Breakdown

### When To Use
Users need to understand how a metric changes over time and where the change is concentrated.

### Primary Decision Supported
Whether to respond to a trend and which segment needs attention.

### Required Data Shape
Time series by segment/entity with metric, count/denominator, and optional target.

### Recommended Page Structure
1. KPI with current value and change.
2. Main trend line.
3. Segment contribution or breakdown.
4. Detail table for top movers.

### Recommended Chart/Card Types
Line chart, small multiples, stacked/clustered bars, contribution table, ranked movers table.

### Filters/Slicers
Date range, segment, metric selector, comparison period.

### Common Mistakes
- Hiding incomplete recent periods.
- Showing percentages without volume.
- Using stacked areas that obscure segment movement.

### Quality Checks
- Time granularity is clear.
- Incomplete periods are labeled.
- Top movers reconcile to total change.

## Funnel / Conversion

### When To Use
Users need to monitor stepwise progression, conversion, leakage, or dropoff.

### Primary Decision Supported
Which step or segment should be improved first.

### Required Data Shape
Entity-level events or step counts by stage, time, and segment.

### Recommended Page Structure
1. Overall conversion KPI.
2. Funnel by step.
3. Dropoff trend by step.
4. Segment comparison.
5. Detail or cohort table.

### Recommended Chart/Card Types
Funnel chart, step conversion bars, trend lines, heatmap by segment and stage.

### Filters/Slicers
Cohort date, source/channel, segment, device/platform, product.

### Common Mistakes
- Mixing event counts and unique entity counts.
- Using steps that are not sequential.
- Omitting cohort definition.

### Quality Checks
- Step definitions are documented.
- Each stage uses consistent entity counting.
- Dropoff percentages include denominators.

## Cohort / Retention

### When To Use
Users need to understand repeat behavior, retention, churn, lifecycle, or adoption over time.

### Primary Decision Supported
Which cohorts or segments need intervention and when dropoff happens.

### Required Data Shape
Entity, cohort period, activity period, retention indicator/count, segment, and cohort size.

### Recommended Page Structure
1. Cohort definition and freshness.
2. Retention heatmap.
3. Cohort size and quality indicators.
4. Retention curve by segment.
5. Dropoff/action section.

### Recommended Chart/Card Types
Cohort heatmap, line curves, cohort-size bars, lifecycle stage cards.

### Filters/Slicers
Cohort date, segment, channel, product, lifecycle stage.

### Common Mistakes
- Comparing incomplete cohorts to mature cohorts.
- Hiding small cohort sizes.
- Changing retention definitions across views.

### Quality Checks
- Incomplete/censored cohorts are labeled.
- Cohort sizes are visible.
- Retention denominator is consistent.

## Forecast Actuals Vs Predicted

### When To Use
Users need to compare actual outcomes to forecasts and act on forecast errors.

### Primary Decision Supported
Whether forecast quality is sufficient for planning and where exceptions require action.

### Required Data Shape
Time, entity/segment, actual value, forecast value, forecast timestamp, horizon, interval bounds, and error.

### Recommended Page Structure
1. Forecast horizon and freshness.
2. Actual vs forecast with prediction interval.
3. Error metrics and bias.
4. Error by horizon/segment.
5. Exception queue and actions.

### Recommended Chart/Card Types
Forecast band chart, error trend, bias chart, ranked exception table, segment small multiples.

### Filters/Slicers
Date range, horizon, segment, product/location, model/version.

### Common Mistakes
- Comparing forecasts generated after actuals were known.
- Omitting prediction intervals.
- Reporting only average error while bias is systematic.

### Quality Checks
- Forecast generation timestamp is preserved.
- Metrics are horizon-aware.
- Exceptions are tied to action thresholds.

## Model Performance And Monitoring

### When To Use
A predictive model influences recurring decisions and needs monitoring.

### Primary Decision Supported
Whether the model remains fit for use, needs threshold review, retraining, rollback, or investigation.

### Required Data Shape
Prediction log with model version, timestamp, features/segments, scores, decisions, labels when available, and monitoring metrics.

### Recommended Page Structure
1. Model/version metadata and freshness.
2. Prediction volume and score distribution.
3. Performance metrics where labels are available.
4. Calibration and threshold outcomes.
5. Drift and segment performance.
6. Alerts, rollback/retraining notes.

### Recommended Chart/Card Types
KPI cards, calibration plot, confusion matrix, PR/ROC summary, drift panels, error tables.

### Filters/Slicers
Model version, date range, segment, threshold, label availability.

### Common Mistakes
- Monitoring only uptime.
- Mixing model versions without labels.
- Ignoring delayed labels.

### Quality Checks
- Label delay is documented.
- Alerts have owners and thresholds.
- Metrics are separated by model version.

## Anomaly / Exception Monitoring

### When To Use
Users need to triage anomalies, incidents, fraud signals, data quality issues, or operational exceptions.

### Primary Decision Supported
Which exceptions require investigation, escalation, or dismissal.

### Required Data Shape
Entity, timestamp, metric, expected value/baseline, observed value, anomaly score, severity, reason, status, owner.

### Recommended Page Structure
1. Alert volume and severity.
2. Trend of anomalies over time.
3. Top affected entities/segments.
4. Investigation queue.
5. False-positive review and escalation rules.

### Recommended Chart/Card Types
Status KPIs, alert trend, ranked bars, anomaly table, reason-code distribution.

### Filters/Slicers
Severity, status, owner, date range, segment, reason code.

### Common Mistakes
- No status workflow.
- Alert fatigue from poor thresholds.
- No false-positive feedback loop.

### Quality Checks
- Severity rules are documented.
- Queue has owner/status/timestamp.
- False positives are reviewed and fed back.

## Operational Queue

### When To Use
Users need to take action on ranked entities, tasks, risks, or opportunities.

### Primary Decision Supported
Which item to handle next and why.

### Required Data Shape
Entity-level table with score/priority, reason, status, owner, timestamp, recommended action, and outcome.

### Recommended Page Structure
1. Queue status KPIs.
2. Filter bar for status/owner/priority.
3. Ranked table.
4. Detail panel.
5. Action outcome tracking.

### Recommended Chart/Card Types
KPI cards, ranked detail table, status chips, reason-code bars, action cards.

### Filters/Slicers
Status, owner, priority, date, segment, reason.

### Common Mistakes
- Ranking has no explanation.
- Users cannot mark disposition.
- Table lacks fields needed for action.

### Quality Checks
- Each row has owner, priority, reason, and next action.
- Status workflow is clear.
- Outcomes can be captured for learning.

## Drilldown / Detail Explorer

### When To Use
Users need controlled exploration after an overview, especially for analysts or operators.

### Primary Decision Supported
Investigate why a metric changed or which entities explain a pattern.

### Required Data Shape
Aggregate metrics plus row/detail records with stable keys and drilldown dimensions.

### Recommended Page Structure
1. Context header with active filters.
2. Summary cards.
3. Breakdown panels.
4. Detail table with export.
5. Definitions and caveats.

### Recommended Chart/Card Types
Filter bar, breakdown charts, ranked tables, detail table, metric definition tooltips.

### Filters/Slicers
All validated dimensions needed by users; avoid exposing fields that create invalid comparisons.

### Common Mistakes
- Drilldown breaks metric reconciliation.
- Users can filter into meaningless samples.
- Export omits active filters or definitions.

### Quality Checks
- Detail rows reconcile to aggregates.
- Active filters and grain are visible.
- Export preserves definitions and filters.
