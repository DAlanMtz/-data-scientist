# Model Selection Guide

Use this guide to choose methods by problem type. Start with the simplest defensible method, then add complexity only when it improves validated performance or decision quality.

## Numeric Prediction

- When to use it: predict a continuous outcome such as revenue, demand, price, spend, time, risk amount, or lifetime value.
- Common methods: mean/median baseline, linear regression, regularized regression, generalized additive models, random forest, gradient boosting, Bayesian regression, quantile regression.
- Required data shape: one row per entity or event with numeric target; features available at prediction time.
- Key preprocessing: handle missing values, encode categoricals, transform skewed target if useful, cap or model outliers deliberately, check units.
- Main metrics: MAE, RMSE, RMSLE, MAPE/sMAPE when denominator is safe, R-squared for explanatory context, prediction interval coverage.
- Main risks: outlier dominance, target leakage, nonstationarity, heteroscedastic errors, optimizing average error when tail errors drive cost.
- Interpretation notes: coefficients are useful for linear models only under assumptions; tree importances need stability checks; report residual patterns and business impact by segment.

## Binary Classification

- When to use it: predict yes/no outcomes such as churn, fraud, conversion, default, defect, response, or eligibility.
- Common methods: majority/current-rule baseline, logistic regression, regularized logistic regression, decision tree, random forest, gradient boosting, naive Bayes, calibrated ensembles.
- Required data shape: one row per decision point with binary target and known outcome window.
- Key preprocessing: define class label carefully, prevent future information, handle imbalance, encode categoricals, preserve missingness indicators when meaningful.
- Main metrics: ROC AUC, PR AUC, log loss, Brier score, accuracy only when classes and costs are balanced, precision/recall/F1 at chosen threshold, lift.
- Main risks: class imbalance hiding poor minority performance, uncalibrated scores, threshold chosen on test set, leakage through post-outcome features.
- Interpretation notes: separate score ranking from probability calibration; explain threshold tradeoffs in false positives, false negatives, capacity, and cost.

## Multiclass Classification

- When to use it: predict one of several exclusive classes such as product category, reason code, diagnosis group, ticket type, or next status.
- Common methods: multinomial logistic regression, tree ensembles, gradient boosting, support vector machines, neural classifiers, hierarchical classifiers.
- Required data shape: one row per entity/event with exactly one class label; enough examples per class.
- Key preprocessing: class consolidation for rare labels, stratified or group/time-aware splitting, text/vector preprocessing if applicable.
- Main metrics: macro/micro/weighted F1, per-class precision/recall, multiclass log loss, top-k accuracy, confusion matrix.
- Main risks: rare classes ignored, ambiguous labels, hierarchy not respected, data leakage from label-derived fields.
- Interpretation notes: report confusion patterns and whether mistakes are operationally similar or costly.

## Ranking

- When to use it: order items, leads, documents, offers, candidates, or interventions by relevance or expected value.
- Common methods: score-based classifiers/regressors, learning-to-rank models, gradient boosting rankers, pairwise/listwise ranking, heuristic business rules.
- Required data shape: queries/users/contexts with candidate items and relevance, click, conversion, or value labels.
- Key preprocessing: construct candidate sets, handle position bias, group splits by query/user, avoid logging-policy leakage.
- Main metrics: NDCG, MAP, MRR, precision@k, recall@k, hit rate@k, lift@k, expected value at capacity.
- Main risks: biased implicit feedback, training on exposed items only, optimizing clicks over business value, evaluation candidate mismatch.
- Interpretation notes: explain top drivers of rank and test whether ranking improves outcomes at the actual decision capacity.

## Customer Segmentation

- When to use it: group customers, accounts, products, stores, or users into actionable segments without a target label.
- Common methods: business rules, k-means, Gaussian mixtures, hierarchical clustering, DBSCAN/HDBSCAN, latent class models.
- Required data shape: one row per entity with stable features measured over a comparable window.
- Key preprocessing: align observation windows, scale numeric features, handle skew, reduce high-cardinality noise, remove size-only artifacts if not desired.
- Main metrics: silhouette, Davies-Bouldin, Calinski-Harabasz, stability, segment size, actionability, downstream KPI separation.
- Main risks: clusters reflect scale or missingness artifacts, too many tiny segments, unstable clusters, no operational use.
- Interpretation notes: profile each segment with plain-language labels, key differentiators, size, value, and recommended actions.

## Dimensionality Reduction

- When to use it: compress many variables, visualize structure, denoise features, create latent factors, or inspect embeddings.
- Common methods: PCA, factor analysis, correspondence analysis, UMAP, t-SNE, autoencoders, matrix factorization.
- Required data shape: matrix of entities by numeric variables, encoded categories, survey responses, text embeddings, or interaction counts.
- Key preprocessing: scaling, imputation policy, sparse handling, outlier review, variable selection.
- Main metrics: explained variance, reconstruction error, trustworthiness, factor loadings, stability across samples.
- Main risks: overinterpreting visualization geometry, unstable components, leakage if fitted before splitting, losing rare but important signals.
- Interpretation notes: PCA/factors need loading review; UMAP/t-SNE are exploratory views, not proof of separable groups.

