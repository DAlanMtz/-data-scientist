# Calibration and Thresholds

> Confirm that probability outputs are calibrated and that the operating threshold is documented, justified, and appropriate for the use case.

> **Note:** Skip this checklist for models that do not produce probabilities or continuous scores (e.g., rule-based classifiers used only for hard decisions, rank-ordering systems where calibration is irrelevant). Mark all items as "Not applicable — model does not produce probabilities or scores."

## What to inspect

- **Probability output vs. claimed calibration** — if the model outputs scores used as probabilities (e.g., "probability of churn", "likelihood of fraud"), calibration must be checked; raw model outputs are rarely well-calibrated without explicit calibration
- **Calibration curve shape** — a well-calibrated model has predicted probability ≈ observed frequency across score buckets; systematic overconfidence or underconfidence is a reliability problem
- **Threshold selection method** — was the operating threshold chosen on the test set (leakage risk) or on a separate validation set? choosing the threshold that maximizes F1 on the test set inflates reported performance
- **Threshold documentation** — is the operating threshold documented and versioned alongside the model artifact?
- **Threshold drift under distribution shift** — a threshold calibrated on historical data may not hold when the scoring population or outcome base rate changes
- **Operating point documentation** — what precision, recall, FPR, and TPR are achieved at the chosen threshold? are these metrics acceptable given the business cost of false positives and false negatives?

## Red flags

- "We use 0.5 as the threshold" with no justification or analysis
- Threshold chosen by maximizing F1 on the stated test set
- Calibration never checked; scores used directly as probabilities in a formula, pricing model, or financial decision
- Calibration curve not available; only AUC or accuracy reported
- Threshold is not documented alongside the model; it lives only in deployment code or team memory
- Operating point metrics (precision/recall at threshold) not reported

## Required evidence

- Calibration plot (reliability diagram) or calibration error metric (ECE or Brier score) on the held-out set
- Explicit documentation of which dataset was used to select the threshold (must be separate from the final test set)
- The operating threshold value, documented alongside the model version
- Operating point metrics at the chosen threshold: precision, recall, FPR, TPR, and F1

If any of these are missing, mark as an open item in the audit report.

## Fix / retest guidance

- If calibration is unchecked: compute a calibration curve on the holdout; apply Platt scaling or isotonic regression if calibration is poor, then re-evaluate
- If threshold was chosen on the test set: acknowledge that reported F1/precision/recall at that threshold is optimistic; use a separate validation set to reselect the threshold
- If the threshold is undocumented: document it explicitly in the model card or versioned config; include operating point metrics
- If base rate drift is a concern: monitor the observed positive rate over time; flag if it drifts beyond ±[domain-specific tolerance] from the calibration baseline
- See parent skill `references/diagnostics-guide.md` for calibration curve and threshold analysis patterns
