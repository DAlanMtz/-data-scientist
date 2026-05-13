# Decision Science Guide

Use this guide to turn analysis, forecasts, scores, and model outputs into decisions. A model is only useful if it changes action in a measurable, responsible way.

## Turning Predictions Into Actions

For every prediction, define:

- Who receives the output.
- What action they can take.
- When the action happens.
- What capacity or budget limits action.
- What false positives and false negatives cost.
- How the action outcome will be measured.
- When the decision rule will be reviewed.

If no action changes, the model is reporting, not decisioning.

## Threshold Setting

Use thresholds when a score triggers action.

Inputs:

- Score distribution.
- True positive value.
- False positive cost.
- False negative cost.
- Capacity.
- Risk tolerance.
- Fairness or policy constraints.
- Calibration quality.

Methods:

- Choose threshold by expected value.
- Choose threshold by fixed capacity: top `k` or top percentile.
- Choose threshold by required precision or recall.
- Choose separate thresholds by segment only when justified, legal, and monitored.
- Use human review bands: auto-approve, review, auto-decline/no-action.

Never use default 0.5 unless it is justified.

## Ranking And Prioritization

Use ranking when the business can act on only some cases.

Questions:

- What is the ranked unit: customer, lead, alert, claim, product, task?
- What is the capacity per day/week/team?
- Is the score probability, expected value, severity, urgency, or a composite?
- Are there must-include or must-exclude rules?
- How are ties handled?

Metrics:

- Precision@k.
- Recall@k.
- Lift@k.
- Expected value at capacity.
- Coverage and fairness guardrails.

Rank by expected decision value when value differs across cases, not only probability.

## Cost-Benefit Analysis

Create a cost table:

| Outcome | Business meaning | Value/cost |
| --- | --- | --- |
| True positive | Correct action on real opportunity/risk | [value] |
| False positive | Action taken unnecessarily | [cost] |
| False negative | Missed opportunity/risk | [cost] |
| True negative | Correct no-action | [value/cost] |

Include:

- Labor cost.
- Customer experience cost.
- Delay cost.
- Opportunity cost.
- Risk/reputation/legal cost.
- Intervention cost.
- Downstream operational constraints.

When exact costs are unknown, use scenario ranges.

## Resource Allocation

Use when deciding how to distribute limited budget, staff, inventory, support, outreach, or capacity.

Steps:

1. Define objective.
2. Define resources and constraints.
3. Estimate benefit or risk by option.
4. Account for uncertainty.
5. Apply policy constraints.
6. Simulate outcomes under alternatives.
7. Select allocation and monitor impact.

Avoid allocating solely by model score when action cost or potential value varies.

## Optimization

Use optimization when there are many possible actions and constraints.

Common approaches:

- Linear programming.
- Integer programming.
- Constraint programming.
- Greedy heuristics.
- Simulation optimization.
- Contextual bandits for sequential learning when appropriate.

Define:

- Decision variables.
- Objective function.
- Constraints.
- Inputs and uncertainty.
- Feasible fallback.
- Review process.

Validate optimization outputs with domain review. A mathematically optimal answer can violate unstated business rules.

## Scenario Analysis

Use scenarios when assumptions are uncertain.

Examples:

- Best/base/worst case.
- Low/medium/high demand.
- Different cost ratios.
- Different capacity levels.
- Different adoption rates.
- Different model thresholds.

Report:

- Which decisions are robust across scenarios.
- Which assumptions change the recommendation.
- Break-even points.

## Sensitivity Analysis

Use sensitivity analysis to identify fragile conclusions.

Vary:

- Cost assumptions.
- Thresholds.
- Forecast inputs.
- Conversion rates.
- Treatment effects.
- Capacity.
- Drift assumptions.
- Data quality assumptions.

If a recommendation changes under small plausible changes, communicate that and prefer pilot testing or reversible actions.

## Business Constraints

Common constraints:

- Budget.
- Staff capacity.
- Inventory or supply.
- SLA or latency.
- Legal/policy rules.
- Fairness rules.
- Customer contact limits.
- Geography or territory ownership.
- Minimum service levels.
- Dependencies between actions.

Encode hard constraints explicitly. Do not bury them in post-hoc manual adjustment.

## Human-In-The-Loop Decisioning

Use when decisions are high-impact, uncertain, or context-heavy.

Patterns:

- Triage: model prioritizes, human decides.
- Review band: model automates low-risk cases and escalates uncertain cases.
- Second opinion: model flags possible issue for expert review.
- Override workflow: human can override with reason.

Track:

- Model recommendation.
- Human action.
- Override reason.
- Outcome.
- Disagreement rate.
- Reviewer workload and latency.

Human review must improve decisions, not just shift responsibility.

## Measuring Decision Impact

Measure the decision, not only the model.

Track:

- Action rate.
- Acceptance or override rate.
- Outcome rate.
- Incremental lift against control or baseline.
- Cost and benefit.
- Customer or user impact.
- Guardrail metrics.
- Operational workload.
- Fairness and subgroup effects.

Use experiments or holdouts when possible. If not, compare carefully against historical or matched baselines and state limitations.

## When A Model Is Not Needed

Do not build a model when:

- A simple rule solves the decision well.
- The action is not defined.
- The data is too poor for reliable prediction.
- The outcome cannot be measured.
- The cost of errors is unacceptable without human review.
- The decision requires causal evidence but only predictive data exists.
- The operational process cannot use the output.
- A dashboard, query, experiment, or process fix answers the need better.

Recommended language:

> A model is not the best next step. The decision would be better served by [data quality fix/rule/dashboard/experiment/process change] because [reason].

## Decision Handoff

A decision-ready handoff includes:

- Recommended action or policy.
- Target population.
- Score, threshold, ranking, or rule.
- Expected impact and uncertainty.
- Required resources.
- Risks and mitigations.
- Monitoring metrics.
- Review trigger.
- Owner.

End with a concrete decision, not only model performance.

