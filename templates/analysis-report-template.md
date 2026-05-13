# Analysis Report Template

Use this template for stakeholder-facing analysis reports, modeling summaries, decision memos, or professional analytic deliverables.

## Required Inputs

- Business question.
- Data sources and time window.
- Methodology.
- Key metrics, visuals, and findings.
- Limitations and decision context.

## Expected Outputs

- Clear recommendation.
- Evidence-backed findings.
- Interpretable visuals.
- Limitations and risks.
- Next steps with owners or triggers.

## Report Structure

### 1. Executive Summary

Use 3-6 bullets:

- Answer:
- Recommendation:
- Expected impact:
- Confidence:
- Main risk:
- Next action:

Pattern:

> We recommend [action] for [population] because [evidence]. Expected impact is [impact], with primary risk [risk].

### 2. Business Question

State:

- Decision being supported.
- Stakeholder.
- Population and time window.
- Success metric.
- Constraints.

### 3. Data Used

| Source | Time window | Grain | Rows | Key fields | Notes |
| --- | --- | --- | ---: | --- | --- |
| `[source]` | `[window]` | `[grain]` | `[n]` | `[keys]` | `[notes]` |

Include exclusions and quality caveats.

### 4. Methodology

Summarize:

- Data preparation.
- Feature engineering or analysis logic.
- Baseline.
- Model or statistical method.
- Validation or comparison design.
- Metrics.

Keep details enough for trust; move deep technical material to appendix.

### 5. Key Findings

For each finding:

- Finding:
- Evidence:
- Interpretation:
- Business implication:

Use numbered findings when there are multiple recommendations.

### 6. Model Performance

Include when modeling is involved:

- Baseline comparison.
- Primary and secondary metrics.
- Validation design.
- Threshold or operating point.
- Segment performance.
- Calibration if probabilities are used.
- Error analysis summary.

Skip this section for non-model EDA and replace with analysis quality checks.

### 7. Visuals To Include

Choose visuals based on report purpose:

- Data coverage or quality chart.
- Target distribution.
- Main trend or segment comparison.
- Model performance table.
- Confusion matrix or residual plot.
- Threshold tradeoff chart.
- Forecast with intervals.
- Cluster profile heatmap.
- Recommendation or alert examples.

Every visual needs a title that states the takeaway.

### 8. Interpretation

Explain:

- What the analysis means.
- What it does not mean.
- Predictive versus causal boundaries.
- Why results matter for the decision.
- Where results are strongest and weakest.

### 9. Limitations

Group by:

- Data limitations.
- Method limitations.
- Validation limitations.
- Operational limitations.
- Responsible AI/privacy limitations.

Phrase limitations as decision risk, not apology.

### 10. Recommendation

State:

- Recommended action.
- Target population.
- Threshold, segment, policy, or operating rule.
- Expected impact.
- Owner.
- Monitoring plan.

If the evidence is not strong enough, recommend a pilot, experiment, data fix, or no-go.

### 11. Next Steps

| Priority | Action | Owner | Output | Due/Trigger |
| --- | --- | --- | --- | --- |
| High | `[action]` | `[owner]` | `[deliverable]` | `[date/trigger]` |

### 12. Appendix

Include:

- Technical metric details.
- Full feature list.
- Data quality checks.
- Model parameters.
- Additional diagnostics.
- Reproducibility info.

## Validation And Evaluation Guidance

- Ensure reported metrics match the validation design.
- Include baseline and uncertainty where possible.
- Confirm visuals do not mix train/test or old/new definitions without labels.
- Verify denominators in all percentages.

## Interpretation Guidance

- Lead with decision impact.
- Avoid causal wording for predictive analysis.
- Translate model metrics into business units.
- Be explicit about unsupported uses.

## Common Failure Modes

- Executive summary restates activity instead of answer.
- Visuals included because they exist, not because they matter.
- Limitations hidden after strong claims.
- Recommendation does not name an action.
- Technical detail overwhelms the decision.

