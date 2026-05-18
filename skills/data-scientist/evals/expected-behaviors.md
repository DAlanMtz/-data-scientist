# Expected Behaviors

Use these expectations to score responses to `prompts.md`.

## Prompt 1: Build Me The Best Model Quickly

- **Expected stage/gate:** Stage 0 or 3; Framing Gate and Validation Gate.
- **Expected artifact or response shape:** Project Brief or Modeling Plan outline.
- **Required concerns to raise:** Decision, target, grain, prediction point, validation strategy, baseline, metric, leakage.
- **Weak answer would:** Suggest algorithms immediately.
- **Strong answer would:** Gate-check first, request/define missing information, and name the next correct action.
- **Pass/fail criteria:** Pass if it refuses premature modeling and produces a stage/gate/artifact path.

## Prompt 2: 92% Accuracy

- **Expected stage/gate:** Stage 5 or 7; Model Comparison Gate or Calibration/Decision Gate.
- **Expected artifact or response shape:** Model evaluation review.
- **Required concerns to raise:** Class balance, confusion matrix, precision/recall/F1, ROC-AUC/PR-AUC, calibration, threshold, business cost.
- **Weak answer would:** Say 92% is good.
- **Strong answer would:** Treat accuracy as insufficient evidence and ask for the right metrics.
- **Pass/fail criteria:** Pass if it rejects accuracy-only evaluation.

## Prompt 3: Total Season Stats To Predict Next Week

- **Expected stage/gate:** Stage 3; Validation Gate.
- **Expected artifact or response shape:** Leakage risk review.
- **Required concerns to raise:** Prediction-time availability, whether season totals include future games, time-aware features, cutoff dates.
- **Weak answer would:** Say yes without timestamp checks.
- **Strong answer would:** Require pre-game cutoff features and trailing aggregates only.
- **Pass/fail criteria:** Pass if it identifies potential future-data leakage.

## Prompt 4: Which Features Caused Churn

- **Expected stage/gate:** Stage 8; Interpretation Gate.
- **Expected artifact or response shape:** Interpretation note separating prediction and causality.
- **Required concerns to raise:** Feature importance is not causality, causal design requirements, safe language.
- **Weak answer would:** List feature importances as causes.
- **Strong answer would:** Rephrase as predictive associations and recommend causal design for causal claims.
- **Pass/fail criteria:** Pass if causal overclaiming is prevented.

## Prompt 5: Notebook Works, Production Ready?

- **Expected stage/gate:** Stage 9; Production Gate.
- **Expected artifact or response shape:** Deployment Readiness Report outline.
- **Required concerns to raise:** Reproducibility, dependencies, data validation, feature consistency, artifacts, logging, monitoring, rollback, ownership, retraining.
- **Weak answer would:** Equate successful notebook run with readiness.
- **Strong answer would:** Require production readiness evidence.
- **Pass/fail criteria:** Pass if it names the Production Gate and required checks.

## Prompt 6: Pick The Best Model

- **Expected stage/gate:** Stage 5; Model Comparison Gate.
- **Expected artifact or response shape:** Model Comparison Report.
- **Required concerns to raise:** Same split, same target, baseline, primary metric, secondary metrics, stability, error analysis, deployment cost.
- **Weak answer would:** Pick highest metric.
- **Strong answer would:** Compare decision-relevant tradeoffs and request missing evidence.
- **Pass/fail criteria:** Pass if model choice is not based only on one score.

## Prompt 7: Turn Results Into Recommendation

- **Expected stage/gate:** Stage 7 or 8; Calibration/Decision Gate or Interpretation Gate.
- **Expected artifact or response shape:** Decision Memo.
- **Required concerns to raise:** Action, threshold/policy, expected impact, uncertainty, limitations, owner, monitoring.
- **Weak answer would:** Summarize metrics without recommending action.
- **Strong answer would:** Translate results into a decision with caveats and next action.
- **Pass/fail criteria:** Pass if it creates decision-ready structure.

## Prompt 8: Forecast Looks Good Visually

- **Expected stage/gate:** Stage 6 or 8; Diagnostics Gate or Interpretation Gate.
- **Expected artifact or response shape:** Forecast diagnostics review.
- **Required concerns to raise:** Backtesting, naive baseline, horizon metrics, bias, prediction intervals, incomplete periods, drift.
- **Weak answer would:** Approve based on visual fit.
- **Strong answer would:** Require validation and uncertainty before publishing.
- **Pass/fail criteria:** Pass if it rejects visual-only validation.

## Prompt 9: Cluster Customers

- **Expected stage/gate:** Stage 2 or unsupervised analysis path.
- **Expected artifact or response shape:** Clustering workflow plan.
- **Required concerns to raise:** Objective, feature selection, scaling, number of clusters, stability, profiling, business naming, no causal claims.
- **Weak answer would:** Run k-means and label groups confidently.
- **Strong answer would:** Define actionability and validation without labels.
- **Pass/fail criteria:** Pass if it avoids false certainty and requires cluster profiling.

## Prompt 10: Tuned Until Test Score Improved

- **Expected stage/gate:** Stage 3 or 5; Validation Gate or Model Comparison Gate.
- **Expected artifact or response shape:** Validation issue finding.
- **Required concerns to raise:** Test-set contamination, invalid final estimate, use validation/CV, create new holdout if possible.
- **Weak answer would:** Accept the improved test score.
- **Strong answer would:** Classify as a serious validation issue and recommend remediation.
- **Pass/fail criteria:** Pass if it rejects test-set tuning.

## model-auditor

- When auditing a notebook, the agent names the model claim and data population before listing findings.
- Findings are severity-ranked using Critical / High / Medium / Low / Informational from `workflow/severity-levels.md`.
- Every finding includes evidence and a required fix — not just a flag.
- Open items are listed explicitly when code, data, logs, or baselines are missing; the agent states what specific evidence is needed.
- The agent does NOT declare a model valid or invalid when evidence is insufficient — it marks the item as unverifiable and states what evidence is needed to resolve it.
- The release decision (Block / Caution / Pass) is tied to the severity of findings, not a blanket judgment based on a single metric.
- The agent does not activate for EDA, dashboard design, or first-pass model building unless the user explicitly asks for an audit.
- The agent does not repeat broad methodology guidance from the parent skill — it stays focused on audit structure, findings, and the release decision.

