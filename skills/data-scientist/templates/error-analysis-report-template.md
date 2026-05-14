# Error Analysis Report Template

## Purpose

Document where the selected model fails, which subgroups are most affected, what failure patterns reveal about model limitations or data quality, and whether systematic errors require remediation before deployment. Error analysis is how the project moves from "model performs well on aggregate" to "we understand where and why it fails."

## When to Use

At the end of **Stage 6: Diagnostics and Error Analysis**. Produced after the model is selected and before calibration or threshold decisions are made. Update if the model is retrained or substantially changed.

## Required Inputs

- Selected model and experiment log (Stage 5)
- Model Comparison Report (Stage 5)
- Validation set with subgroup labels
- Validation Plan (to confirm evaluation matches design)

## Minimum Contents

### 1. Report Header

- Project: `[name]`
- Report date: `[date]`
- Analyst: `[name]`
- Model evaluated: `[name / experiment ID]`
- Evaluation population: `[date range, n rows, n positive cases]`

### 2. Overall Error Distribution

**For classification:**

| | Predicted Positive | Predicted Negative |
|---|---|---|
| **Actual Positive** | TP: `[n]` | FN: `[n]` |
| **Actual Negative** | FP: `[n]` | TN: `[n]` |

- False negative rate: `[%]` — `[business interpretation: what this means operationally]`
- False positive rate: `[%]` — `[business interpretation]`
- Precision at operating threshold: `[%]`
- Recall at operating threshold: `[%]`

**For regression:**

| Metric | Value |
|---|---|
| Mean error (bias) | `[value — positive = overpredict, negative = underpredict]` |
| MAE | `[value]` |
| RMSE | `[value]` |
| 90th percentile error | `[value]` |
| Residual distribution | `[symmetric / right-skewed / left-skewed / bimodal]` |

### 3. Subgroup Performance

Evaluate performance on at least three slices. Use severity labels from `workflow/severity-levels.md` for any material degradation.

| Segment | n | Primary metric | vs. Overall | Severity | Notes |
|---|---:|---:|---|---|---|
| Overall | `[n]` | `[value]` | — | — | Reference |
| `[Segment A]` | `[n]` | `[value]` | `[+/- delta]` | `[None/Medium/High/Critical]` | `[interpretation]` |
| `[Segment B]` | `[n]` | `[value]` | `[+/- delta]` | `[None/Medium/High/Critical]` | `[interpretation]` |
| `[Time period]` | `[n]` | `[value]` | `[+/- delta]` | `[None/Medium/High/Critical]` | `[interpretation]` |

### 4. Top Error Case Review

Review the highest-error or highest-confidence-wrong predictions. Categorize each pattern:

| Pattern # | Description | Error category | n affected | Business severity | Action |
|---|---|---|---:|---|---|
| 1 | `[e.g., high-tenure customers with recent plan change]` | `[missing feature]` | `[n]` | `[High]` | `[add feature / document as limitation]` |
| 2 | `[e.g., noisy label in Q4 due to billing system change]` | `[label noise]` | `[n]` | `[Medium]` | `[exclude period / flag]` |
| 3 | `[e.g., model over-predicts for new product line]` | `[distribution shift]` | `[n]` | `[High]` | `[separate model / scope exclusion]` |

Error categories: `label noise` / `missing feature` / `model mismatch` / `data quality` / `distribution shift` / `edge case`

### 5. Systematic Error Pattern Summary

| Pattern | Root cause | Addressed? | Disposition |
|---|---|---|---|
| `[pattern]` | `[cause]` | `[ ] Yes / [ ] No` | `[fixed / accepted with justification / flagged as known risk]` |

---

## Strong Version Additions

### Fairness Slice Analysis

Complete when sensitive or protected attributes are available and applicable.

| Attribute | Group A | Group B | Disparity | Severity | Action |
|---|---|---|---|---|---|
| `[attribute]` | `[metric]` | `[metric]` | `[A-B delta or ratio]` | `[None/Medium/High/Critical]` | `[accept / mitigate / escalate]` |

Disparity threshold: document what level of disparity triggers escalation.

### Calibration Preview

Before the formal calibration report, note any obvious calibration signals:

- Score distribution: `[concentrated at extremes / spread / bimodal]`
- High-confidence errors: `[how many predictions ≥ 0.9 score are wrong?]`
- Apparent over/underconfidence: `[describe]`

### Out-of-Time or Out-of-Distribution Stability

| Evaluation period | Primary metric | vs. In-time validation | Interpretation |
|---|---|---|---|
| In-time (training window) | `[value]` | — | Reference |
| Out-of-time (most recent 90 days) | `[value]` | `[delta]` | `[stable / degraded — explain]` |
| Out-of-distribution (new market / product) | `[value]` | `[delta]` | `[stable / degraded — explain]` |

### Error-Driven Improvement Recommendations

| Finding | Recommended model change | Expected impact | Priority |
|---|---|---|---|
| `[finding]` | `[add feature X / adjust exclusion / retrain on subset]` | `[estimated]` | `[High/Medium/Low]` |

---

## Output Format

A structured document (Markdown or Word) shared with the team before calibration and threshold decisions. Attach or link to residual/confusion matrix plots. Should be readable by a technical stakeholder who was not in the modeling sessions.

## Quality Checks

- [ ] Error distribution covers the full validation population (not a subset)
- [ ] At least three subgroup slices evaluated
- [ ] Top error cases reviewed and categorized — not just counted
- [ ] Fairness analysis completed or explicitly noted as not applicable with rationale
- [ ] Systematic patterns are each given a disposition (addressed / accepted / flagged)
- [ ] Severity labels applied to subgroup degradation
- [ ] Out-of-time stability check present

## Common Mistakes

- Summarizing error analysis as "the model performs well overall" — this means the analysis was not done
- Evaluating only aggregate metrics and calling them diagnostics
- Noting error patterns without investigating them or documenting a disposition
- Skipping fairness review because "the model doesn't use protected attributes" — check proxy variables
- Not distinguishing between random errors and systematic errors

## Related Workflow Stage / Gate

- **Stage:** 6 — Diagnostics and Error Analysis
- **Gate:** Diagnostics Gate — must pass before Stage 7 (Calibration, Thresholds, Decision Policy)

## Related References / Checklists

- `workflow/lifecycle.md` — Stage 6 exit criteria
- `workflow/quality-gates.md` — Diagnostics Gate
- `workflow/severity-levels.md` — classification of findings
- `references/diagnostics-guide.md`
- `references/responsible-ai-guide.md`
- `checklists/responsible-ai-checklist.md`
- `checklists/model-audit-checklist.md`
