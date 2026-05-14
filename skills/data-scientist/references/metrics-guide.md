# Metrics Guide

Choose metrics from the decision. A good metric rewards the behavior the business actually wants and exposes the cost of failure.

## Regression Metrics

- MAE: average absolute error. Use when errors have a linear cost and interpretability matters.
- RMSE: penalizes large errors more strongly. Use when large misses are disproportionately costly.
- Median absolute error: robust to outliers. Use when typical error matters more than tail error.
- R-squared: explanatory context, not a decision metric by itself.
- RMSLE: useful for positive skewed targets when relative error matters; invalid for negative values.
- MAPE: easy to explain but unstable near zero.
- sMAPE: reduces some MAPE issues but can still behave oddly near zero.
- Quantile loss / pinball loss: use for prediction intervals or percentile forecasts.
- Prediction interval coverage: use when uncertainty bounds matter.

Selection rule: if overprediction and underprediction have different costs, use a cost-weighted metric or quantile objective.

## Classification Metrics

- Accuracy: only useful when classes and error costs are roughly balanced.
- Precision: of predicted positives, how many are true positives. Use when false positives are costly.
- Recall/sensitivity: of actual positives, how many are found. Use when false negatives are costly.
- Specificity: of actual negatives, how many are correctly ignored.
- F1: balances precision and recall when one threshold is needed and costs are similar.
- ROC AUC: ranking quality across thresholds; can look optimistic under severe imbalance.
- PR AUC: better for rare positives.
- Log loss: rewards calibrated probabilities and penalizes confident wrong predictions.
- Brier score: probability accuracy and calibration quality.
- Confusion matrix: always include for thresholded classifiers.

Selection rule: report threshold-free ranking metrics and threshold-specific operating metrics when the model will trigger action.

## Imbalanced Classification Metrics

For rare events, avoid accuracy as the headline metric.

- PR AUC: summary of precision-recall tradeoff.
- Precision@k: useful when only the top cases can be reviewed.
- Recall@k: useful when the business has fixed review capacity.
- Lift@k: improvement over random selection in the top scored group.
- False positives per day/week: operational alert burden.
- Detection rate at fixed false positive rate: useful for fraud, risk, and monitoring.
- Cost-weighted confusion matrix: best when business costs are known.

Always compare to prevalence and a simple ranking baseline.

## Ranking Metrics

- Precision@k: fraction of top-k items that are relevant.
- Recall@k: fraction of relevant items retrieved in top-k.
- MAP: average precision across ranked relevant items.
- MRR: rewards placing the first relevant item high.
- NDCG: rewards correct ordering with graded relevance.
- Hit rate@k: whether at least one relevant item appears in top-k.
- Lift@k: business-friendly comparison to random or current process.

Match `k` to the actual interface or operational capacity.

## Forecasting Metrics

- MAE: average absolute forecast error.
- RMSE: penalizes large misses.
- WAPE: total absolute error divided by total actuals; useful for aggregate demand.
- MASE: compares against naive forecast; good across series with different scales.
- MAPE: understandable but unsafe with zeros and small actuals.
- sMAPE: sometimes useful, still imperfect near zero.
- Pinball loss: evaluates quantile forecasts.
- Interval coverage and interval width: evaluate forecast uncertainty.
- Bias / mean error: detects systematic over- or under-forecasting.

Always compare to naive and seasonal naive baselines.

## Clustering Metrics

- Silhouette score: cohesion and separation; sensitive to shape and distance metric.
- Davies-Bouldin: lower is better; favors compact separated clusters.
- Calinski-Harabasz: higher is better; can favor more clusters.
- Stability: whether clusters persist across samples, seeds, or time windows.
- Segment size: avoids unusably tiny clusters.
- Business separation: differences in outcomes, behaviors, or actions.
- Interpretability/actionability: whether stakeholders can name and use the segments.

Internal cluster metrics are not enough. A useful segmentation must be stable and actionable.

## Recommendation Metrics

- Precision@k, recall@k, NDCG, MAP, MRR, and hit rate@k.
- Coverage: share of catalog/users receiving recommendations.
- Diversity: variety within recommendations.
- Novelty: avoids only recommending obvious popular items.
- Serendipity: useful unexpected recommendations, often requiring human or online evaluation.
- Conversion, retention, revenue, watch time, or satisfaction in online tests.
- Guardrail metrics: unsubscribe, returns, complaints, latency, fairness, fatigue.

Offline metrics can be biased by historical exposure. Prefer online tests for final claims when feasible.

## Anomaly Detection Metrics

- Precision@k: analyst yield at review capacity.
- Recall against known incidents: coverage of confirmed anomalies.
- False alarm rate: alert burden.
- Time-to-detect: delay between incident start and alert.
- Alert volume: operational feasibility.
- Area under PR curve: useful when labeled anomalies exist.
- Business loss captured: value-weighted detection.

When labels are incomplete, evaluate with case review, backtesting known incidents, and alert burden.

## Calibration Metrics

- Calibration curve / reliability diagram: predicted probability versus observed rate.
- Brier score: squared error of probability predictions.
- Expected calibration error: summary of calibration gaps by bins.
- Log loss: punishes confident wrong probabilities.
- Calibration-in-the-large: average predicted probability versus observed rate.
- Slope calibration: whether probabilities are too extreme or too muted.

Calibration matters when scores are interpreted as probabilities, used for expected value, or thresholded by cost.

## Business-Cost-Based Metric Selection

Define the cost table:

- True positive value.
- False positive cost.
- False negative cost.
- True negative value or no-action cost.
- Capacity constraints.
- Delay cost.
- Customer, legal, or reputational risk.

Then choose:

- Threshold metric when action is binary.
- Ranking metric when capacity is fixed.
- Cost-weighted objective when costs are known.
- Calibration metric when probabilities drive expected value.
- Forecast interval metric when planning risk matters.

Report technical metrics with business translation: expected cases caught, alerts created, dollars saved, staff hours used, missed opportunities, and uncertainty.