## Survey Or Preference Analysis

- When to use it: analyze attitudes, satisfaction, conjoint choices, ratings, preference tradeoffs, or latent constructs.
- Common methods: descriptive statistics, factor analysis, reliability analysis, ordinal/logistic models, conjoint models, mixed effects models, clustering.
- Required data shape: respondent-level data with question responses, metadata, weights, and survey design if applicable.
- Key preprocessing: code scales consistently, handle skip logic, weights, missingness, straight-lining, and reverse-coded items.
- Main metrics: confidence intervals, reliability coefficients, factor fit, part-worth utilities, segment differences.
- Main risks: sampling bias, leading questions, treating ordinal data carelessly, overclaiming causal effects from cross-sectional surveys.
- Interpretation notes: separate stated preference from revealed behavior; report uncertainty and respondent base sizes.

## Forecasting

- When to use it: predict future values indexed by time, such as demand, revenue, traffic, staffing, inventory, or capacity.
- Common methods: naive, seasonal naive, exponential smoothing, ARIMA/SARIMA, dynamic regression, Prophet-style decompositions, gradient boosting with lags, deep forecasting for large panels.
- Required data shape: timestamped series with consistent frequency; optional exogenous variables known in the future.
- Key preprocessing: frequency alignment, missing time periods, calendar effects, holidays, outliers, train/validation backtesting.
- Main metrics: MAE, RMSE, MAPE/sMAPE with caution, WAPE, MASE, pinball loss, interval coverage.
- Main risks: future-known covariates not actually available, leakage from centered rolling windows, regime shifts, stockouts or censored demand, aggregate accuracy hiding item-level failures.
- Interpretation notes: show trend, seasonality, residuals, forecast intervals, and backtest windows.

## Text Mining

- When to use it: classify, cluster, extract, search, summarize, or understand unstructured text.
- Common methods: keyword rules, bag-of-words, TF-IDF, topic models, embeddings, transformer classifiers, named entity recognition, semantic search.
- Required data shape: text documents with metadata; labels when supervised; document boundaries and language known.
- Key preprocessing: deduplication, language detection, PII handling, tokenization or embedding generation, train/test split by entity/time where needed.
- Main metrics: classification metrics, retrieval metrics, topic coherence, extraction precision/recall, human evaluation for subjective tasks.
- Main risks: label noise, memorized duplicates, data drift in language, prompt or annotation bias, privacy exposure.
- Interpretation notes: inspect representative texts, false positives/negatives, top terms, nearest neighbors, and subgroup language variation.

## Recommendation

- When to use it: suggest products, content, offers, actions, or matches to users or contexts.
- Common methods: popularity, content-based filtering, collaborative filtering, matrix factorization, two-tower retrieval, sequence models, hybrid rankers.
- Required data shape: user-item interactions with timestamps; item/user metadata; exposure data if available.
- Key preprocessing: define positive/negative events, handle cold start, time splits, candidate generation, negative sampling.
- Main metrics: precision@k, recall@k, NDCG, MAP, hit rate, coverage, diversity, novelty, business value, online A/B metrics.
- Main risks: feedback loops, popularity bias, exposure bias, stale recommendations, offline-online mismatch.
- Interpretation notes: explain why an item is recommended using similar users/items, content attributes, or recent behavior; monitor diversity and fairness.

## Anomaly Detection

- When to use it: identify rare, unusual, or suspicious records, series, events, users, or system states.
- Common methods: rules, robust z-scores, isolation forest, one-class SVM, autoencoders, density models, change point detection, control charts.
- Required data shape: normal behavior history; labels are helpful but often incomplete; timestamp and entity context matter.
- Key preprocessing: separate entity baselines, scale features, remove known incidents from normal training if possible, handle seasonality.
- Main metrics: precision@k, recall against known incidents, alert volume, time-to-detect, false alarm rate, analyst yield.
- Main risks: no ground truth, alert fatigue, concept drift, rare legitimate behavior flagged, training on contaminated anomalies.
- Interpretation notes: provide reason codes, feature deviations, peer comparison, and expected normal range.

## Association Rules

- When to use it: discover co-occurrence patterns such as basket analysis, bundles, cross-sell, content combinations, or event sequences.
- Common methods: Apriori, FP-growth, sequence mining, lift analysis, co-occurrence matrices.
- Required data shape: transaction/session/entity baskets with item sets and timestamps if sequence matters.
- Key preprocessing: define basket boundaries, filter rare items, normalize item taxonomy, remove trivial bundles or policy-driven co-occurrence.
- Main metrics: support, confidence, lift, conviction, leverage, coverage, business value.
- Main risks: high-confidence rules from popular items, spurious multiple comparisons, non-actionable rules, seasonality artifacts.
- Interpretation notes: prioritize rules with lift, sufficient support, and a plausible action.

## Causal Questions

