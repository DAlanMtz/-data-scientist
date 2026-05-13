# Experiment Log Template

Use this template to track modeling, feature, validation, and analysis experiments so comparisons stay fair and reproducible.

## When To Use

Use for any project with multiple model runs, feature sets, thresholds, validation designs, or analytic approaches. It can be implemented as Markdown, a spreadsheet, a notebook table, a database table, or an experiment tracker.

## Required Inputs

- Business question.
- Dataset and target definition.
- Validation split.
- Feature set.
- Model/method choices.
- Primary and secondary metrics.

## Expected Outputs

- Comparable experiment records.
- Decision history.
- Reproducibility trail.
- Follow-up action list.

## Experiment Record

| Field | Value |
| --- | --- |
| Experiment ID | `[EXP-YYYYMMDD-###]` |
| Date | `[date]` |
| Owner | `[person/agent]` |
| Business question | `[decision or question]` |
| Hypothesis | `[what this run tests]` |
| Dataset version | `[snapshot/query/file hash/partition]` |
| Target version | `[target definition and outcome window]` |
| Train/test split | `[split type, seed/cutoff/group key]` |
| Feature set | `[feature set ID and summary]` |
| Model/method | `[method name]` |
| Hyperparameters | `[key parameters]` |
| Preprocessing | `[imputation, encoding, scaling, text/vector steps]` |
| Metrics | `[primary and secondary metrics]` |
| Error analysis notes | `[main failure modes]` |
| Responsible-use notes | `[fairness/privacy/proxy concerns]` |
| Decision | `[keep/reject/revise/promote/investigate]` |
| Follow-up actions | `[next steps and owner]` |

## Comparison Table

| Experiment ID | Data | Split | Feature set | Method | Primary metric | Secondary metrics | Decision | Notes |
| --- | --- | --- | --- | --- | ---: | --- | --- | --- |
| `[id]` | `[version]` | `[split]` | `[features]` | `[method]` | `[value]` | `[values]` | `[decision]` | `[notes]` |

## Step-By-Step Workflow

1. Register the baseline before advanced experiments.
2. Record dataset, target, split, and feature set before running.
3. Run model or analysis.
4. Log metrics and diagnostics.
5. Add error analysis notes.
6. Decide whether the run changes the project direction.
7. Record follow-up actions.
8. Keep rejected experiments; they prevent repeated dead ends.

## Validation And Evaluation Guidance

- Do not compare runs with different splits unless the difference is the experiment.
- Keep final test results separate from validation experiments.
- Record metric variance across folds or windows.
- Include baseline in every comparison table.
- Mark any run with known leakage or invalid validation as invalid.

## Interpretation Guidance

- Add a one-sentence interpretation for each experiment.
- Explain why a metric change matters or does not matter.
- Note operational cost, interpretability, and production risk.
- Prefer clear decisions over raw metric lists.

## Common Failure Modes

- Hyperparameters recorded but data version omitted.
- Feature set changes silently.
- Test set used during iteration.
- Only successful experiments logged.
- No baseline.
- Metrics logged without error analysis.

## Tool-Flexible Notes

- Python/R: write logs to CSV, JSON, MLflow, W&B, or Markdown.
- SQL: store experiment metadata in a table for pipeline runs.
- Excel/Sheets: useful for small project comparison logs.
- Notebooks: maintain an experiment summary table near the top or bottom.
- Production pipelines: attach run IDs to model artifacts and monitoring records.

