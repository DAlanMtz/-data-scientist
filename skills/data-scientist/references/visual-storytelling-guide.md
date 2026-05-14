# Visual Storytelling Guide

Use this guide to turn analysis into a visual narrative for stakeholders. The goal is not to show all the work. The goal is to help the audience make the next decision with appropriate confidence.

## Audience And Decision First

Before choosing charts, answer:

- Who is the audience?
- What decision or action does this deliverable support?
- What do they already know?
- What tradeoff, uncertainty, or risk must they understand?
- What action should they take after reading or using it?

If no decision or action is defined, produce a visual analysis plan or EDA summary rather than a stakeholder report.

## Headline Finding

Write the headline before building the final chart sequence.

Good headline:

- States the finding in business language.
- Names the affected population or segment.
- Includes direction and magnitude when possible.
- Avoids causal language unless the design supports causality.

Weak headline:

- Names a method or chart type.
- Says "interesting pattern" without an implication.
- Overstates certainty from exploratory or observational data.

## Chart Sequence

Use a sequence that builds the decision:

1. **Context:** scope, population, denominator, time window.
2. **Status:** what is happening now versus target, baseline, or prior period.
3. **Driver or segment:** where the pattern is concentrated.
4. **Tradeoff or uncertainty:** risk, variance, confidence interval, forecast interval, or sensitivity.
5. **Recommendation:** what should change next.
6. **Appendix:** method, diagnostics, robustness checks, detailed tables.

Do not sequence charts by the order they were created. Sequence them by the order the audience needs to reason.

## Supporting Detail

Use supporting visuals to answer specific follow-up questions:

- Where is the problem concentrated?
- Is the pattern stable over time?
- Is the finding robust to denominator, filter, or sample changes?
- What is the cost of each option?
- What uncertainty changes the decision?

Move supporting detail to the appendix if it validates the finding but does not change the main decision.

## Uncertainty And Limitations

Show uncertainty when it affects action:

- Confidence intervals or bootstrap intervals for small samples.
- Forecast intervals for future values.
- Error bands or variability across folds for model performance.
- Sample size labels for subgroup comparisons.
- Data freshness, missingness, or coverage caveats.

Do not bury limitations after a strong recommendation if the limitation could reverse the decision.

## Recommendation

A visual recommendation should include:

- Recommended action.
- Evidence that supports it.
- Expected impact or tradeoff.
- Assumptions and risks.
- Owner or next action.
- Measurement plan, if the action should be evaluated.

Avoid recommendations that only say "monitor" unless monitoring has a metric, threshold, owner, and cadence.

## Appendix And Detail Separation

Main report:

- Decision, answer, evidence, risk, recommendation.
- Few charts with strong captions.
- Only the detail needed to trust the conclusion.

Appendix:

- Data definitions.
- Method details.
- Sensitivity checks.
- Diagnostic charts.
- Full metric tables.
- Data quality checks.

## Dashboard Vs Report Storytelling

Reports tell a fixed story:

- Best for one-time decisions, executive summaries, project readouts, and published findings.
- Use a deliberate sequence and captions.
- Prioritize a clear recommendation.

Dashboards support repeated decisions:

- Best for monitoring, operations, drilldowns, and recurring decision cadence.
- Prioritize current status, trend, exceptions, and next action.
- Provide filters and drilldowns only when they support user workflows.

Do not force a dashboard to behave like a report or a report to carry every operational drilldown.

## Caption Writing

Use captions as takeaways:

> [Metric] changed by [amount] for [population] during [period], which means [decision implication]. Caveat: [uncertainty or limitation].

Caption checks:

- Does it state the insight?
- Does it define the denominator or population?
- Does it avoid causal overclaiming?
- Does it tell the viewer what to notice?
- Does it mention uncertainty if relevant?

## Executive Summary Visuals

Use only visuals that answer the executive decision:

- KPI cards with baseline/target and trend.
- Ranked bars for prioritization.
- Simple time trend with annotated event.
- Waterfall or bridge chart for contribution analysis when appropriate.
- Threshold/cost curve for policy decisions.
- Forecast with interval when planning capacity or demand.

Avoid dashboards-in-miniature on executive summary pages.

## Common Storytelling Mistakes

- Starting with method details instead of the decision.
- Showing every chart created during EDA.
- Hiding the main conclusion until the end.
- Using captions that only repeat axis labels.
- Mixing exploratory and final claims without labeling them.
- Overclaiming causality from predictive models.
- Omitting uncertainty, sample size, or denominator.
- Letting dashboard filters change metric meaning silently.
- Presenting a recommendation without an owner, threshold, or next action.
