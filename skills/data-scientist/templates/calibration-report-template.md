# Calibration Report Template

## Purpose

Document whether predicted probabilities or scores are well-calibrated, whether correction was applied, and how calibration holds across key subgroups. Calibration is separate from discrimination — a model can rank well (high AUC) but be poorly calibrated, leading to incorrect probability interpretation and threshold selection.

## When to Use

At **Stage 7: Calibration, Thresholds, and Decision Policy**. Produced before or alongside the Decision Memo. May be embedded within the Decision Memo for simpler projects. Required whenever model output is used as a probability, not just as a ranking.

## Required Inputs

- Selected model and validation set (Stage 5 / Stage 6)
- Error Analysis Report (Stage 6)
- Business context: will scores be interpreted as probabilities? Are they used for threshold-based decisions?

## Minimum Contents

### 1. Report Header

- Project: `[name]`
- Report date: `[date]`
- Analyst: `[name]`
- Model: `[name / experiment ID]`
- Calibration population: `[validation set — date range, n rows]`
- Calibration verdict: `[ ] Well-calibrated` / `[ ] Acceptable — minor bias` / `[ ] Requires correction` / `[ ] Poorly calibrated`

### 2. Calibration Assessment

**Primary method:** Reliability diagram (calibration curve)

- Number of bins: `[e.g., 10 equal-width bins]`
- Calibration curve description: `[above / below / near the diagonal; over/underconfident in which score range]`

| Score bin | Mean predicted score | Observed positive rate | n in bin | Deviation from perfect |
|---|---:|---:|---:|---|
| 0.0–0.1 | `[mean]` | `[rate]` | `[n]` | `[+/- delta]` |
| 0.1–0.2 | `[mean]` | `[rate]` | `[n]` | `[+/- delta]` |
| … | | | | |
| 0.9–1.0 | `[mean]` | `[rate]` | `[n]` | `[+/- delta]` |

**Summary metrics:**

| Metric | Value | Interpretation |
|---|---|---|
| Expected Calibration Error (ECE) | `[value]` | `[well-calibrated < 0.05 / concern 0.05–0.10 / poor > 0.10]` |
| Brier Score | `[value]` | `[lower is better; compare to baseline Brier score]` |
| Baseline Brier Score | `[value]` | `[majority class prediction Brier score]` |

### 3. Calibration Correction

- Correction applied: `[ ] Yes — method: [Platt Scaling / Isotonic Regression / Beta Calibration / Temperature Scaling]` / `[ ] No — not needed`
- If applied:
  - Fitted on: `[calibration fold — separate from training and holdout]`
  - Post-correction ECE: `[value]`
  - Post-correction Brier Score: `[value]`
  - Reliability diagram comparison: `[description of improvement]`

### 4. Calibration Verdict and Business Implication

| Score range | Pre-correction | Post-correction | Business meaning |
|---|---|---|---|
| Low (0.0–0.3) | `[over/underestimates by X%]` | `[corrected to within Y%]` | `[Threshold actions in this range: describe]` |
| Mid (0.3–0.7) | `[over/underestimates by X%]` | `[corrected to within Y%]` | `[describe]` |
| High (0.7–1.0) | `[over/underestimates by X%]` | `[corrected to within Y%]` | `[describe]` |

---

## Strong Version Additions

### Subgroup Calibration

Calibration may hold overall but fail for key segments.

| Segment | ECE | Verdict | Notes |
|---|---|---|---|
| Overall | `[value]` | `[good/concern/poor]` | — |
| `[Segment A]` | `[value]` | `[good/concern/poor]` | `[worse than overall — describe]` |
| `[Segment B]` | `[value]` | `[good/concern/poor]` | `[describe]` |

### Calibration Over Time

For models with temporal data, confirm calibration stability across time periods:

| Period | ECE | Verdict |
|---|---|---|
| Training period (Q1–Q3 2023) | `[value]` | `[stable]` |
| Holdout period (Q4 2023) | `[value]` | `[stable / degraded — explain]` |

### Discrimination vs. Calibration Tradeoff

Note if calibration correction affected discrimination:

| Metric | Pre-correction | Post-correction | Change |
|---|---|---|---|
| AUC / Gini | `[value]` | `[value]` | `[unchanged / slight change]` |
| ECE | `[value]` | `[value]` | `[improved]` |

---

## Output Format

A structured document (Markdown or Word) with the calibration curve plot attached or embedded. May be combined with the Decision Memo for smaller projects. Keep brief — this report answers one question: "Can we trust these probabilities?"

## Quality Checks

- [ ] Calibration curve produced with labeled bins
- [ ] ECE or equivalent metric calculated
- [ ] Verdict is explicit — not left as "it looks mostly okay"
- [ ] If correction applied, correction was fit on a held-out calibration fold (not training data)
- [ ] Post-correction curve is shown and compared to pre-correction
- [ ] At least one subgroup calibration check performed

## Common Mistakes

- Reporting only AUC/F1 and assuming calibration is good — discrimination and calibration are independent
- Fitting the calibration correction on training data — reintroduces overfitting
- Reporting calibration only on the full population when key subgroups may diverge
- Skipping calibration entirely for non-probability outputs — even scores used for ranking benefit from a monotonic calibration check
- Treating "mostly near the diagonal" as sufficient without quantifying the deviation

## Related Workflow Stage / Gate

- **Stage:** 7 — Calibration, Thresholds, and Decision Policy
- **Gate:** Calibration/Decision Gate — must pass before Stage 8 (Interpretation and Reporting)

## Related References / Checklists

- `workflow/lifecycle.md` — Stage 7 exit criteria
- `workflow/quality-gates.md` — Calibration/Decision Gate
- `references/metrics-guide.md` — calibration and threshold sections
- `references/diagnostics-guide.md`
- `templates/decision-memo-template.md` — companion artifact
