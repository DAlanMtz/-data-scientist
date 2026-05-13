# Validation And Leakage Checklist

Use this before trusting performance numbers. Leakage is not a minor technical issue; it can invalidate the entire conclusion.

## Train/Test Split Standards

- Define the prediction point and outcome window before splitting.
- Split after the target is defined but before fitting preprocessing, feature selection, resampling, or model tuning.
- Keep a final holdout set untouched until final model comparison is complete.
- Use stratification for classification only when it does not violate time or group structure.
- Keep the test set representative of the future evaluation population.
- Do not repeatedly tune decisions on the test set.
- Record split logic, random seed if applicable, date cutoffs, group keys, and row counts.

## Cross-Validation Standards

- Use cross-validation for model selection when observations are independent enough for folds to be exchangeable.
- Put all learned preprocessing inside the fold: imputation, scaling, encoding, feature selection, resampling, dimensionality reduction, target encoding, and tuning.
- Report mean and variation across folds.
- Use nested cross-validation when the same data would otherwise be used for both tuning and unbiased performance estimation.
- Do not use standard k-fold CV for forecasting, future prediction, or repeated entity observations unless those structures are handled.

## Time-Aware Validation

Use when data has temporal order or the model will score future cases.

- Train on past data and validate on later data.
- Use rolling-origin or expanding-window backtests when possible.
- Ensure features use only data available before the prediction timestamp.
- Avoid centered rolling windows, full-period aggregates, and retrospectively revised fields.
- Separate model selection windows from final test windows.
- Evaluate across multiple time windows to detect regime instability.
- Check whether labels arrive with delay and whether the validation mimics that delay.

## Group-Aware Validation

Use when rows share entities such as customers, accounts, devices, households, patients, stores, products, sessions, or documents.

- Keep all rows for the same entity in the same split when the deployment target is new or unseen entities.
- If deployment predicts future events for known entities, combine group logic with time-aware validation.
- Split by higher-level entity when leakage can occur through related records.
- Check for duplicate or near-duplicate records across splits.
- For recommender and ranking systems, split by user, query, session, or time according to the deployment scenario.

## Data Leakage Checks

Ask these questions for every feature:

- Would this value be known at the decision time?
- Is it created, updated, or corrected after the outcome?
- Does it contain the target directly or indirectly?
- Is it derived from a table that only exists after the event?
- Does missingness itself reveal the outcome?
- Does it encode manual action taken because staff already knew the outcome?
- Does it include full-period aggregates that use future observations?

## Target Leakage Checks

Common target leakage examples:

- Status fields recorded after the outcome.
- Cancellation reason used to predict cancellation.
- Collection activity used to predict default.
- Diagnosis, repair, or resolution fields used to predict the diagnosis, defect, or resolution.
- Revenue including the future period being predicted.
- Churn label embedded in account state.
- Survey completion used to predict satisfaction among all customers.

Action: remove, lag, or redefine the feature. If it is legitimately available, document why and verify timestamps.

## Preprocessing Leakage Checks

Ensure these are fitted only on training data or inside validation folds:

- Scaling and normalization.
- Imputation values.
- One-hot category discovery when rare or new categories matter.
- Target encoding and mean encoding.
- Feature selection.
- PCA, factor analysis, embeddings trained on task data, or learned dimensionality reduction.
- Oversampling, undersampling, SMOTE, or class balancing.
- Outlier thresholds learned from distributions.

## Duplicate And Entity Leakage Checks

- Exact duplicate rows across train/test.
- Same entity in both train and test when entity memory inflates results.
- Same document, ticket, image, transaction, or text with slight edits across splits.
- Household, company, device, IP, location, or account hierarchies crossing splits.
- Multiple rows from the same event lifecycle spread across train/test.
- Aggregates computed using all rows for an entity before splitting.

Action: deduplicate, split by group, or redesign the validation around the deployment target.

## Feature Leakage Checks

Flag features with:

- Names containing outcome, label, target, final, status, resolved, cancelled, charged_off, converted, returned, refunded, diagnosis, claim, or post.
- Timestamps after the prediction time.
- Values populated only for positive cases.
- Extremely high single-feature performance.
- Suspiciously strong correlation with target.
- Business process fields triggered by the outcome.
- Analyst notes, support tags, or workflow states applied after review.

Do not automatically delete every strong feature; verify availability and lineage.

## Evaluation Leakage Checks

- Threshold selected on the test set.
- Test labels used to choose feature definitions.
- Manual test-set inspection followed by targeted feature changes.
- Multiple model attempts reported only for the best test score.
- Business rules tuned on the holdout period.
- Time windows chosen after seeing performance.
- Removing hard test examples without a predeclared exclusion rule.

Action: create a new validation split, use nested validation, or clearly downgrade performance claims.

## Red Flags

Treat these as stop signs:

- Test performance is dramatically better than expected or better than operational reality.
- Cross-validation is excellent but future holdout is poor.
- Model relies heavily on fields generated after the outcome.
- Random split is used for time series, repeated customers, documents, or sessions.
- Same entity appears in train and test.
- Preprocessing was run on the full dataset before splitting.
- A feature has near-perfect predictive power with no business explanation.
- The test set was used many times during development.
- There is no naive baseline.
- The data extract does not include timestamps needed to prove feature availability.

