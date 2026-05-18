# Metrics and Baselines

> Confirm that the reported metric is aligned with the business cost of errors and that at least a naive baseline exists for comparison.

## What to inspect

- **Metric alignment with business cost** — is the chosen metric appropriate for the problem? common mismatches: accuracy on imbalanced data, AUC without calibration for a probability use case, RMSE when asymmetric errors make MAE more appropriate, F1 when precision and recall have very different costs
- **Class imbalance and accuracy misuse** — if the minority class is < 10% of the dataset, accuracy is misleading; require precision, recall, F1, AUC-ROC, or PR-AUC
- **Training vs. validation metric reporting** — is the reported performance from held-out data or from the training set? training performance is not a valid performance estimate
- **Missing naive baseline** — at minimum, compare to majority-class classifier, mean prediction, or historical average; if this comparison is absent, there is no evidence the model adds value
- **Missing current-process baseline** — if a manual rule, decision tree, or prior model exists in production, compare the new model against it on the same holdout
- **Cherry-picked metrics** — is only the best metric reported across multiple runs, seeds, or threshold choices? are unfavorable metrics omitted?
- **Subgroup performance gaps** — aggregate metrics can mask failure modes; check whether performance was broken out by relevant subgroups (demographics, time cohort, geography, product line, etc.)

## Red flags

- "Accuracy 94%" with no mention of class distribution
- No baseline comparison of any kind
- Performance reported only on training data
- A single metric reported for a multi-objective problem
- Subgroup analysis absent for a model that will affect different populations differently
- Multiple candidate models evaluated on the test set (model selection on the test set is leakage)
- Metric chosen after seeing results rather than defined upfront

## Required evidence

- Chosen metric documented with written rationale before seeing results
- A naive baseline (majority-class, mean, historical average, or simple rule) defined and evaluated on the same holdout
- If a current-process baseline exists, it is evaluated on the same holdout and compared
- Performance on held-out data (not training data)
- Subgroup performance broken out by relevant dimensions where the model affects different populations

If any of these are missing, mark as an open item in the audit report.

## Fix / retest guidance

- If accuracy is the only metric on an imbalanced dataset: recompute precision, recall, F1, and AUC on the same holdout
- If no baseline exists: compute majority-class and mean-prediction baselines on the holdout; report the lift over baseline
- If training performance is reported: obtain held-out performance; if no holdout exists, flag as a validation design issue (see `checklists/validation-and-splits.md`)
- If subgroup analysis is missing and the model affects different populations: partition the holdout by relevant dimensions and compare metrics
- See parent skill `references/metrics-guide.md` for metric selection guidance by problem type
