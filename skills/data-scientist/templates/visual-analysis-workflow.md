# Visual Analysis Workflow

Use this workflow when the task needs visual data analysis, visual model diagnostics, dashboard planning, or stakeholder-facing visual storytelling.

## Required Inputs

- Business question or decision.
- Dataset, data dictionary, and grain.
- Target variable or outcome, if relevant.
- Key segments, time fields, and metrics.
- Audience: analyst, executive, operator, client, or technical reviewer.
- Delivery format: notebook, report, dashboard, slide, spreadsheet, BI tool, or app.

## Expected Outputs

- Focused set of visuals tied to questions.
- Data quality and diagnostic visuals.
- Stakeholder-ready charts with captions and takeaways.
- Dashboard or report visual plan, if recurring.
- Notes on limitations, uncertainty, and misleading-chart risks.

## Deliverable Routing

- Exploratory visuals -> EDA Summary (`templates/eda-notebook-template.md` or `templates/analysis-report-template.md`).
- Stakeholder narrative -> Visual Report (`templates/visual-report-template.md`).
- Polished PDF/web output -> HTML Report (`templates/html-report-template.md`).
- Dashboard planning -> Dashboard Design Brief (`templates/dashboard-design-brief-template.md`).
- Dashboard validation -> Dashboard QA Checklist (`templates/dashboard-qa-checklist-template.md` and `checklists/dashboard-qa-checklist.md`).

Use `references/visual-report-design-system.md` for stakeholder-facing design standards and `references/visual-storytelling-guide.md` for visual narrative structure.

## Visual Analysis Objectives

- [ ] Identify data quality problems.
- [ ] Understand distributions and outliers.
- [ ] Compare groups or segments.
- [ ] Show relationships and possible predictors.
- [ ] Show time trends, seasonality, and breaks.
- [ ] Diagnose model behavior and failure modes.
- [ ] Communicate decisions, tradeoffs, and uncertainty.

Do not make charts because the data exists. Make charts because a question needs answering.

## Chart Selection By Question Type

| Question | Recommended visuals |
| --- | --- |
| How complete is the data? | Missingness bar, missingness heatmap, row count by date/source |
| What is the distribution? | Histogram, density, ECDF, boxplot |
| Are there outliers? | Boxplot, scatter, sorted values, residual plot |
| How do groups compare? | Sorted bar, dot plot, boxplot, grouped summary with intervals |
| How do two numeric fields relate? | Scatter, hexbin, fitted line, residual view |
| How does something change over time? | Line chart, small multiples, annotated trend |
| What explains model errors? | Confusion matrix, residuals, calibration, error by segment |
| What should stakeholders do? | Ranked bar, threshold tradeoff, forecast interval, KPI plus trend |

## Step-By-Step Workflow

### 1. Define The Visual Question

- Write the question above the chart before building it.
- Identify the metric, denominator, population, and time window.
- Decide whether the chart is exploratory, diagnostic, or communicative.

### 2. Build Data Quality Visuals

Use:

- Row count by date/source.
- Missingness rate by column.
- Missingness by time or segment.
- Duplicate count by key.
- Range violation count by field.
- Category frequency chart for unexpected values.

Interpretation should end with: fix, exclude, monitor, or document.

### 3. Build Distribution Visuals

Use:

- Histograms for numeric shape.
- ECDFs for distribution comparison.
- Boxplots for outlier and group comparison.
- Bar charts for categorical frequencies.

Check spikes at zero, long tails, impossible values, and business thresholds.

### 4. Build Relationship Visuals

Use:

- Scatter or hexbin for numeric pairs.
- Boxplots or grouped summaries for category versus numeric.
- Stacked or grouped bars for category versus category.
- Correlation heatmap for numeric screening.

Avoid implying causality from relationship visuals.

### 5. Build Time-Series Visuals

Use:

- Line chart for trend.
- Small multiples for many series.
- Rolling average plus raw values for noisy series.
- Event annotations for launches, campaigns, outages, and policy changes.
- Forecast intervals when showing predictions.

