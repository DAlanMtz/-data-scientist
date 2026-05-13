# Responsible AI Checklist

Use for any analysis or model that affects people, access, ranking, eligibility, pricing, enforcement, safety, opportunity, or resource allocation.

## Intended And Non-Intended Use

- [ ] Intended use is stated.
- [ ] Intended users are identified.
- [ ] Affected population is defined.
- [ ] Action taken from output is described.
- [ ] Non-intended uses are documented.
- [ ] Automation level is clear: advisory, triage, or automated decision.
- [ ] Use outside validated population is prohibited or requires review.

## Sensitive And Proxy Variables

- [ ] Sensitive/protected variables are identified.
- [ ] Sensitive variables are excluded, included, or used for audit with explicit rationale.
- [ ] Proxy variables are reviewed.
- [ ] Geography, language, device, school, employer, income, names, or behavior proxies are considered.
- [ ] Feature importance is reviewed for proxy risk.
- [ ] Sensitive/proxy handling is documented.

## Bias And Fairness

- [ ] Coverage is checked by relevant subgroup.
- [ ] Missingness is checked by subgroup.
- [ ] Label rates are checked by subgroup.
- [ ] Error rates are checked by subgroup.
- [ ] Selection/action rates are checked where relevant.
- [ ] Calibration by group is checked when probabilities are used.
- [ ] Fairness metric choice is justified for the decision.
- [ ] Mitigation is proposed for material disparate impact.

## Privacy, Consent, And Data Rights

- [ ] PII and sensitive data are identified.
- [ ] Data use matches consent and permitted purpose.
- [ ] Data minimization is applied.
- [ ] Retention policy is documented.
- [ ] Access controls are defined.
- [ ] Reports avoid unnecessary raw personal data.
- [ ] Logs avoid unnecessary sensitive data.
- [ ] Embeddings or derived features are reviewed for privacy risk.

## Explainability And Transparency

- [ ] Explanation depth matches decision risk.
- [ ] Operators can understand score meaning.
- [ ] Reason codes or local explanations exist when needed.
- [ ] Feature importance is not presented as causality.
- [ ] Limitations are documented in stakeholder-ready language.
- [ ] Users or reviewers have enough context to challenge output.

## Human Oversight

- [ ] Human review is required for high-impact decisions.
- [ ] Reviewer sees evidence or reason codes.
- [ ] Override path exists.
- [ ] Appeal or correction path exists where appropriate.
- [ ] Reviewer decisions are logged.
- [ ] Automation bias risk is considered.
- [ ] Model is not used as proof of wrongdoing without investigation.

## High-Risk Domain Review

- [ ] Domain is checked for high-risk status: health, credit, insurance, housing, employment, education, legal, immigration, safety, surveillance, biometrics, children, or essential services.
- [ ] Legal/compliance/risk review is triggered where needed.
- [ ] Additional validation and monitoring are required for high-risk use.
- [ ] Human appeal path is defined.
- [ ] Deployment is blocked if review is incomplete.

## Harm Assessment

- [ ] False positive harms are documented.
- [ ] False negative harms are documented.
- [ ] Privacy harms are documented.
- [ ] Group harms are documented.
- [ ] Feedback loop harms are documented.
- [ ] Misuse and abuse risks are documented.
- [ ] Mitigations and owners are assigned.

## Monitoring For Disparate Impact

- [ ] Subgroup performance monitoring is defined where feasible.
- [ ] Selection/action rate monitoring is defined.
- [ ] Drift in population mix is monitored.
- [ ] Complaint, appeal, override, or harm signals are monitored.
- [ ] Monitoring owner and escalation path are defined.

## Documentation

- [ ] Intended use and non-intended use are documented.
- [ ] Data sources and limitations are documented.
- [ ] Sensitive/proxy review is documented.
- [ ] Fairness/subgroup results are documented.
- [ ] Privacy decisions are documented.
- [ ] Human oversight and appeal process are documented.
- [ ] Approval status is documented.

## Escalation Or Refusal Conditions

- [ ] Request involves illegal discrimination or evasion.
- [ ] Request infers sensitive traits without legitimate purpose and safeguards.
- [ ] High-impact automated decision lacks validation or review.
- [ ] Model is known to be leaky, invalid, or materially unfair.
- [ ] Private data use exceeds permitted purpose.
- [ ] User asks to hide limitations, bias, or uncertainty.

If any checked condition applies, refuse, pause, or escalate rather than proceed.

## Minimum Acceptable Standard

- [ ] Intended use, affected population, sensitive/proxy review, privacy review, fairness/error review, human oversight, and documentation are complete for consequential use.

## Strong Practice

- [ ] Responsible-use review is completed before model selection is finalized.
- [ ] Model card includes non-intended use, harms, and monitoring plan.
- [ ] Post-deployment monitoring includes subgroup and appeal/override signals.

## Red Flags

- [ ] "We removed protected attributes, so bias is solved."
- [ ] Model affects people but has no human review or appeal path.
- [ ] Sensitive text/location/behavior data is used without purpose review.
- [ ] High-risk domain deployment has no compliance review.
- [ ] Feature importance is used to justify causal or policy claims.

