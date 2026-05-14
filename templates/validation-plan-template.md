# Validation Plan Template

## Purpose

Lock in the target definition, feature construction rules, split strategy, baseline approach, and evaluation metrics before any modeling code is written. The validation plan is the single most important pre-modeling document — it prevents leakage, invalid comparisons, and the most common and most expensive data science errors.

## When to Use

At the end of **Stage 3: Target, Feature, and Validation Design**. The plan is finalized *before* any model is trained. Changes after modeling begins must be documented, justified, and version-stamped — not silently incorporated.

## Required Inputs

- Project Brief (Stage 0)
- Data Audit (Stage 1)
- EDA Summary (Stage 2)
- Business cost-of-error information from the stakeholder

## Minimum Contents

### 1. Plan Header

- Project: `[name]`
- Plan version: `[v1.0]`
- Date: `[date]`
- Analyst: `[name]`
- Status: `[ ] Draft` / `[ ] Final — locked for modeling`

### 2. Target Definition

| Element | Specification |
|---|---|
| Target name | `[column or derived variable name]` |
| Business definition | `[plain-language description of what a positive/high value means]` |
| Technical definition | `[exact logic — e.g., churned_30d = 1 if subscription.end_date is within 30 days of scoring_date]` |
| Outcome window | `[e.g., 30 days after the prediction point]` |
| Positive class | `[what positive / high means in business terms]` |
| Label source | `[which table/field/event drives the label]` |
| Known label limitations | `[delay, noise, ambiguous cases, exclusions]` |
| Exclusions from target population | `[e.g., trial accounts, first-month subscribers, fraud-flagged]` |

### 3. Prediction Point

| Element | Specification |
|---|---|
| Prediction timestamp column | `[field name]` |
| Prediction timing | `[e.g., first day of each month at 00:00 UTC]` |
| Lag from event to data availability | `[e.g., 2-day lag on transaction data]` |
| Feature window cutoff | `[all features must be derived from data before this timestamp]` |
| Confirmed: no features use data after prediction point | `[ ] Yes — confirmed` / `[ ] No — exceptions: [list]` |

### 4. Feature List

| Feature | Source table/field | Available at prediction point | Leakage risk | Notes |
|---|---|---|---|---|
| `[feature name]` | `[source]` | `[ ] Yes / [ ] No` | `[ ] None / [ ] Review` | `[notes]` |

Flag any feature where availability is conditional or uncertain.

### 5. Split Strategy

| Element | Decision |
|---|---|
| Split type | `[ ] Random` / `[ ] Time-based` / `[ ] Group-based` / `[ ] Stratified` / `[ ] Combined` |
| Rationale | `[why this split type is appropriate for this data and deployment scenario]` |
| Training period | `[date range or row selection logic]` |
| Validation / CV design | `[e.g., 5-fold time-series CV with 3-month folds; or random 80/20]` |
| Final holdout | `[date range or selection rule — touched only once, at final evaluation]` |
| Group key (if group-based) | `[e.g., customer_id — no customer appears in both train and test]` |

### 6. Baseline Strategy

| Element | Specification |
|---|---|
| Baseline type | `[ ] Majority class` / `[ ] Historical rate` / `[ ] Simple rule` / `[ ] Current process` / `[ ] Linear/logistic model` |
| Baseline definition | `[exact description — e.g., predict positive for any customer with tenure < 90 days]` |
| Uses only permissible features | `[ ] Confirmed` |
| Evaluation: same split as candidates | `[ ] Confirmed` |

### 7. Evaluation Metrics

| Metric | Primary / Secondary | Formula or definition | Business rationale |
|---|---|---|---|
| `[metric]` | `[ ] Primary` / `[ ] Secondary` | `[formula]` | `[why this metric reflects business cost]` |

Include at minimum: one primary metric with business rationale. For classification: specify whether accuracy, AUC, precision, recall, F1, or a cost-weighted metric is primary and why. For regression: specify MSE, MAE, RMSE, MAPE, or custom. For forecasting: specify naive baseline metric.

---

## Strong Version Additions

### Feature-by-Feature Availability Audit

For each feature, document the exact availability check:

| Feature | Availability evidence | Conditional availability? | Handling if unavailable |
|---|---|---|---|
| `[feature]` | `[query / log / data contract]` | `[always / sometimes — when?]` | `[impute / exclude / fallback]` |

### Pre-Registered Hypotheses for Model Comparison

List what you expect to find in modeling, so results can be evaluated against prior expectations:

| Hypothesis | Expected result | What would falsify it |
|---|---|---|
| `[hypothesis]` | `[expected metric or pattern]` | `[what outcome would contradict it]` |

### Cost-of-Error Framework

| Error type | Business cost | Cost asymmetry ratio | Implication for metric |
|---|---|---|---|
| False positive | `[cost — e.g., wasted retention offer: $5]` | `FP:FN = [ratio]` | `[e.g., use recall-weighted F-beta]` |
| False negative | `[cost — e.g., missed churner: $200 LTV]` | — | — |

### Holdout Protection Rules

- The final holdout set is not to be examined, profiled, or used in any way until the final model evaluation
- Holdout set defined as: `[exact selection rule]`
- Holdout is protected: `[ ] Confirmed — analyst has not accessed it`

---

## Output Format

A written document (Markdown or shared doc) circulated to the team before modeling begins. The validation plan is versioned. If it must be changed after modeling starts, the new version is dated and the change is explained.

## Quality Checks

- [ ] Target definition is written out in full — not a field name only
- [ ] Prediction point is a specific timestamp, not "when the data is available"
- [ ] Every feature in the list has an availability confirmation
- [ ] Split strategy matches the deployment scenario (time-based if predicting the future)
- [ ] Baseline is defined and will use the same split as candidate models
- [ ] Primary metric has a business rationale, not just a technical one
- [ ] Holdout set is defined and protection rules are stated

## Common Mistakes

- Writing "churn" as the target definition — the full definition includes event, grain, outcome window, and exclusions
- Omitting the prediction point — allows features to silently include future information
- Using a random split on time-series data because it is the default
- Choosing accuracy as the metric without checking class imbalance
- Defining the baseline after seeing candidate model results

## Related Workflow Stage / Gate

- **Stage:** 3 — Target, Feature, and Validation Design
- **Gate:** Validation Gate — must pass before Stage 4 (Baseline Modeling) begins

## Related References / Checklists

- `workflow/lifecycle.md` — Stage 3 exit criteria
- `workflow/quality-gates.md` — Validation Gate pass requirements
- `checklists/pre-modeling-checklist.md` — full pre-modeling review
- `references/validation-and-leakage-checklist.md`
- `references/metrics-guide.md`
