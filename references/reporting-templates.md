# Reporting Templates

Use these formats to turn analysis into decisions. Keep reports direct: answer first, evidence second, caveats clearly separated.

## Executive Summary Format

Use for senior stakeholders.

Sections:

1. Answer: one or two sentences with the decision-relevant conclusion.
2. Recommendation: what should be done now.
3. Expected impact: quantified range or directional effect.
4. Confidence: high/medium/low with reason.
5. Key evidence: three bullets maximum.
6. Risks and limitations: material caveats only.
7. Next action: owner, timing, and measurement plan.

Writing pattern:

> We recommend [action] for [population] because [evidence]. Expected impact is [range/metric], with main risk [risk]. Validate through [measurement plan].

## Notebook Narrative Format

Use for exploratory or technical notebooks.

Structure:

- Objective and decision context.
- Data sources, grain, and time window.
- Data quality checks.
- Target or outcome definition.
- EDA findings.
- Feature preparation.
- Baseline.
- Modeling or analysis.
- Validation and diagnostics.
- Interpretation.
- Limitations.
- Recommendation and next steps.

Rules:

- Put conclusions at the top of each section.
- Keep code cells reproducible and ordered.
- Avoid hidden state, manual cell execution dependencies, and unexplained constants.
- End with a plain-English summary that can stand outside the notebook.

## Technical Report Format

Use when another data scientist, analyst, or engineer must review or reproduce the work.

Sections:

- Problem statement.
- Data lineage and extraction logic.
- Unit of analysis and target definition.
- Inclusion/exclusion rules.
- Data quality summary.
- Feature definitions.
- Split and validation design.
- Baseline and candidate methods.
- Metrics and business rationale.
- Results table.
- Diagnostics and error analysis.
- Interpretation.
- Reproducibility: code path, parameters, data version, environment.
- Production or handoff notes.

Include enough detail to rerun, challenge, or extend the work.

## Stakeholder Report Format

Use for nontechnical decision makers.

Sections:

- What we analyzed.
- What we found.
- Why it matters.
- What we recommend.
- Expected tradeoffs.
- What could change the conclusion.
- What we need from stakeholders.

Writing pattern:

> The analysis suggests [finding]. This matters because [business consequence]. The practical action is [recommendation], with [tradeoff] to manage.

## Model Evaluation Report Format

Sections:

- Model purpose and intended use.
- Data and target definition.
- Validation design.
- Baseline comparison.
- Main metrics.
- Threshold or operating point.
- Segment and subgroup performance.
- Calibration if probabilities are used.
- Error analysis.
- Interpretability.
- Responsible AI review.
- Production-readiness assessment.
- Recommendation: deploy, pilot, revise, or do not use.

Required table:

| Model | Baseline? | Validation | Primary metric | Secondary metrics | Notes |
| --- | --- | --- | --- | --- | --- |
| [model] | [yes/no] | [split] | [value] | [values] | [risk/use] |

## Data Quality Report Format

Sections:

- Data sources and owners.
- Expected grain and actual row counts.
- Schema and type checks.
- Freshness and coverage.
- Missingness.
- Duplicate and key integrity.
- Range and validity checks.
- Category drift or unexpected values.
- Join match rates.
- Label quality if applicable.
- Impact on analysis/model.
- Required fixes and owners.

Severity pattern:

> Severity [high/medium/low]: [issue] affects [field/population/time]. Impact is [analysis/model risk]. Recommended fix is [action/owner].

## Findings And Recommendations Format

For each finding:

- Finding: concise statement.
- Evidence: metric, chart, test, or example.
- Interpretation: what it means.
- Recommendation: action.
- Owner: who should act.
- Measurement: how to know it worked.

Pattern:

> Finding: [segment] has [behavior]. Evidence: [metric]. Recommendation: [action], measured by [KPI] over [window].

## Limitations Format

Separate limitations by type:

- Data: missing fields, sample bias, label quality, time coverage.
- Method: assumptions, validation constraints, model class limitations.
- Operational: tooling, latency, capacity, adoption, workflow fit.
- Ethical/legal: fairness, privacy, intended use, human oversight.

Pattern:

> This result is reliable for [supported scope]. It may not generalize to [unsupported scope] because [reason].

## Next-Steps Format

Use action-oriented next steps:

| Priority | Step | Owner | Output | Due/Trigger |
| --- | --- | --- | --- | --- |
| High | [action] | [owner] | [deliverable] | [date/condition] |

Prefer fewer, owned steps over long wish lists.

## Decision Memo Format

Use when the analysis supports a go/no-go, threshold, policy, investment, or launch decision.

Sections:

1. Decision requested.
2. Recommendation.
3. Options considered.
4. Evidence summary.
5. Expected impact.
6. Risks and mitigations.
7. Implementation requirements.
8. Monitoring plan.
9. Decision owner and date.

Decision language:

> Choose [option] because it maximizes [objective] under [constraints]. The main risk is [risk], mitigated by [mitigation]. Revisit if [trigger].

