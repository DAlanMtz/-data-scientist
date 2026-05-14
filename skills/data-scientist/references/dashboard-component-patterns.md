# Dashboard Component Patterns

Use these components as reusable building blocks across BI tools, spreadsheets, notebooks, HTML/CSS, React, Streamlit, Shiny, and custom dashboards. Components should support decisions; do not add them only for visual polish.

## KPI Card

- **Purpose:** Show one primary metric status quickly.
- **Required inputs:** Metric value, unit, date range, comparison point, definition, freshness.
- **Best used when:** A user needs a first-screen health/status read.
- **Design rules:** Use short label, large value, comparison delta, target/baseline, and optional sparkline.
- **Interpretation rules:** Explain whether higher/lower is good and what threshold matters.
- **Common mistakes:** No denominator, no baseline, inconsistent date window, too many cards.

## Delta Badge

- **Purpose:** Show change vs prior period, target, forecast, or baseline.
- **Required inputs:** Current value, comparison value, direction semantics.
- **Best used when:** Change magnitude affects prioritization.
- **Design rules:** Use sign, magnitude, and semantic color/text. Pair color with words.
- **Interpretation rules:** State whether change is favorable, unfavorable, or neutral.
- **Common mistakes:** Showing percentage change on tiny baselines without context.

## Sparkline

- **Purpose:** Show compact trend context inside a KPI or table.
- **Required inputs:** Ordered time values with consistent frequency.
- **Best used when:** Direction matters more than precise readings.
- **Design rules:** Keep simple; avoid axes unless needed; mark latest point when useful.
- **Interpretation rules:** Use as context, not as sole evidence.
- **Common mistakes:** Hiding missing periods or volatile scale changes.

## Status Chip

- **Purpose:** Encode status such as On track, Warning, Critical, Draft, Approved, Stale.
- **Required inputs:** Status value and rule/threshold.
- **Best used when:** Users scan queues, QA states, or alert status.
- **Design rules:** Use stable labels and colors; include icon/text when color meaning matters.
- **Interpretation rules:** Define what each status means and what action follows.
- **Common mistakes:** Status labels without rules or owner.

## Data Freshness Badge

- **Purpose:** Make data currency visible.
- **Required inputs:** Latest data timestamp, expected refresh cadence, refresh status.
- **Best used when:** Decisions depend on current data.
- **Design rules:** Place in header; show "Last updated" and stale/warning state.
- **Interpretation rules:** State whether data is fresh enough for the dashboard cadence.
- **Common mistakes:** Hiding freshness in a tooltip or footer only.

## Filter Bar

- **Purpose:** Let users scope the dashboard to valid decision contexts.
- **Required inputs:** Filter fields, defaults, allowed values, and apply/reset behavior.
- **Best used when:** Users need repeated views by time, segment, owner, status, or version.
- **Design rules:** Put near top; show active filters; limit to meaningful controls.
- **Interpretation rules:** Filters must not silently change metric definitions.
- **Common mistakes:** Too many filters, unclear defaults, inconsistent cross-filter behavior.

## Metric Definition Tooltip

- **Purpose:** Provide denominator, source, grain, and formula without cluttering the dashboard.
- **Required inputs:** Metric name, formula, numerator, denominator, exclusions, owner.
- **Best used when:** Metrics are reused or business-critical.
- **Design rules:** Keep short; link to full glossary if needed.
- **Interpretation rules:** Tooltip should clarify, not hide essential caveats.
- **Common mistakes:** Definitions are missing, stale, or not aligned to source logic.

## Trend Chart Panel

- **Purpose:** Show movement over time.
- **Required inputs:** Date/time, metric value, frequency, comparison/target, completeness flag.
- **Best used when:** Cadence, seasonality, and trend direction matter.
- **Design rules:** Use line charts for continuous time; annotate important events; label incomplete periods.
- **Interpretation rules:** Mention trend, breakpoints, and caveats.
- **Common mistakes:** Uneven time intervals, hidden missing dates, truncated context.

## Segment Breakdown Panel

- **Purpose:** Show how a metric differs across groups.
- **Required inputs:** Segment, metric, denominator/count, time window.
- **Best used when:** Prioritization depends on where performance differs.
- **Design rules:** Use sorted bars/dots; show counts for rates; keep category colors stable.
- **Interpretation rules:** Distinguish large effects from small sample artifacts.
- **Common mistakes:** Comparing rates without denominators or too many categories.

## Cohort Heatmap

