# Monitoring Plan Template

## Purpose

Define how the deployed model will be observed, what degradation looks like, what actions are taken when issues are detected, and when the model will be retrained or retired. Monitoring is how the project remains honest after deployment — it operationalizes the assumption that model performance does not stay constant.

## When to Use

**Draft** at the end of **Stage 9: Deployment Readiness** as part of the production sign-off. **Activate** at the start of **Stage 10: Monitoring and Iteration**. Update when the model, data pipeline, or business context changes materially.

## Required Inputs

- Deployment Readiness Report (Stage 9)
- Model Card (Stage 8)
- Decision Memo (Stage 7) — to understand which metrics matter operationally
- Business outcome data: what downstream events will be observable after scoring?

## Minimum Contents

### 1. Plan Header

- Project: `[name]`
- Plan version: `[v1.0]`
- Date: `[date]`
- Analyst / owner: `[name]`
- Model: `[name / version]`
- Monitoring start date: `[date]`
- Review cadence: `[daily / weekly / monthly — depends on deployment frequency and risk level]`

### 2. Monitoring Metric Registry

Define at minimum one metric per category below. Add more based on risk and deployment frequency.

#### Data Quality Metrics

| Metric | Definition | Alert threshold | Alert owner | Cadence |
|---|---|---|---|---|
| Input row count | `[rows in scoring population vs. expected]` | `[< X% of expected → alert]` | `[person]` | `[each run]` |
| Key field missingness | `[null rate for field Y]` | `[> X% → alert]` | `[person]` | `[each run]` |
| Schema validation | `[all required fields present and typed correctly]` | `[any failure → alert]` | `[person]` | `[each run]` |
| Data freshness | `[max(timestamp) in input data vs. expected]` | `[> N hours stale → alert]` | `[person]` | `[each run]` |

#### Feature Drift Metrics

| Feature | Drift method | Baseline distribution | Alert threshold | Cadence |
|---|---|---|---|---|
| `[feature name]` | `[PSI / KS test / mean shift]` | `[training mean ± std or deciles]` | `[PSI > 0.2 / p < 0.05 / mean shift > Xσ]` | `[weekly]` |

PSI guidance: < 0.1 no action; 0.1–0.2 monitor; > 0.2 alert.

#### Prediction Drift Metrics

| Metric | Definition | Baseline | Alert threshold | Cadence |
|---|---|---|---|---|
| Mean score | `[average prediction score]` | `[training mean: X]` | `[shift > ±Y% → alert]` | `[weekly]` |
| Score distribution | `[decile or histogram comparison]` | `[training distribution]` | `[PSI > 0.2]` | `[weekly]` |
| Action volume | `[% of population above threshold]` | `[training rate: X%]` | `[> 2× or < 0.5× baseline → alert]` | `[weekly]` |

#### Performance Metrics (When Labels Are Available)

| Metric | Measurement method | Expected value | Alert threshold | Label delay | Cadence |
|---|---|---|---|---|---|
| `[primary metric]` | `[ground truth matching]` | `[validation value: X]` | `[drop > Y% → alert]` | `[N days / weeks]` | `[monthly]` |
| Calibration | `[observed vs. predicted rate by score band]` | `[ECE < X]` | `[ECE > Y → alert]` | `[same as above]` | `[monthly]` |

#### Business Outcome Metrics

| Metric | Definition | Expected value | Alert threshold | Cadence |
|---|---|---|---|---|
| `[e.g., conversion rate of flagged accounts]` | `[% of flagged accounts that converted]` | `[X%]` | `[< Y% → review / > Z% → investigate for leakage]` | `[monthly]` |

### 3. Alert Response Actions

| Alert type | Immediate action | Investigation steps | Escalation path | Time to respond |
|---|---|---|---|---|
| Schema failure | `[abort run / use fallback]` | `[check upstream pipeline]` | `[data engineer]` | `[< 1 hour]` |
| Row count anomaly | `[hold scores / alert]` | `[trace to source]` | `[pipeline owner]` | `[< 4 hours]` |
| Feature drift alert | `[log / flag for review]` | `[compare to training distribution / check upstream change]` | `[model owner]` | `[< 1 week]` |
| Performance degradation | `[flag for retraining review]` | `[check data, features, label definition]` | `[model owner + business owner]` | `[< 2 weeks]` |

### 4. Retraining Policy

