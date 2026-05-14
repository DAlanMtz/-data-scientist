# Causal Versus Predictive Guide

Use this guide whenever analysis could be interpreted as "what causes what" or "what should we change."

## Prediction Versus Causation

Prediction asks:

- Given current information, what is likely to happen?
- Which cases should be prioritized?
- What score, forecast, or ranking is most accurate?

Causation asks:

- What will happen if we intervene?
- Did this policy, campaign, product change, or treatment cause the outcome?
- Which action should we choose to change the outcome?

A predictive model can be useful without being causal. A causal analysis can be valuable even when predictive accuracy is modest.

## Correlation Versus Causation

Correlation means variables move together. It can arise from:

- Direct causal effect.
- Reverse causation.
- Common cause/confounding.
- Selection bias.
- Measurement artifact.
- Time trend.
- Leakage.
- Random chance.

Do not recommend changing a feature just because it is correlated with the target.

## Feature Importance Is Not Causality

Feature importance means a variable helped prediction under the model and data.

It does not prove:

- The feature causes the outcome.
- Changing the feature will change the outcome.
- The feature is fair or appropriate to act on.
- The feature is stable in a new policy environment.

Safe phrasing:

> [Feature] is a strong predictor of [outcome].

Unsafe phrasing:

> Increasing [feature] will increase [outcome].

## When Causal Claims Are Invalid

Do not make causal claims when:

- Treatment was self-selected and confounding is unaddressed.
- Important pre-treatment covariates are missing.
- Post-treatment variables are controlled for.
- Outcome timing is ambiguous.
- Treated and comparison groups are not comparable.
- Pre-trends differ in difference-in-differences.
- Instrument validity is not credible.
- Regression discontinuity has manipulation around cutoff.
- A predictive model was trained only for accuracy.

If causal validity is weak, report association and recommend experiment or stronger design.

## A/B Testing

Use when treatment can be randomized.

Requirements:

- Clear unit of randomization.
- Stable treatment assignment.
- Predefined primary metric and guardrails.
- Power or minimum detectable effect.
- No major interference between units.
- Consistent exposure logging.
- Predefined analysis window.

Report:

- Treatment effect.
- Confidence interval.
- Practical significance.
- Guardrail impact.
- Sample and exclusions.

A/B tests are usually strongest for causal claims when implemented correctly.

## Matching

Use when treatment is observational and comparable untreated units exist.

Steps:

- Define treatment timing.
- Use only pre-treatment covariates.
- Estimate propensity or match on key covariates.
- Check balance after matching.
- Estimate treatment effect on matched sample.
- State that unobserved confounding may remain.

Avoid matching on post-treatment outcomes or mediators.

## Difference-In-Differences

Use when treated and comparison groups are observed before and after an intervention.

Requirements:

- Plausible parallel trends before treatment.
- Clear intervention timing.
- No simultaneous confounding intervention.
- Stable composition or accounted composition changes.

Diagnostics:

- Pre-trend plot.
- Event study if multiple periods exist.
- Placebo tests where possible.

Report assumptions prominently.

## Instrumental Variables

Use when an external source of variation affects treatment but not outcome except through treatment.

Instrument requirements:

- Relevance: instrument predicts treatment.
- Exclusion: instrument affects outcome only through treatment.
- Independence: instrument is not related to unobserved confounders.

IV is fragile. Do not use it unless the instrument story is credible and tested where possible.

## Regression Discontinuity

Use when treatment assignment changes at a cutoff.

Requirements:

- Clear cutoff rule.
- No manipulation around cutoff.
- Units near cutoff are comparable.
- Enough observations near cutoff.

Diagnostics:

- Outcome plot around cutoff.
- Covariate balance around cutoff.
- Density test around cutoff.
- Sensitivity to bandwidth.

Interpret effect as local to the cutoff.

## Natural Experiments

Use when external events create as-if random variation.

Examples:

- Policy rollout.
- Geographic boundary.
- System outage.
- Eligibility rule.
- Random assignment by queue or capacity.

Validate:

- Assignment mechanism.
- Timing.
- Who was affected.
- Whether other changes happened at the same time.
- Whether results generalize beyond affected units.

## Causal Language Guardrails

Use:

- "is associated with"
- "predicts"
- "is correlated with"
- "is higher among"
- "the model uses"
- "under this experimental design, we estimate the effect"

Avoid unless design supports it:

- "causes"
- "drives"
- "leads to"
- "increases"
- "reduces"
- "because of"

When reporting causal estimates, name the design and assumptions.

## How To Phrase Predictive Findings Safely

Predictive:

> Customers with [feature] have higher predicted risk of [outcome]. This helps prioritize [action], but it does not prove that changing [feature] will reduce risk.

Segment:

> Segment [A] has higher observed [outcome] than segment [B]. The difference may reflect [confounders], so use this for targeting or further study, not causal attribution.

Model importance:

> [Feature] was one of the strongest contributors to model performance. Before using it as a policy lever, test whether it is causal, actionable, and appropriate.

Recommendation:

> If the business goal is to change [outcome], run [experiment/design] to estimate the effect of [intervention].

