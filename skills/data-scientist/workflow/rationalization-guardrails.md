# Rationalization Guardrails

Use this file when the user, prior work, or the assistant is tempted to skip framing, data quality, validation, baselines, calibration, error analysis, responsible AI, or production-readiness. The purpose is not to slow work down. The purpose is to prevent confident but invalid data science.

Each guardrail has a required response. If the minimum evidence is missing, do not advance the stage or present the result as validated.

---

## "Let's just build the model first."

- **Why it is risky:** Modeling before framing often creates the wrong target, wrong grain, wrong split, and wrong metric. It produces impressive-looking work that cannot support a decision.
- **Required assistant behavior:** Check target, grain, prediction point, validation strategy, baseline, and metric before building. If any are missing, produce or request a Project Brief and Validation Plan first.
- **Minimum evidence needed to proceed:** Defined decision, target, unit of analysis, prediction timestamp, success metric, baseline, and split strategy.
- **Recommended artifact/gate:** Project Brief; Validation Plan; Framing Gate; Validation Gate.

## "The data looks clean enough."

- **Why it is risky:** Silent schema drift, missingness, duplicates, join fan-out, stale data, or leakage can invalidate every downstream chart and model.
- **Required assistant behavior:** Run or request data quality checks: schema, missingness, duplicates, valid ranges, freshness, referential integrity, and leakage risks.
- **Minimum evidence needed to proceed:** Field-level profile, key uniqueness check, missingness summary, date coverage, duplicate results, and leakage candidate disposition.
- **Recommended artifact/gate:** Data Audit Report; Data Readiness Gate; `checklists/data-quality-checklist.md`.

## "Accuracy is good enough."

- **Why it is risky:** Accuracy can hide rare-event failure, class imbalance, bad calibration, and unacceptable false positive or false negative costs.
- **Required assistant behavior:** Check class balance, confusion matrix, precision, recall, F1, ROC-AUC, PR-AUC, calibration, threshold, and business cost. For imbalanced data, do not use accuracy as the headline metric.
- **Minimum evidence needed to proceed:** Class distribution, thresholded confusion matrix, precision/recall metrics, ranking metric where relevant, calibration check if probabilities are used, and cost/capacity statement.
- **Recommended artifact/gate:** Model Comparison Report; Calibration Report; Calibration/Decision Gate.

## "This feature probably is not leakage."

- **Why it is risky:** Plausible-sounding features often contain future, target-derived, or post-outcome information through status fields, aggregates, notes, or workflow actions.
- **Required assistant behavior:** Verify prediction-time availability and whether the feature contains future, target-derived, post-outcome, or human-review information. Trace source timestamp and lineage.
- **Minimum evidence needed to proceed:** Feature definition, source table, event timestamp, update timestamp, prediction timestamp, and documented leakage disposition.
- **Recommended artifact/gate:** Data Audit Report; Validation Plan; `references/validation-and-leakage-checklist.md`.

## "The sample is small but the win rate/performance looks strong."

- **Why it is risky:** Small samples produce unstable rates, wide uncertainty, and selection effects. Apparent lift may disappear with more data.
- **Required assistant behavior:** Report sample size uncertainty, confidence intervals or bootstrap where appropriate, and classify the finding as exploratory unless sufficiently powered.
- **Minimum evidence needed to proceed:** Numerators, denominators, uncertainty interval or resampling check, segment size, and statement of whether the result is exploratory or decision-ready.
- **Recommended artifact/gate:** EDA Summary; Model Comparison Report; Decision Memo.

## "We can tune on the test set just once."

- **Why it is risky:** Test-set tuning destroys the test set as an unbiased final estimate. "Just once" becomes hidden model selection.
- **Required assistant behavior:** Reject the shortcut. Preserve the test set as the final estimate. Use validation data, cross-validation, nested CV, or a new holdout instead.
- **Minimum evidence needed to proceed:** Separate validation/tuning process and untouched final holdout, or explicit downgrade of the claim if the test set was already used.
- **Recommended artifact/gate:** Validation Plan; Experiment Log; Validation Gate.

## "The model is complex but performs better."

- **Why it is risky:** Small metric gains may not justify lower interpretability, unstable behavior, harder deployment, slower scoring, or higher monitoring cost.
- **Required assistant behavior:** Compare against baseline and simpler models. Evaluate interpretability, stability, subgroup performance, runtime, operational fit, and deployment cost.
- **Minimum evidence needed to proceed:** Baseline comparison, simple-model comparison, validation variance, error analysis, complexity rationale, and production-readiness note.
- **Recommended artifact/gate:** Model Comparison Report; Error Analysis Report; Production Gate.

## "Feature importance tells us what caused the outcome."

- **Why it is risky:** Predictive importance measures usefulness for prediction, not causal effect. Acting on noncausal features can fail or harm users.
- **Required assistant behavior:** Separate predictive importance from causality. Use causal language only with a causal design such as randomized experiment, difference-in-differences, matching with assumptions, IV, RD, or natural experiment.
- **Minimum evidence needed to proceed:** Clear statement of predictive versus causal claim, design assumptions if causal, and limitations.
- **Recommended artifact/gate:** Interpretation section; Causal Analysis note; Decision Memo.

## "The dashboard/report looks convincing."

- **Why it is risky:** Polished visuals can hide wrong denominators, stale data, misleading axes, missing uncertainty, filter artifacts, or unsupported conclusions.
- **Required assistant behavior:** Check whether visuals match the data, metric definitions, denominators, uncertainty, limitations, and business question. Confirm freshness and filters.
- **Minimum evidence needed to proceed:** Data source and refresh date, metric definitions, denominator checks, visual captions, limitations, and QA of filters/slicers.
- **Recommended artifact/gate:** Analysis Report; Visual Analysis Workflow; Data Quality Checklist.

## "The model is ready for production because the notebook works."

- **Why it is risky:** A working notebook does not provide reproducibility, input contracts, artifact versioning, logging, monitoring, rollback, ownership, or retraining.
- **Required assistant behavior:** Require deployment readiness checks: reproducibility, environment/dependencies, data validation, feature consistency, model artifact storage, logging, monitoring, rollback, ownership, and retraining plan.
- **Minimum evidence needed to proceed:** Production pipeline outline, input/output contracts, artifact version, test plan, monitoring plan, rollback plan, owner, and incident path.
- **Recommended artifact/gate:** Deployment Readiness Report; Monitoring Plan; Production Gate.

---

## How To Use These Guardrails

1. Name the rationalization when it appears.
2. State the risk in one sentence.
3. Require the minimum evidence before advancing.
4. Produce or request the recommended artifact.
5. End with the next correct action.

