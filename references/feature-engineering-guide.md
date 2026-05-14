# Feature Engineering Guide

Feature engineering turns raw observations into decision-time signals. Build features that are valid, stable, interpretable enough for the use case, and refreshable in the user's environment.

## Operating Rules

- Define the prediction or decision timestamp before creating features.
- Use only information available at or before that timestamp.
- Fit learned transformations inside the training fold or training split.
- Prefer features that can be recomputed reliably in SQL, Python, R, spreadsheets, or a production feature pipeline.
- Track feature definitions, source tables, time windows, refresh cadence, and null behavior.
- Remove or quarantine features whose business meaning cannot be explained.

## Numeric Features

Use for amounts, counts, durations, rates, sensor values, balances, prices, scores, and measurements.

Practical steps:

- Check units and convert before modeling.
- Inspect zero, negative, and extreme values for business meaning.
- Add missingness indicators when missing values may signal behavior or process.
- Consider log, square root, winsorized, or robust-scaled versions for skewed variables.
- Keep original values when interpretability matters and the model can handle scale.
- Use domain caps only when they reflect real limits, not convenience.

Avoid:

- Scaling on the full dataset before splitting.
- Blindly removing outliers that are real high-value or high-risk cases.
- Treating IDs, ZIP codes, or category codes as numeric magnitudes.

## Categorical Features

Use for product, region, channel, status, plan, category, role, segment, device, source, or reason codes.

Options:

- One-hot encoding: good for low-cardinality categories.
- Ordinal encoding: only when order is real.
- Frequency/count encoding: useful for high-cardinality categories when leakage-safe.
- Target encoding: powerful but high leakage risk; compute within folds with smoothing.
- Hashing: useful for very high cardinality when interpretability is less important.
- Group rare categories into "other" using training data only.

Guardrails:

- Preserve unseen category behavior for scoring.
- Do not let rare category grouping learn from test data.
- Document category mappings used in production.
- Watch for categories created after the target event, such as final status or resolution code.

## Date And Time Features

Use when timing, seasonality, recency, or lifecycle stage matters.

Common features:

- Hour, day of week, week, month, quarter, year.
- Weekend, holiday, business day, pay period, fiscal period.
- Age at event, tenure, time since signup, time since last activity.
- Time until renewal, deadline, shipment, appointment, or contract end.
- Local time zone and daylight-saving handling when behavior depends on local time.

Guardrails:

- Use event time, not ingestion time, unless ingestion delay is the signal.
- Avoid extracting future calendar facts unavailable at prediction time.
- Validate that time zones are consistent before computing durations.

## Text Features

Use for reviews, tickets, notes, emails, search queries, descriptions, transcripts, documents, or survey responses.

Options:

- Length, word count, punctuation, language, readability, and keyword flags.
- Bag-of-words or TF-IDF for transparent baselines.
- Topic model proportions for exploratory themes.
- Embeddings for semantic similarity, retrieval, clustering, or classification.
- Entity, phrase, sentiment, intent, or category extraction when validated.

Guardrails:

- Remove or protect PII and sensitive attributes where required.
- Split by entity or time when repeated text can leak across train/test.
- Check for templated text, duplicates, boilerplate, and post-outcome notes.
- Do not use free-text fields entered after human review to predict the review outcome.

## Geospatial Features

Use for location, distance, region, mobility, service area, weather exposure, or proximity effects.

Common features:

- Latitude/longitude validation and geocoding confidence.
- Distance to store, facility, competitor, depot, route, or event.
- Region, market, census tract, service area, or territory.
- Urban/rural classification, density, drive time, or catchment area.
- Spatial lags or neighborhood aggregates when appropriate.

Guardrails:

- Respect privacy and aggregation rules for precise location.
- Avoid proxies for protected attributes unless justified and reviewed.
- Use consistent coordinate systems and units.
- Compute distance features from locations known at decision time.

## Event And Log Features

Use for clickstream, app events, transactions, machine logs, support events, lifecycle changes, and system telemetry.

Patterns:

