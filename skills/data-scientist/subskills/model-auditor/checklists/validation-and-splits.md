# Validation and Splits

> Confirm that the split strategy is appropriate for the data structure and that the holdout was never used during model development.

## What to inspect

- **Split strategy vs. data structure** — random splits are only valid when observations are truly IID; time-series data requires time-aware splits; grouped data (multiple rows per customer, user, device, or entity) requires group-aware splits
- **Holdout contamination** — was the test set ever used during feature selection, threshold tuning, hyperparameter search, or any other development decision?
- **Cross-validation leakage** — was preprocessing (scaling, encoding, imputation, feature selection) applied to the full dataset before the CV fold boundary? if so, information from validation folds has leaked into training
- **Sample size adequacy** — are there enough events per class for the validation to be meaningful? flag if minority class n < ~50 for classification (exact threshold depends on domain)
- **Class balance and stratification** — is accuracy or similar metric reported on imbalanced classes without stratification or acknowledgment of the imbalance?
- **Backtest / production population match** — was the model trained and tested on a historical population that differs from the live population it will score (different time window, different inclusion criteria, different data availability)?
- **Temporal leakage in windows** — does the training window overlap the evaluation window? does the evaluation use data from within the training period?

## Red flags

- Single train/test split with no cross-validation and no held-out temporal period
- Model trained on the full dataset, then evaluated on a subset of that same data
- Split performed after feature engineering steps (scaling, encoding, imputation applied first)
- "I used an 80/20 split" with no mention of time ordering or grouping structure
- Backtest uses 2021 population but model scores 2024 population without population comparison
- Cross-validation folds selected randomly on time-series data
- Threshold or hyperparameter tuned on the stated test set

## Required evidence

- Explicit description of the split strategy (random / time-aware / group-aware) with justification
- Date ranges or version identifiers for train, validation, and test sets
- Confirmation that no preprocessing step (scaling, encoding, imputation, feature selection) crossed the split boundary
- Population description for training set and for the intended production scoring population
- If cross-validation was used, confirmation that folds respect temporal or group structure

If any of these are missing, mark as an open item in the audit report and state what evidence is needed.

## Fix / retest guidance

- For time-series data: rebuild splits using a time-based cutoff; ensure no training row postdates any test row
- For grouped data: rebuild splits using group-aware methods (e.g., `GroupKFold`, splitting by entity ID before any feature construction)
- For holdout contamination: create a new held-out partition that was never used; if this is not possible, note the limitation explicitly and mark all reported performance metrics as potentially optimistic
- For preprocessing leakage in CV: wrap all preprocessing inside the pipeline/fold boundary; refit transformers on each fold's training data only
- See parent skill `references/validation-and-leakage-checklist.md` for detailed split strategy guidance
