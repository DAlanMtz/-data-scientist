# Model Comparison Report Template

## Purpose

Communicate the results of the model development phase: which candidates were evaluated, how they compared against each other and the baseline, and why the preferred model was selected. Creates an auditable record of the selection decision.

## When to Use

At the end of **Stage 5: Model Development and Comparison**. Produced after the experiment log is complete and before diagnostics begin.

## Required Inputs

- Experiment Log (all candidate entries)
- Validation Plan (to confirm evaluation was performed as specified)
- Baseline result from Stage 4

## Minimum Contents

### 1. Report Header

- Project: `[name]`
- Report date: `[date]`
- Analyst: `[name]`
- Evaluation metric: `[primary metric]`
- Validation design: `[e.g., 5-fold time-series CV + final holdout]`
- Selected model: `[name / experiment ID]`

### 2. Baseline Reference

| Model | Description | Primary metric (validation) | Notes |
|---|---|---|---|
| Baseline | `[e.g., majority class / historical rate / simple rule]` | `[value]` | Reference for all comparisons |

### 3. Candidate Comparison Table

| Experiment ID | Model family | Key config | Primary metric | Secondary metric | CV variance | Holdout | Decision |
|---|---|---|---:|---:|---|---:|---|
| `[EXP-001]` | `[Logistic Reg]` | `[C=1, no reg]` | `[0.72]` | `[metric: val]` | `[±0.03]` | `[0.70]` | `[rejected / finalist]` |
| `[EXP-002]` | `[GBT]` | `[n=200, lr=0.05]` | `[0.78]` | `[metric: val]` | `[±0.02]` | `[0.76]` | `[selected]` |

Include every candidate evaluated. Do not omit experiments that underperformed.

### 4. Selected Model

- **Model:** `[name / experiment ID]`
- **Primary metric on holdout:** `[value]`
- **Improvement over baseline:** `[+X absolute / +Y%]`
- **CV variance:** `[±value — stable / unstable — explain]`

### 5. Selection Rationale

Beyond the primary metric, explain why this model was chosen:

| Factor | Assessment | Notes |
|---|---|---|
| Performance on holdout | `[acceptable / strong / marginal]` | `[value vs. baseline]` |
| CV stability | `[stable / variable — explain]` | `[±value]` |
| Subgroup / slice performance | `[comparable / better / worse on key slices]` | `[describe]` |
| Interpretability | `[meets requirement / acceptable / concern]` | `[SHAP available / not needed]` |
| Inference latency | `[within budget / concern]` | `[Xms average]` |
| Maintenance burden | `[low / moderate / accepted with justification]` | `[describe]` |
| Infrastructure fit | `[compatible / requires work]` | `[describe]` |

### 6. Rejected Candidates — Brief Rationale

| Experiment ID | Why rejected |
|---|---|
| `[EXP-001]` | `[underperformed baseline / unstable / failed latency requirement]` |

---

## Strong Version Additions

### Performance Summary Charts

List visuals included with one-line takeaways:

| Visual | Takeaway |
|---|---|
| Metric comparison bar chart | `[GBT outperforms logistic by 8pp recall at k=10%]` |
| CV fold variance plot | `[All candidates stable; GBT slightly lower variance]` |
| Subgroup heatmap | `[GBT performs consistently across segments; logistic degrades on segment C]` |

### Fold-Level Results

| Experiment ID | Fold 1 | Fold 2 | Fold 3 | Fold 4 | Fold 5 | Mean | Std |
|---|---:|---:|---:|---:|---:|---:|---:|
| Baseline | `[val]` | — | — | — | — | `[val]` | — |
| `[EXP-001]` | `[val]` | `[val]` | `[val]` | `[val]` | `[val]` | `[val]` | `[val]` |

### Known Risks of Selected Model

| Risk | Likelihood | Mitigation |
|---|---|---|
| `[e.g., overfits on short training windows]` | `[low/med/high]` | `[monitor temporal stability in diagnostics]` |

---

## Output Format

A structured document (Markdown, Word, or slide section) shared with the stakeholder and engineering partner before proceeding to diagnostics. Should be readable without the experiment log — include enough context that someone who was not in the experiments can understand the selection decision.

## Quality Checks

- [ ] Baseline is the first row in the comparison table
- [ ] All candidates evaluated on the same holdout, not different splits
- [ ] CV variance reported for all candidates — not only the winner
- [ ] Selection rationale includes non-metric criteria
- [ ] Rejected candidates have a documented reason
- [ ] Final holdout accessed only once per candidate — not iterated upon

## Common Mistakes

- Reporting only the winning model — rejected experiments are equally important to document
- Selecting a model based on a single aggregate metric without variance or slice checks
- Using training-set performance as the comparison metric
- Treating interpretability and latency as post-selection problems
- Holdout used multiple times during iteration — inflating apparent generalization

## Related Workflow Stage / Gate

- **Stage:** 5 — Model Development and Comparison
- **Gate:** Model Comparison Gate — must pass before Stage 6 (Diagnostics and Error Analysis)

## Related References / Checklists

- `workflow/lifecycle.md` — Stage 5 exit criteria
- `workflow/quality-gates.md` — Model Comparison Gate
- `templates/experiment-log-template.md` — source data for this report
- `references/model-selection-guide.md`
- `references/metrics-guide.md`