- Counts by event type in fixed windows.
- Recency of last event.
- Frequency and velocity over recent windows.
- Sequence indicators: first event, last event, repeated path, funnel step reached.
- Time between events.
- Error rate, retry count, session duration, abandonment flags.

Guardrails:

- Define sessionization rules clearly.
- Use closed windows relative to the prediction timestamp.
- Avoid full-lifecycle summaries when predicting an in-lifecycle outcome.
- Distinguish late-arriving events from true absence.

## Behavioral Features

Use for engagement, purchases, usage, support, payments, retention, or product adoption.

Examples:

- Active days in last 7/30/90 days.
- Spend, order count, average order value, and refund rate.
- Feature adoption count and depth.
- Support ticket rate and unresolved ticket age.
- Payment retries, failed transactions, or delinquency counts.
- Trend: current period versus prior period.

Guardrails:

- Align observation windows across users.
- Normalize by exposure or tenure when appropriate.
- Separate behavior caused by an intervention from behavior available before the intervention.

## Customer, Product, And Transaction Features

Customer:

- Tenure, lifecycle stage, plan, industry, size, region, acquisition channel, usage depth.

Product:

- Category, price, margin, age, availability, seasonality, return rate, review profile.

Transaction:

- Basket size, discount, payment method, shipping method, margin, risk flags, recurrence.

Guardrails:

- Confirm entity grain: customer, account, household, product, SKU, transaction, line item.
- Avoid target leakage from post-transaction fields such as refund, cancellation, final status, or collections outcome.
- Use historical aggregates cut off before the transaction or prediction event.

## Time-Series Features

Use for forecasting or future-state prediction.

Common features:

- Lags: previous value at 1, 7, 14, 28, or seasonal periods.
- Rolling mean, median, min, max, standard deviation.
- Rolling counts and rates.
- Change from previous period.
- Seasonal indicators, holidays, promotions, known events.
- External regressors known at forecast time.

Guardrails:

- Use trailing windows only; never centered windows for future prediction.
- Backtest feature generation exactly as it will run in production.
- Treat stockouts, outages, and censored demand separately from true demand.

## Aggregations

Use aggregations to summarize history at entity, group, or time-window level.

Examples:

- Count, sum, mean, median, min, max, distinct count.
- Last, first, most recent, most frequent.
- Windowed aggregates over trailing 7/30/90 days.
- Group-level benchmarks: entity value minus peer average.

Guardrails:

- Build aggregations from training-period or pre-prediction data only.
- Use time-aware joins for slowly changing dimensions.
- Avoid leakage from aggregating all records for an entity across train and test.

## Ratios

Use ratios for normalized behavior:

- Conversion rate, defect rate, refund rate, utilization, margin rate, click-through rate.
- Spend per active day, events per session, revenue per user.
- Current period divided by prior period.

Guardrails:

- Handle zero denominators explicitly.
- Track denominator size; tiny denominators create noisy ratios.
- Include denominator as a separate feature when useful.

## Interaction Terms

Use interactions when the effect of one feature depends on another.

Examples:

- Price by discount.
- Tenure by usage.
- Region by season.
- Customer segment by channel.

Guardrails:

- Prefer domain-driven interactions before exhaustive crosses.
- Watch cardinality explosion.
- Validate that interactions improve out-of-sample performance.
- Keep interactions interpretable when stakeholders need explanations.

## Transformations

Common transformations:

- Log or square root for skew.
- Standardization or robust scaling for distance-based and linear models.
- Normalization for bounded comparisons.
- Box-Cox or Yeo-Johnson when useful and supported.
- Clipping or winsorizing with documented thresholds.

Guardrails:

- Fit parameters on training data only.
- Preserve inverse transform logic for reporting predictions in original units.
- Do not transform solely to improve a chart if it harms interpretation.

## Binning

Use binning for nonlinear relationships, interpretability, or business rules.

Options:

- Domain bins: age bands, tenure bands, spend tiers.
- Quantile bins from training data.
- Fixed-width bins.
- Monotonic bins for scorecards.

Guardrails:

