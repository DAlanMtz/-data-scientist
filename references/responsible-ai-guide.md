# Responsible AI Guide

Use this guide when a model or analysis can affect people, access, pricing, eligibility, ranking, surveillance, safety, or resource allocation. Responsible AI review is practical risk control, not a compliance decoration.

## First Questions

Ask before modeling:

- Who is affected by the output?
- What action will be taken because of the model?
- Can the action harm someone financially, medically, legally, educationally, professionally, or socially?
- Is the model advisory, triage, or fully automated?
- What data about people is used, and was it collected for this purpose?
- What human appeal, override, or review path exists?
- What failure would be unacceptable even if aggregate metrics look good?

If these cannot be answered, do not recommend deployment.

## Bias

Bias can enter through:

- Historical decisions used as labels.
- Sampling that excludes relevant populations.
- Missingness that differs by group.
- Measurement error in some groups.
- Proxy variables for protected traits.
- Feedback loops from previous model or policy decisions.
- Human annotation bias.

Practical checks:

- Compare coverage, missingness, label rates, and error rates by relevant group.
- Inspect whether the target represents truth or past institutional behavior.
- Review features for proxy behavior.
- Test performance across time and segments, not just protected categories.

## Fairness

Fairness is contextual. Choose metrics with stakeholders and domain constraints.

Common checks:

- Demographic parity: selection rates by group.
- Equal opportunity: true positive rates by group.
- Equalized odds: true positive and false positive rates by group.
- Calibration by group: predicted probability matches observed outcome within group.
- Error burden: which group receives false positives or false negatives.
- Benefit allocation: who receives helpful interventions.

Do not optimize a fairness metric blindly. Some metrics conflict mathematically. State the chosen fairness goal and why it fits the decision.

## Privacy

Review:

- PII, sensitive personal data, location data, health/financial/legal data.
- Data minimization: use only fields needed for the purpose.
- Consent and permitted use.
- Retention and deletion requirements.
- Re-identification risk in aggregates, embeddings, or examples.
- Access controls for raw data, model outputs, logs, and reports.

Practical rules:

- Remove PII from modeling features unless essential and approved.
- Avoid including raw sensitive examples in reports.
- Mask or aggregate small cells.
- Log only what is necessary for audit and monitoring.

## Explainability

The explanation depth should match the decision risk.

- Low-risk internal prioritization: feature importance and examples may be enough.
- Customer-facing or high-impact decisions: provide reason codes, appeal path, and reviewable evidence.
- Regulated decisions: document method, data, limitations, validation, and governance.

Check explanations for:

- Stability across samples.
- Consistency with domain knowledge.
- Leakage or proxy features.
- Actionability for the user or operator.

Do not present feature importance as causality.

## Sensitive Variables

Sensitive variables may include protected class, age, gender, race, ethnicity, disability, religion, sexual orientation, health status, financial status, immigration status, precise location, or other domain-specific sensitive attributes.

Handling options:

- Exclude from model but use for fairness evaluation where lawful and appropriate.
- Include only when legally justified and beneficial for fairness or service quality.
- Use aggregated or transformed versions when privacy risk is lower.
- Prohibit use when the decision context makes it inappropriate.

Removing sensitive variables does not remove bias if proxies remain.

## Proxy Variables

Proxy variables can encode sensitive traits indirectly.

Examples:

- ZIP code, school, employer, language, device, purchase history, browsing behavior, income band, geography, social network, or name-derived features.

Checks:

- Correlation or predictive relationship with sensitive attributes where data is available.
- Feature importance review for proxy candidates.
- Subgroup error analysis with and without proxy features.
- Business legitimacy review: is the feature necessary and appropriate?

## Harm Assessment

Document:

- Affected groups.
- Benefits and harms.
- False positive harm.
- False negative harm.
- Automation harm.
- Privacy harm.
- Feedback loop risk.
- Misuse risk.
- Mitigations and owner.

Severity levels:

- Low: internal analysis with no individual-level action.
- Medium: prioritization or recommendation with human review.
- High: eligibility, pricing, safety, employment, credit, health, legal, education, housing, or surveillance.

High-risk uses require escalation and stronger validation.

## Human Review

Use human-in-the-loop when:

- Decisions are high-impact.
- Labels are noisy or context-heavy.
- The model flags rare events or anomalies.
- False positives or false negatives are costly.
- The model is new or not yet proven in production.

Human review must be meaningful:

- Show reason codes and evidence.
- Allow override and appeal.
- Log reviewer decisions.
- Monitor reviewer-model disagreement.
- Avoid forcing reviewers to rubber-stamp model output.

## Model Misuse And Non-Intended Uses

State intended use and prohibited use.

Common misuse:

- Using risk scores as proof of wrongdoing.
- Applying a model to a new population without validation.
- Using a descriptive segmentation as eligibility logic.
- Treating a predictive model as causal guidance.
- Reusing embeddings or text models for sensitive inference.
- Automating decisions that were designed for triage.

If a user asks for a high-risk or unsupported use, redirect to validation, governance, or safer analysis.

## High-Risk Domains

Escalate or require extra review for:

- Healthcare, mental health, and clinical decisions.
- Credit, lending, insurance, housing, employment, education, legal, immigration.
- Child safety, surveillance, biometrics, law enforcement.
- Safety-critical infrastructure or operations.
- Pricing or eligibility decisions affecting essential services.

Minimum bar:

- Clear intended use.
- Documented data provenance.
- Subgroup performance review.
- Human review and appeal path.
- Monitoring and incident plan.
- Legal/compliance review where applicable.

## Responsible Deployment Guidance

Before deployment:

- Confirm validation matches deployment population.
- Compare to baseline and current process.
- Review subgroup metrics and error examples.
- Document intended use, non-intended use, limitations, and monitoring.
- Define human override and escalation.
- Define rollback criteria.
- Confirm data and model logging are privacy-safe.

Do not deploy when:

- Performance is materially worse for a vulnerable group without mitigation.
- The model cannot be explained enough for the decision risk.
- The model uses disallowed or unjustified sensitive/proxy features.
- There is no monitoring for a consequential model.
- Users cannot challenge high-impact decisions.

## When To Refuse Or Escalate

Refuse, pause, or escalate when asked to:

- Build a model for illegal discrimination or evasion.
- Infer sensitive traits without legitimate purpose and safeguards.
- Make high-impact decisions with no validation, oversight, or appeal.
- Deploy a model known to be leaky, invalid, or unfair.
- Use private personal data beyond its permitted purpose.
- Hide model limitations, bias, or uncertainty.

Escalation language:

> I cannot recommend using this model for [decision] until [validation/fairness/privacy/human review] is addressed. The safer next step is [audit/pilot/de-identified analysis/manual review design].