| Element | Specification |
|---|---|
| Trigger type | `[ ] Scheduled` / `[ ] Metric-based` / `[ ] Event-based` |
| Scheduled cadence (if scheduled) | `[e.g., quarterly]` |
| Metric trigger (if metric-based) | `[e.g., primary metric drops below X% on 2 consecutive monthly reviews]` |
| Event trigger (if event-based) | `[e.g., major product change / data pipeline migration / regulatory update]` |
| Retraining requires | `[champion/challenger comparison / full validation plan re-run / approval]` |
| Retraining owner | `[person / team]` |

### 5. Rollback Criteria

- Rollback trigger: `[conditions that warrant rolling back — e.g., Critical data quality failure / performance drops below minimum acceptable floor]`
- Rollback method: `[reference Deployment Readiness Report rollback plan]`
- Rollback owner: `[name]`

### 6. Review Schedule

| Review type | Cadence | Owner | Output |
|---|---|---|---|
| Automated metric check | `[daily / each run]` | `[system / pipeline]` | `[dashboard update / alert]` |
| Weekly monitoring review | `[weekly]` | `[model owner]` | `[monitoring note in incident log]` |
| Full model review | `[quarterly / trigger-based]` | `[model owner + business owner]` | `[updated model card / retraining decision]` |

---

## Strong Version Additions

### Monitoring Dashboard Specification

| Dashboard element | Metric shown | Time window | Owner |
|---|---|---|---|
| Input health | `[row count, missingness, freshness]` | `[rolling 30 days]` | `[data engineer]` |
| Feature drift | `[PSI trend for top features]` | `[rolling 90 days]` | `[model owner]` |
| Prediction drift | `[score mean, distribution, action volume]` | `[rolling 90 days]` | `[model owner]` |
| Performance | `[primary metric, calibration — when labels available]` | `[monthly]` | `[model owner]` |
| Business outcomes | `[outcome rate, business KPIs]` | `[monthly]` | `[business owner]` |

### Incident Log Format

For each monitoring alert or model incident:

| Field | Value |
|---|---|
| Incident ID | `[INC-YYYYMMDD-###]` |
| Date detected | `[date]` |
| Alert type | `[data quality / feature drift / performance / business outcome]` |
| Description | `[what was observed]` |
| Root cause | `[upstream data change / concept drift / label shift / pipeline bug / other]` |
| Action taken | `[describe]` |
| Resolution date | `[date]` |
| Model update required | `[yes / no — describe]` |

### Subgroup Monitoring

For high-stakes models, monitor performance by key subgroups:

| Subgroup | Metric | Alert threshold | Cadence |
|---|---|---|---|
| `[Segment A]` | `[primary metric]` | `[< X]` | `[monthly]` |
| `[Segment B]` | `[primary metric]` | `[< X]` | `[monthly]` |

---

## Output Format

A living document (Markdown or shared doc) with a version history. The plan is referenced in the Deployment Readiness Report and the Model Card. Updated when any alert threshold, metric, or owner changes.

## Quality Checks

- [ ] At least one metric defined in each category: data quality, feature drift, prediction drift, performance
- [ ] Every metric has an alert threshold and a named owner
- [ ] Alert response actions are defined for each alert type
- [ ] Retraining trigger is explicit — not "we'll decide when needed"
- [ ] Review schedule has dates and owners
- [ ] Rollback criteria reference the Deployment Readiness Report

## Common Mistakes

- Monitoring plan covers only technical availability (job succeeded/failed) — not model quality
- Alert thresholds set without baselining — no reference distribution to detect drift against
- No label-based performance monitoring — assumes the model is always right
- Retraining defined as "when performance degrades" without a measurable threshold
- Monitoring plan created but never activated — model runs unobserved for months

## Related Workflow Stage / Gate

- **Stage:** 9 (drafted) → Stage 10 (activated and maintained)
- **Gate:** Production Gate (must exist before deployment) → Monitoring Gate (reviewed on cadence)

## Related References / Checklists

- `workflow/lifecycle.md` — Stage 10 exit criteria
- `workflow/quality-gates.md` — Monitoring Gate
- `templates/deployment-readiness-report-template.md` — companion artifact
- `templates/model-card-template.md` — companion artifact
- `references/diagnostics-guide.md` — drift and degradation sections
- `checklists/deployment-checklist.md`
