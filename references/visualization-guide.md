# Visualization Guide

Use visuals to answer questions, expose data problems, diagnose models, and support decisions. Every chart should have a job.

## Plot Selection Rules

- Distribution: histogram, density, box plot, violin, bar chart for categories.
- Relationship between two numeric variables: scatter, hexbin, contour, fitted line with residual check.
- Relationship between category and numeric variable: box plot, violin, dot plot, grouped summary with intervals.
- Relationship between two categories: stacked bar, mosaic, heatmap, contingency table.
- Change over time: line chart, area chart only for additive quantities, calendar heatmap for seasonality.
- Ranking: sorted bar chart, dot plot, Pareto chart.
- Composition: stacked bar for few categories; avoid pies except for very simple shares.
- Uncertainty: error bars, confidence intervals, prediction intervals, fan charts.
- Spatial pattern: map only when geography is central; otherwise use ranked regional charts.

If the question is not clear, write the question before choosing the chart.

## EDA Visuals

Use EDA visuals to understand structure:

- Target distribution by population and time.
- Feature distributions for numeric variables.
- Category frequency bars for high-impact categorical variables.
- Correlation heatmap for numeric feature screening.
- Scatter or hexbin plots for important numeric relationships.
- Segment comparison plots for known business groups.
- Cohort tables or heatmaps for lifecycle behavior.

Keep EDA charts compact and label the implication, not just the variable name.

## Data Quality Visuals

Use to find defects:

- Row counts by day/source to detect gaps and backfills.
- Distinct key counts by period.
- Invalid value counts by source.
- Duplicate rate over time.
- Schema-change timeline.
- Range plots for important numeric fields.
- Join match rate by table and period.

Pair each data quality visual with a decision: fix, exclude, document, or monitor.

## Missingness Visuals

Useful patterns:

- Missingness bar chart by column.
- Missingness heatmap for row/column structure.
- Missingness by time, source, segment, or target.
- Co-missingness matrix for related fields.
- Missing versus target or outcome rate plot.

Interpretation guardrail: missingness can be data quality, business process, or signal. Do not impute before understanding which.

## Distribution Plots

Choose:

- Histogram for count and shape.
- Density for smooth comparisons when sample size is adequate.
- Box plot for summary and outliers.
- Violin for distribution shape across groups.
- ECDF for comparing distributions without bin choices.

Avoid:

- Too many overlaid densities.
- Default bins hiding spikes at zero or business thresholds.
- Treating outliers as errors without investigation.

## Relationship Plots

Choose:

- Scatter for small/medium numeric pairs.
- Hexbin or 2D density for large datasets.
- Facets for segment-specific relationships.
- Partial dependence or accumulated local effects for model relationships.
- Grouped means with intervals for category-to-numeric relationships.

Always check whether relationships change by time, segment, or data source.

## Time-Series Plots

Use:

- Line chart for trend and seasonality.
- Small multiples for many related series.
- Seasonal subseries plot for weekly/monthly patterns.
- Rolling average with raw values for noisy series.
- Event annotations for launches, outages, policy changes, campaigns.
- Backtest cutoffs and forecast intervals for forecasting work.

Avoid dual axes unless the relationship is impossible to show otherwise and clearly labeled.

## Regression Diagnostics Visuals

Use:

- Actual versus predicted plot.
- Residuals versus fitted values.
- Residual distribution.
- Residuals by time and segment.
- Q-Q plot when distributional assumptions matter.
- Prediction interval coverage plot.
- Error by predicted value band.

Look for bias, heteroscedasticity, nonlinear residual patterns, and tail failures.

## Classification Visuals

Use:

- Confusion matrix at chosen threshold.
- ROC curve and PR curve.
- Calibration curve.
- Score distribution by class.
- Lift or gains chart.
- Precision/recall by threshold.
- Performance by subgroup.
- False positive and false negative example tables.

For imbalanced classification, lead with PR, lift, and operating threshold charts rather than accuracy.

## Clustering Visuals

Use:

- Cluster profile heatmap.
- Feature distribution by cluster.
- Size bar chart.
- PCA/UMAP/t-SNE projection for exploration only.
- Silhouette plot.
- Stability chart across seeds or samples.
- Business KPI comparison by cluster.

Do not use a 2D projection as proof that clusters are real. Use it as a diagnostic view.

## PCA And Factor Analysis Visuals

Use:

- Scree plot.
- Explained variance cumulative plot.
- Loading heatmap or loading bar chart.
- Biplot when readable.
- Factor score distributions.
- Cross-loading table for factors.

Make component interpretation explicit. Avoid naming components without reviewing loadings.

## Forecasting Visuals

Use:

- Historical actuals plus forecast and prediction intervals.
- Backtest actual versus forecast by window.
- Error by horizon.
- Residual autocorrelation plot.
- Seasonal pattern plots.
- Forecast bias by item or segment.
- Coverage plot for forecast intervals.

Show naive or seasonal naive baseline when comparing forecast models.

## NLP And Text Visuals

Use:

- Label distribution.
- Document length distribution.
- Term frequency or TF-IDF bars.
- Topic prevalence over time.
- Embedding projection for exploration.
- Confusion matrix for text classifiers.
- Example tables for false positives/negatives.
- Retrieval relevance examples by query type.

Avoid word clouds as primary evidence. They are weak for analysis and often hide frequency scale.

## Recommendation Visuals

Use:

- Precision/recall/NDCG at k.
- Coverage by user and item.
- Popularity bias curve.
- Recommendation diversity distribution.
- Cold-start performance.
- Online funnel metrics by variant.
- Exposure distribution across catalog or creators.

Show both relevance and guardrails. A high-click recommender can still be stale, narrow, or harmful.

## Anomaly Detection Visuals

Use:

- Time series with anomalies highlighted.
- Score distribution and alert threshold.
- Alert volume over time.
- Top contributing features or deviations.
- Peer comparison bands.
- Known incident overlay.
- False alarm themes by source or segment.

Keep anomaly visuals operational: what happened, why it was flagged, how severe it is, and what to do next.

## Dashboard And Reporting Visuals

Use dashboards for repeated decisions:

- KPI tiles only for metrics that drive action.
- Trend lines with targets and annotations.
- Drilldowns by segment, source, cohort, or model version.
- Data freshness and quality indicators.
- Model monitoring panels for drift, performance, calibration, and volume.
- Clear filter defaults and definitions.

Do not create dashboards that require the viewer to infer definitions, population, or time window.

## Common Visualization Mistakes

- Chart chosen before the question is defined.
- Too many metrics on one visual.
- Unsorted bars for ranked comparisons.
- Truncated axes that exaggerate differences without notice.
- Percentages without denominators.
- Averages hiding important subgroup failures.
- No uncertainty shown when sampling error matters.
- Mixing train, validation, and test performance without labels.
- Showing model curves without the business operating point.
- Using decorative visuals where a small table is clearer.

