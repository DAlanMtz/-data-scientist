# Leakage and Target Integrity

> Verify that no feature encodes information unavailable at prediction time and that the target is clearly defined, consistently applied, and causally valid.

## What to inspect

- **Feature availability at prediction time** — for each feature, confirm it would exist in the production system at the moment the prediction is made, not after the event resolves
- **Post-event fields** — features derived from outcomes that occur after the event being predicted (e.g., `days_to_resolution` in a ticket-priority model)
- **Target definition** — is the target well-defined, unambiguous, and consistently applied across the dataset?
- **Proxy targets** — is the target a stand-in for what actually matters? what are the gaps between the proxy and the real outcome?
- **Label timing** — does the label arrive before or after the prediction point? is there a lag between event and label that could cause inconsistencies?
- **Entity overlap between train and test** — do the same customers, users, devices, or entities appear in both the training and test sets?
- **Row-level leakage from joins or aggregations** — did a join inadvertently pull in future data? did a rolling window include data from within the target period?
- **Feature names for post-event signals** — scan feature names for `outcome_`, `result_`, `post_`, `final_`, `resolved_`, `closed_`, `actual_`

## Red flags

- AUC or accuracy is suspiciously high (> 0.95 on real-world data with no obvious explanation)
- Feature importance is dominated by a single unexpected feature
- Model performance collapses significantly when evaluated on a truly held-out or time-forward dataset
- Features with names like `outcome_`, `result_`, `post_`, `final_`, `account_closed_flag`, `days_to_resolution`
- Target is defined using an event that happens after the prediction window closes
- No feature availability timestamp or data dictionary is provided

## Required evidence

- Feature data dictionary with timestamps or notes on when each feature is available in production
- Code showing the feature construction pipeline (joins, aggregations, window functions)
- Explicit confirmation that test set rows had no data overlap with the training period
- Clear written definition of the target variable including how and when the label is assigned

If any of these are missing, mark the relevant item as an open item in the audit report and specify what evidence is needed.

## Fix / retest guidance

- Remove any feature confirmed as leaked; retrain from scratch using only pre-prediction-point data
- If entity overlap is found, rebuild the split using group-aware splitting (e.g., `GroupKFold` in scikit-learn or equivalent)
- If label timing is unclear, audit the ETL pipeline and document the exact timestamp used for label assignment
- Re-evaluate all performance metrics on the clean holdout after removing leaked features — do not patch the existing evaluation
- For proxy target gaps, document the divergence explicitly and note what business decisions are and are not supported by the proxy
- See parent skill `references/validation-and-leakage-checklist.md` for deeper leakage review guidance