Do not hide missing periods or incomplete recent periods.

### 6. Build Segmentation Visuals

Use:

- Segment profile heatmap.
- Sorted bar charts of segment size and value.
- Boxplots by segment.
- Small multiples by segment.
- PCA/UMAP/t-SNE views only as exploratory aids.

Name segments after profiling, not before.

### 7. Build Model Diagnostic Visuals

Regression:

- Actual versus predicted.
- Residuals versus fitted.
- Residual distribution.
- Error by segment/time.

Classification:

- Confusion matrix.
- ROC and PR curves.
- Calibration curve.
- Score distribution by class.
- Threshold tradeoff chart.

Forecasting:

- Actual versus forecast.
- Backtest windows.
- Error by horizon.
- Interval coverage.

Clustering/recommendation/anomaly:

- Cluster profiles and silhouette.
- Ranking metrics at `k`.
- Alert volume and reason-code distributions.

### 8. Plan Stakeholder Communication Visuals

For stakeholder-facing outputs:

- Lead with the visual that answers the decision question.
- Use fewer visuals with stronger captions.
- Show baseline and current process where relevant.
- Show uncertainty when it changes the decision.
- Convert technical metrics into business quantities.

## Visual Storytelling Sequence

Use this order for reports or decks:

1. Context: what population and question.
2. Data trust: why the data is usable or what caveats matter.
3. Main finding: the chart that answers the question.
4. Driver or segmentation: why the pattern differs.
5. Risk or uncertainty: limitations, error, confidence, or tradeoff.
6. Recommendation: action, threshold, policy, or next test.

## Caption And Takeaway Writing

Good caption pattern:

> [Metric] is [higher/lower/changing] for [population/segment] during [period], suggesting [decision-relevant implication]. Caveat: [limitation or denominator].

Rules:

- Put the takeaway in the title or caption.
- Include denominator and time window.
- Say what the viewer should notice.
- Avoid causal words unless the design supports them.
- Mention uncertainty when relevant.

## Dashboard Planning

Before building:

- Define user and decision cadence.
- Define metric glossary.
- Define default filters.
- Define freshness and source status indicators.
- Define drilldowns.
- Define owner and refresh process.

Dashboard layout:

1. Top row: KPIs with trends and freshness.
2. Middle: decision-driving trends and segment comparisons.
3. Bottom: diagnostics, data quality, and drilldown tables.

Avoid dashboards that are just chart collections with no operating decision.

## Accessibility And Readability

- Use descriptive titles and axis labels.
- Include units.
- Use colorblind-safe palettes.
- Avoid relying on color alone.
- Sort bars by value unless natural order matters.
- Keep labels readable.
- Use direct labels where legends are hard to follow.
- Show sample sizes for small groups.
- Avoid chart clutter and excessive precision.

## Misleading Chart Risks

- Truncated y-axis exaggerates differences.
- Percentages shown without denominators.
- Dual axes imply relationships that may not exist.
- Area/3D charts distort magnitude.
- Aggregates hide subgroup failures.
- Incomplete recent periods look like drops.
- Log scales are not disclosed.
- Correlation visuals are described causally.
- Filters or slicers are not visible.

## Common Failure Modes

- Chart does not answer a stated question.
- Too many visuals dilute the finding.
- Visuals use inconsistent definitions.
- Missing values are silently dropped.
- Test/train/model versions are mixed in one chart.
- Dashboard lacks freshness and ownership.
- Captions describe the chart instead of the implication.

## Tool-Flexible Notes

- Python: use pandas for shaping and matplotlib for portable plots; seaborn/plotly can improve aesthetics/interactivity when available.
- R: use tidyverse for shaping and ggplot2 for grammar-of-graphics consistency.
- SQL: build clean aggregate tables and denominators before visualization.
- Excel/Sheets: use pivots, charts, slicers, and conditional formatting for smaller or stakeholder-facing analysis; protect raw data.
- Notebooks: pair each chart with a markdown takeaway and caveat.
- Dashboards/BI tools: define metric glossary, refresh process, filters, row-level security, and ownership.