- Learn bin edges from training data only unless bins are domain-defined.
- Avoid bins with too few cases.
- Preserve ordered meaning in labels.

## Lags And Rolling Windows

Use for temporal history.

Rules:

- Lag from the prediction timestamp backward.
- Define window inclusivity: does the current event count?
- Require minimum periods where needed.
- Make late-arriving data behavior explicit.
- Match training feature windows to scoring feature windows.

## Feature Selection

Use selection to reduce noise, cost, instability, and maintenance burden.

Methods:

- Remove impossible, duplicate, constant, near-constant, and leaky features.
- Remove features unavailable in production.
- Use domain review for legitimacy and actionability.
- Use regularization, permutation importance, recursive selection, or tree-based importance carefully.
- Check stability across folds, time periods, and segments.

### Classical Selection Methods

Backward elimination, forward selection, and stepwise selection are classical methods from statistical modeling. Use them mainly for interpretable regression contexts, teaching, or when a transparent manual variable-selection process is required.

- **Backward elimination**: start with all candidate variables, remove the least significant one at a time based on p-values or AIC/BIC until all remaining variables meet a retention criterion.
- **Forward selection**: start with no variables, add the most significant one at a time until adding more variables does not improve fit by the chosen criterion.
- **Stepwise selection**: alternate between forward and backward steps; allows re-entry and re-removal.
- **Best subsets regression**: evaluate all possible subsets of a candidate variable set and select by AIC, BIC, Cp, or adjusted R-squared. Computationally feasible for small to moderate predictor counts.
- **Recursive feature elimination (RFE)**: fit a model, rank features by importance, remove the weakest, refit. Available in scikit-learn and the `caret` / `tidymodels` ecosystems.
- **Regularization-based selection**: LASSO (L1) shrinks coefficients toward zero, often zeroing out weak predictors. Elastic net combines L1 and L2. Ridge (L2) does not produce sparse solutions but stabilizes estimates.
- **Domain-driven selection**: choose variables based on subject matter expertise and business logic before fitting any model. Often the most defensible and maintainable approach.

Guardrails:

- Treat classical stepwise methods as exploratory and interpretability tools, not as default best practice for predictive modeling.
- If using any data-driven selection method to estimate predictive performance, the entire selection process must be nested inside the validation loop — not run on the full dataset first.
- Do not run backward elimination or forward selection on the full dataset, select variables, then split and report test-set performance as unbiased. The test estimate will be optimistic.
- Regularization and domain-driven selection are generally safer for predictive modeling because regularization is differentiable and nestable inside training, and domain selection makes no data-driven choices that inflate performance.
- For classical statistical inference (coefficient p-values, confidence intervals), stepwise selection invalidates standard errors and p-values even when done carefully. Report this limitation.

Do not select features using the full dataset before validation.

## Feature Leakage Risks

High-risk features:

- Final status, resolution, refund, cancellation, diagnosis, chargeoff, or outcome reason.
- Timestamps after the prediction point.
- Aggregates over the full dataset or full customer lifecycle.
- Human review flags created because the outcome was suspected.
- Missingness populated only for positives.
- Target encoding computed outside folds.
- Embeddings or dimensionality reduction fitted on all data when evaluation must be isolated.

When unsure, trace the feature lineage and timestamp.

## Interpretability Tradeoffs

- Raw counts and ratios are easier to explain than opaque embeddings.
- Domain bins can communicate better than high-degree interactions.
- Target encodings may perform well but need careful explanation and leakage control.
- Text embeddings and deep features require example-based explanations and drift monitoring.
- Highly engineered features may improve metrics but reduce trust and maintainability.

Choose the simplest feature set that supports the decision.

## When Not To Engineer More Features

Stop adding features when:

- The target definition or validation split is still questionable.
- A simple baseline has not been built.
- Existing features are leaky or unavailable in production.
- Performance gains are within validation noise.
- Added features cannot be refreshed reliably.
- The model already meets the decision requirement.
- Error analysis points to label quality, sampling, or business process issues rather than missing predictors.

