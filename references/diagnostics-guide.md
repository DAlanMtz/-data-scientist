# Diagnostics Guide

Use diagnostics to understand whether the model is valid, stable, useful, and safe to act on. Do not stop at one aggregate score.

## Regression Diagnostics

Check:

- Residuals versus fitted values for nonlinearity and heteroscedasticity.
- Residuals by time, segment, geography, channel, and data source.
- Error distribution and tail errors.
- Actual versus predicted plots.
- Prediction bias: mean error overall and by segment.
- Influence of outliers and high-leverage points.
- Multicollinearity for linear models.
- Prediction interval coverage if intervals are used.

Actions:

- Transform target or features when residual patterns are systematic.
- Use robust or quantile methods when outliers dominate.
- Add interactions or nonlinear terms only when validated.
- Segment or hierarchical modeling may be needed when errors differ structurally.

## Classification Diagnostics

Check:

- Confusion matrix at business-relevant thresholds.
- Precision-recall and ROC curves.
- Calibration curve and score distribution.
- Lift chart or gains chart.
- Performance by subgroup and time window.
- False positives and false negatives with representative examples.
- Threshold sensitivity and capacity tradeoffs.
- Feature availability for top predictors.

Actions:

- Calibrate probabilities when scores are used as risk probabilities.
- Adjust threshold by cost and capacity, not by default 0.5.
- Investigate confident wrong predictions first.
- Check whether subgroup differences reflect data quality, bias, or real operational differences.

## Clustering Diagnostics

Check:

- Cluster sizes and outlier clusters.
- Stability across seeds, samples, and time periods.
- Feature distributions by cluster.
- Distance to centroids or membership uncertainty.
- Internal metrics: silhouette, Davies-Bouldin, Calinski-Harabasz.
- External validation: known labels, outcomes, or business KPIs not used in clustering.
- Actionability: each cluster needs a name, profile, and potential decision.

Actions:

- Rescale or transform features if clusters reflect only magnitude.
- Remove redundant or noisy variables.
- Reduce dimensionality when high-dimensional distance is unhelpful.
- Prefer fewer actionable segments over many fragile ones.

## PCA And Factor Diagnostics

Check:

- Explained variance by component.
- Scree plot or eigenvalue pattern.
- Loadings and whether components have interpretable structure.
- Sensitivity to scaling and outliers.
- Stability across samples.
- Reconstruction error if used for compression.
- Factor reliability and cross-loadings for survey constructs.

Actions:

- Standardize variables before PCA when units differ.
- Do not overinterpret components with weak or unstable loadings.
- Use rotation for factor interpretability when appropriate.
- Fit dimensionality reduction inside validation folds if used for predictive modeling.

## Forecasting Diagnostics

Check:

- Backtest performance across multiple cutoffs.
- Residual autocorrelation.
- Residual seasonality and calendar effects.
- Forecast bias by horizon.
- Error by item, region, segment, and volume band.
- Prediction interval coverage and width.
- Performance against naive and seasonal naive baselines.
- Sensitivity to holidays, promotions, stockouts, outages, and regime changes.

Actions:

- Add lag/seasonal features only if available at forecast time.
- Treat outliers and missing periods explicitly.
- Use hierarchical or pooled methods when many related series are sparse.
- Report horizon-specific accuracy, not only average accuracy.

## NLP Diagnostics

Check:

- Duplicate or near-duplicate texts across splits.
- Label quality and annotator disagreement.
- Performance by document length, language, source, topic, and time.
- Confident wrong examples.
- Top terms, examples, or nearest neighbors driving predictions.
- Embedding drift or vocabulary drift over time.
- PII exposure and sensitive attribute proxies.
- Retrieval relevance by query class if search or RAG-like workflows are involved.

Actions:

- Split by entity or time when text repeats or topics drift.
- Improve label guidelines before chasing model complexity.
- Use human review for ambiguous or high-impact categories.
- Maintain representative evaluation sets for changing language.

## Recommendation Diagnostics

Check:

- Offline ranking metrics at the actual `k`.
- Coverage across users and items.
- Popularity bias and long-tail exposure.
- Cold-start performance for new users/items.
- Diversity and repetition.
- Freshness and stale recommendations.
- Segment-level performance.
- Online guardrails: complaints, fatigue, returns, unsubscribes, latency.

Actions:

- Compare against popularity and recency baselines.
- Use time-aware splits.
- Separate candidate generation diagnostics from ranking diagnostics.
- Monitor feedback loops and exposure bias.

## Anomaly Detection Diagnostics

Check:

- Alert volume by day, entity, segment, and source.
- Precision among reviewed alerts.
- Known incident recall.
- False alarm themes.
- Feature contribution or reason codes.
- Drift in normal behavior.
- Seasonality and entity-specific baselines.
- Time-to-detect and time-to-resolve.

Actions:

- Tune for analyst capacity and severity, not just statistical rarity.
- Create suppression or grouping logic for duplicate alerts.
- Provide reason codes and peer comparisons.
- Periodically review normal training data for contamination.

## Data Quality Diagnostics

Check:

- Schema changes, missing columns, type changes, and new categories.
- Row counts and entity counts over time.
- Duplicate keys and broken joins.
- Missingness by source, segment, and time.
- Invalid ranges, impossible dates, and inconsistent units.
- Late-arriving data and backfills.
- Label delays and label availability.
- Data drift in critical features.

Actions:

- Convert important assumptions into automated checks.
- Fail loudly when core input contracts break.
- Separate source defects from model defects before retraining.
- Keep data quality reports close to model monitoring.

## Model Failure And Error Analysis

Use this sequence:

1. Compare to baseline. If the model cannot beat a naive or current-process baseline, stop and diagnose.
2. Slice errors by time, segment, source, and operational pathway.
3. Review the highest-confidence wrong predictions.
4. Check whether errors share missingness, outliers, rare categories, or text patterns.
5. Inspect whether top features are leaky, unstable, or proxies for disallowed attributes.
6. Test threshold sensitivity and capacity constraints.
7. Quantify business impact of error modes.
8. Decide whether to fix data, change features, change model class, adjust threshold, add human review, or avoid deployment.

Failure analysis should produce an action list, not just observations.