- When to use it: estimate the effect of an intervention, policy, treatment, product change, price change, campaign, or exposure.
- Common methods: randomized experiments, difference-in-differences, matching, weighting, regression adjustment, instrumental variables, regression discontinuity, causal forests.
- Required data shape: treatment/exposure, outcome, timing, units, confounders, and assignment mechanism.
- Key preprocessing: define treatment timing, outcome window, eligibility, covariates measured before treatment, and interference risk.
- Main metrics: average treatment effect, heterogeneous treatment effect, confidence intervals, balance diagnostics, pre-trend checks, power.
- Main risks: confounding, selection bias, post-treatment controls, interference, survivorship bias, weak instruments, violated parallel trends.
- Interpretation notes: causal claims require design assumptions; state them plainly and test what can be tested.

## Optimization Or Decision Problems

- When to use it: choose actions under constraints, allocate resources, set thresholds, schedule, route, price, or optimize policy.
- Common methods: threshold optimization, linear/integer programming, simulation, decision trees, contextual bandits, reinforcement learning where justified.
- Required data shape: alternatives, constraints, objective function, cost/reward estimates, uncertainty, and operational rules.
- Key preprocessing: estimate costs and benefits, validate constraints, simulate edge cases, define capacity and fairness limits.
- Main metrics: expected value, cost saved, service level, regret, constraint violations, robustness, sensitivity.
- Main risks: optimizing a proxy objective, brittle assumptions, ignored constraints, unstable estimates, unfair allocation.
- Interpretation notes: show tradeoff curves and sensitivity to key assumptions; make the recommended policy auditable.

## Variable Selection for Statistical and Regression Models

Variable selection is the process of choosing which predictors to include in a model. The right approach depends on the goal: interpretability, inference, or predictive performance.

### Classical Selection Methods

Backward elimination, forward selection, and stepwise selection are classical methods. Use them mainly for interpretable statistical modeling, teaching, or when stakeholders require a transparent, step-by-step variable-selection process. They are not the default recommended approach for predictive modeling.

| Method | How it works | When to use | Key risk |
|---|---|---|---|
| Backward elimination | Start full, remove least significant variables one at a time | Small datasets, explanatory models | Overfitting if not validated |
| Forward selection | Start empty, add most significant variables one at a time | Large predictor pools, interpretability first | Misses interactions |
| Stepwise selection | Alternate add/remove steps | Exploratory modeling | Invalidates p-values; unstable |
| Best subsets | Evaluate all subsets, select by AIC/BIC/Cp | Small predictor count, exhaustive search | Computationally expensive; multiple comparisons |

**Guardrails for classical methods:**

- These methods are exploratory. They do not guarantee the optimal or most generalizable variable set.
- Stepwise selection and best subsets invalidate standard errors and p-values due to the implicit multiple comparisons. Do not interpret selected coefficients as if the variables were pre-specified.
- If estimating predictive performance, the entire selection procedure must be nested inside the validation loop. Running selection on the full dataset and then reporting test-set performance as unbiased is a form of data leakage.
- Use AIC or BIC as selection criteria when the goal is model explanation; use cross-validated metrics when the goal is prediction.

### Regularization-Based Selection

Regularization is generally safer for predictive modeling because the selection mechanism is continuous, differentiable, and naturally nestable inside training folds.

- **LASSO (L1 regularization)**: shrinks coefficients toward zero; zeroes out weak predictors, producing sparse solutions. Select the regularization strength by cross-validation.
- **Ridge (L2 regularization)**: shrinks coefficients without zeroing them; good for correlated predictors.
- **Elastic net**: combines L1 and L2; better than pure LASSO when predictors are correlated.
- **Regularized logistic regression**: the same L1/L2/elastic-net approach for classification.

Regularization does not require pre-selecting variables. It learns sparsity from data within validation.

### Model-Based and Wrapper Methods

- **Recursive feature elimination (RFE)**: fit, rank, remove weakest features, repeat. Must be nested inside cross-validation folds when used for feature selection that informs performance estimation.
- **Permutation importance**: measure how much performance drops when a feature is randomly shuffled. More reliable than impurity-based importance for correlated features.
- **Tree-based importance**: fast and interpretable but biased toward high-cardinality features. Use alongside permutation importance.

### Domain-Driven Selection

Choose variables based on subject matter expertise and business logic before fitting any model. This is often the most defensible approach because:

- It is not susceptible to data-driven overfitting
- It produces interpretable, maintainable feature sets
- It aligns with how decisions are explained to stakeholders

Use domain selection to produce the candidate set, then apply regularization or validation-based comparison to confirm which candidates earn their place.

### Choosing a Selection Strategy

| Goal | Recommended approach |
|---|---|
| Interpretable explanatory model | Domain selection + backward elimination with AIC/BIC; acknowledge p-value limitations |
| Predictive performance | Regularization (LASSO/elastic net) or RFE nested inside CV |
| High-dimensional data | Regularization; avoid stepwise |
| Transparency required by stakeholders | Domain selection first; classical methods documented step by step |
| Classical statistical inference | Domain selection; avoid data-driven selection if inference is the goal |