- **Purpose:** Show retention or repeat behavior across cohorts and periods.
- **Required inputs:** Cohort period, activity period index, cohort size, retention measure.
- **Best used when:** Lifecycle behavior and dropoff timing matter.
- **Design rules:** Put cohorts on rows, periods on columns, show cohort sizes, label incomplete cells.
- **Interpretation rules:** Compare mature cohorts carefully; disclose censoring.
- **Common mistakes:** Treating incomplete cohorts as underperforming.

## Funnel Chart

- **Purpose:** Show stepwise conversion and dropoff.
- **Required inputs:** Ordered steps, entity counts, conversion/dropoff rates.
- **Best used when:** A process has defined sequential stages.
- **Design rules:** Label counts and rates; show step definitions; consider bars over decorative funnels.
- **Interpretation rules:** Identify biggest actionable dropoff, not just lowest step.
- **Common mistakes:** Mixing unique users and events, non-sequential stages.

## Forecast Band Chart

- **Purpose:** Compare actuals to forecasts with uncertainty.
- **Required inputs:** Forecast generation date, horizon, actual, predicted, lower/upper interval.
- **Best used when:** Planning decisions depend on future uncertainty.
- **Design rules:** Show actual line, forecast line, interval band, and horizon.
- **Interpretation rules:** Discuss bias, interval coverage, and exceptions.
- **Common mistakes:** Forecasts without intervals or forecast timestamp.

## Confusion Matrix Panel

- **Purpose:** Show classification error types.
- **Required inputs:** Actual class, predicted class, threshold, sample size, date/model version.
- **Best used when:** False positives and false negatives have different costs.
- **Design rules:** Show counts and rates; label positive class; include threshold.
- **Interpretation rules:** Translate cells into business consequences.
- **Common mistakes:** Showing accuracy without error costs or class balance.

## Calibration Panel

- **Purpose:** Show whether predicted probabilities match observed outcomes.
- **Required inputs:** Predicted scores, observed labels, bins, sample counts.
- **Best used when:** Scores are used as probabilities or thresholds.
- **Design rules:** Reliability curve plus score distribution or bin table.
- **Interpretation rules:** State whether scores can be trusted as probabilities.
- **Common mistakes:** Calibrating on the test set or omitting sample sizes by bin.

## Error Analysis Table

- **Purpose:** Surface model failures for investigation.
- **Required inputs:** Entity, prediction, actual, error type/residual, segment, reason code.
- **Best used when:** Users need to diagnose failure patterns.
- **Design rules:** Sort by severity or impact; include filters by segment/time/error type.
- **Interpretation rules:** Categorize errors as label issue, data quality, missing signal, or model mismatch.
- **Common mistakes:** Listing errors without reason codes or next actions.

## Alert / Anomaly Table

- **Purpose:** Provide a triage queue for exceptions.
- **Required inputs:** Entity, timestamp, metric, expected value, observed value, anomaly score, severity, status, owner.
- **Best used when:** People must investigate alerts.
- **Design rules:** Include status chips, owner, age, reason, and recommended action.
- **Interpretation rules:** Separate high-severity anomalies from volume noise.
- **Common mistakes:** No false-positive feedback or escalation workflow.

## Ranked Detail Table

- **Purpose:** Show prioritized entities for action or investigation.
- **Required inputs:** Entity key, rank/score, metrics, reason, owner/status, last updated.
- **Best used when:** The dashboard drives queue work or targeted actions.
- **Design rules:** Sort by priority; keep action fields visible; allow export with filters.
- **Interpretation rules:** Explain why the top rows are top-ranked.
- **Common mistakes:** Too many columns, no stable key, no reason for ranking.

## Narrative Insight Card

- **Purpose:** Summarize the takeaway from a visual or metric group.
- **Required inputs:** Finding, evidence, caveat, implication.
- **Best used when:** Stakeholders need interpretation, not just data.
- **Design rules:** Keep to 2-4 short sentences or bullets; place near supporting visual.
- **Interpretation rules:** Use cautious language for observational findings.
- **Common mistakes:** Generic commentary that repeats chart labels.

## Recommendation / Action Card

- **Purpose:** Convert evidence into next action.
- **Required inputs:** Recommendation, owner, timing, expected impact, risk, measurement plan.
- **Best used when:** Dashboard supports operational or management decisions.
- **Design rules:** Make action and owner obvious; include status if tracked.
- **Interpretation rules:** Tie recommendation directly to metric evidence.
- **Common mistakes:** Recommendation lacks owner, threshold, or success measure.
