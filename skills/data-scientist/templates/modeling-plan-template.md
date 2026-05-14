# Modeling Plan Template

## Purpose

Document the intended modeling approach before building it — which model families to explore, in what order, at what complexity, and how they will be compared. Prevents unstructured experimentation, aligns stakeholders on scope, and ensures interpretability and operational constraints are considered before the first model runs.

## When to Use

At the start of **Stage 5: Model Development and Comparison**, or optionally during Stage 3 for larger projects. Most valuable when multiple stakeholders have opinions on approach, when the experiment budget is constrained, or when the project involves a new problem type for the team.

## Required Inputs

- Validation Plan (Stage 3)
- Baseline results (Stage 4)
- Business constraints from the Project Brief (interpretability, latency, infrastructure)

## Minimum Contents

### 1. Plan Header

- Project: `[name]`
- Plan date: `[date]`
- Analyst: `[name]`
- Baseline performance to beat: `[metric: value]`
- Experiment budget: `[approximate number of meaningful experiments]`

### 2. Problem Type Confirmation

| Element | Value |
|---|---|
| Problem type | `[ ] Binary classification` / `[ ] Multiclass` / `[ ] Regression` / `[ ] Ranking` / `[ ] Forecasting` / `[ ] Clustering` / `[ ] Other` |
| Data shape | `[rows × features; sparse/dense; time-series; grouped]` |
| Sample size | `[n training rows, n positive cases if classification]` |
| Key challenge | `[e.g., class imbalance / concept drift / high cardinality / small n / interpretability requirement]` |

### 3. Candidate Model Families

List in order of planned evaluation (simple to complex).

| # | Model family | Rationale | Interpretability | Approx. latency | Key risk |
|---|---|---|---|---|---|
| 1 | `[e.g., Logistic Regression]` | `[why appropriate]` | `[high/medium/low]` | `[ms/s]` | `[risk]` |
| 2 | `[e.g., Gradient Boosted Trees]` | `[why appropriate]` | `[medium]` | `[ms]` | `[overfitting / tuning cost]` |
| 3 | `[e.g., Neural network]` | `[only if justified]` | `[low]` | `[variable]` | `[data volume requirement]` |

Stop adding complexity when simpler models meet the performance and constraint requirements.

### 4. Feature Engineering Plan

| Feature family | Examples | Engineering step | Leakage risk check |
|---|---|---|---|
| Numeric transformations | `[log, clip, scale]` | `[fit on training only]` | `[ ] Confirmed safe` |
| Categorical encodings | `[OHE, target encoding]` | `[fit on training only]` | `[ ] Confirmed safe` |
| Temporal features | `[lags, rolling means, days-since]` | `[window cutoff = prediction point]` | `[ ] Confirmed safe` |
| Interaction terms | `[A × B]` | `[justified by EDA hypothesis]` | `[ ] Confirmed safe` |
| Text / embeddings | `[TF-IDF, embeddings]` | `[fit on training only]` | `[ ] Confirmed safe` |

### 5. Hyperparameter Search Strategy

| Model | Parameters to search | Search method | Budget |
|---|---|---|---|
| `[model]` | `[key parameters]` | `[ ] Grid / [ ] Random / [ ] Bayesian` | `[n trials or time]` |

Rule: tune only after the split and metric are locked. Do not tune on the final holdout.

### 6. Stopping Criteria

Stop the experiment phase when any of the following are met:

- [ ] A model exceeds the minimum acceptable performance threshold: `[metric ≥ value]`
- [ ] Diminishing returns: last `[n]` experiments produced < `[delta]` improvement
- [ ] Experiment budget exhausted: `[n]` meaningful experiments completed
- [ ] No additional model family adds interpretable or operational value over the current leader

---

## Strong Version Additions

### Model Complexity Ladder

Commit to a principled escalation path:

> Start with `[simplest model]` → Add complexity only if it adds `[min improvement]` on `[metric]` → Cap complexity at `[family]` unless justified by further evidence.

### Non-Metric Selection Criteria

Beyond performance, document how the final model will be evaluated:

| Criterion | Weight | Notes |
|---|---|---|
| Interpretability | `[required / preferred / low priority]` | `[e.g., stakeholder requires SHAP explanations]` |
| Inference latency | `[required under X ms / not constrained]` | `[deployment context]` |
| Maintenance burden | `[low / acceptable / high — justified]` | `[retraining frequency, dependency risk]` |
| Infrastructure fit | `[must run in X]` | `[e.g., Snowflake ML / Python only / no external libs]` |

### Risk Review

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Overfitting on small training set | `[high/med/low]` | `[high]` | `[regularization, cross-validation variance check]` |
| Model instability across time folds | `[high/med/low]` | `[high]` | `[use time-based CV, check fold variance]` |
| Interpretability requirement unmet | `[high/med/low]` | `[high]` | `[constrain family to intrinsically interpretable models]` |

---

## Output Format

A short Markdown document or shared doc (1–2 pages). Does not need to be exhaustive — it exists to align the team on scope and prevent unstructured exploration.

## Quality Checks

- [ ] Candidate families are listed in order from simple to complex
- [ ] Every feature engineering step is confirmed to be fit on training data only
- [ ] Hyperparameter search method and budget are defined
- [ ] Stopping criteria are specified
- [ ] Non-metric constraints (interpretability, latency) are documented

## Common Mistakes

- Jumping to complex models without a simple baseline — baseline comes from Stage 4, not this plan
- Tuning aggressively without a clear performance ceiling to aim for
- Treating interpretability as optional until after model selection
- No stopping criteria — experiments continue indefinitely until time runs out
- Not specifying that preprocessing must be inside the validation fold

## Related Workflow Stage / Gate

- **Stage:** 5 — Model Development and Comparison
- **Gate:** Model Comparison Gate — must pass before Stage 6 (Diagnostics and Error Analysis) begins

## Related References / Checklists

- `workflow/lifecycle.md` — Stage 5 exit criteria
- `workflow/quality-gates.md` — Model Comparison Gate
- `references/model-selection-guide.md`
- `references/metrics-guide.md`
- `templates/experiment-log-template.md`
- `checklists/supervised-learning-checklist.md`
