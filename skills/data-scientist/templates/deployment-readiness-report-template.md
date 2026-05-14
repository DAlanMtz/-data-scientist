# Deployment Readiness Report Template

## Purpose

Certify that the model, its inputs, outputs, dependencies, and operational processes meet the requirements for production deployment. This is the formal sign-off artifact — not a technical guide for building the pipeline. It answers: "Is this ready to go live?"

> **Relationship to `production-pipeline-template.md`:** That template guides the *implementation* of a production pipeline (architecture, code structure, scheduling, logging). This template is the *readiness certification* — the checklist and sign-off document produced at the end of Stage 9, confirming that the pipeline built with that template meets production standards.

## When to Use

At the end of **Stage 9: Deployment Readiness**. Must be completed and reviewed before the model goes live. For phased rollouts (shadow mode, limited launch), complete for the scope of the initial deployment.

## Required Inputs

- All prior artifacts: Project Brief, Data Audit, Validation Plan, Experiment Log, Model Comparison Report, Error Analysis Report, Calibration Report, Decision Memo, Model Card
- Engineering review of the scoring pipeline
- Platform or infrastructure specifications

## Minimum Contents

### 1. Report Header

- Project: `[name]`
- Report date: `[date]`
- Analyst: `[name]`
- Model: `[name / version / artifact ID]`
- Deployment type: `[ ] Batch scoring` / `[ ] Real-time API` / `[ ] Embedded rule` / `[ ] Dashboard / report`
- Overall readiness verdict: `[ ] Ready for production` / `[ ] Conditionally ready — see open items` / `[ ] Not ready — see blockers`

### 2. Input Contract

Define exactly what the model expects as input in production:

| Field | Type | Required | Allowed range / values | Missing-value handling | Notes |
|---|---|---|---|---|---|
| `[field_name]` | `[int/float/str/date]` | `[ ] Yes / No` | `[range or categories]` | `[impute / error / fallback]` | `[notes]` |

- Data freshness requirement: `[e.g., input data must be no older than 24 hours]`
- Failure behavior if input is missing or stale: `[e.g., abort scoring run and alert owner]`

### 3. Output Contract

Define exactly what the model produces in production:

| Field | Type | Range | Semantics | Downstream consumers |
|---|---|---|---|---|
| `[score]` | `[float]` | `[0.0–1.0]` | `[probability of event X in window Y]` | `[team / system / dashboard]` |
| `[prediction]` | `[int/str]` | `[0/1 or category]` | `[threshold applied: score ≥ T → 1]` | `[operations team]` |
| `[reason_codes]` | `[list of str]` | `[top 3 drivers]` | `[SHAP-based top features]` | `[CRM system]` |

- Output delivery mechanism: `[e.g., Snowflake table / REST API / CSV / BigQuery view]`
- Output freshness SLA: `[e.g., scores available by 06:00 UTC each Monday]`

### 4. Artifact Versioning

| Artifact | Location | Version / ID | Date |
|---|---|---|---|
| Trained model object | `[path / registry]` | `[v2.1 / hash]` | `[date]` |
| Preprocessing pipeline | `[path / registry]` | `[v2.1 / hash]` | `[date]` |
| Feature definitions | `[path / doc link]` | `[v2.1]` | `[date]` |
| Scoring code | `[git commit / package version]` | `[commit hash]` | `[date]` |
| Calibration object (if used) | `[path / registry]` | `[v2.1]` | `[date]` |
| Threshold config | `[path / config file]` | `[v1.0]` | `[date]` |

### 5. Training-Serving Skew Review

| Check | Status | Notes |
|---|---|---|
| Scoring uses identical feature definitions as training | `[ ] Pass / [ ] Fail` | `[notes]` |
| Preprocessing applied in same order as training | `[ ] Pass / [ ] Fail` | `[notes]` |
| Categorical encodings match training categories | `[ ] Pass / [ ] Fail` | `[notes]` |
| Unseen category handling defined | `[ ] Pass / [ ] N/A` | `[e.g., map to "other" / impute with training mean]` |
| Sample scoring run output matches expected range | `[ ] Pass / [ ] Fail` | `[notes]` |

### 6. Monitoring Plan Summary

Reference the full Monitoring Plan (`templates/monitoring-plan-template.md`). Confirm minimum monitoring is in place:

| Monitoring metric | Alert threshold | Review cadence | Alert owner |
|---|---|---|---|
| Input row count | `[< X rows → alert]` | `[each run]` | `[person/team]` |
| Feature missingness | `[> X% null on field Y → alert]` | `[weekly]` | `[person/team]` |
| Prediction distribution | `[mean score shifts > X → alert]` | `[weekly]` | `[person/team]` |
| Business outcome | `[e.g., recall drops below X% → alert]` | `[monthly]` | `[person/team]` |

### 7. Owner and Escalation

| Role | Name | Responsibility |
|---|---|---|
| Model owner | `[name]` | Performance, retraining, deprecation |
| Data pipeline owner | `[name]` | Input data freshness, schema changes |
| Operational user | `[name]` | Uses scores for decisions |
| Escalation path | `[name / team]` | Contacted if model failure affects operations |

### 8. Rollback Plan

- Rollback trigger: `[conditions that warrant reverting — e.g., precision drops below X%, system failure, data quality failure]`
- Rollback method: `[e.g., revert to previous artifact version / disable model and apply fallback rule]`
- Previous artifact available: `[ ] Yes — version: [v1.x]` / `[ ] No — first deployment`
- Rollback owner: `[name]`
- Estimated rollback time: `[e.g., < 30 minutes]`

### 9. Open Items (if Conditionally Ready)

| # | Item | Severity | Owner | Due date |
|---|---|---|---|---|
| 1 | `[description]` | `[Critical/High/Medium]` | `[name]` | `[date]` |

---

## Strong Version Additions

### Sign-Off Log

| Role | Name | Decision | Date | Notes |
|---|---|---|---|---|
| Data science owner | `[name]` | `[ ] Approved / [ ] Pending / [ ] Blocked` | `[date]` | `[notes]` |
| Engineering owner | `[name]` | `[ ] Approved / [ ] Pending / [ ] Blocked` | `[date]` | `[notes]` |
| Business owner | `[name]` | `[ ] Approved / [ ] Pending / [ ] Blocked` | `[date]` | `[notes]` |
| Risk / compliance | `[name]` | `[ ] Approved / [ ] Not needed / [ ] Pending` | `[date]` | `[notes]` |

### Shadow Mode Results

If the model ran in shadow mode before live deployment:

- Shadow run period: `[date range]`
- Shadow population: `[n scored]`
- Output distribution matched expected: `[ ] Yes / [ ] No — explain`
- Any unexpected errors or anomalies: `[describe / none]`

### Retraining Plan

- Retraining trigger: `[metric-based / scheduled / event-based]`
- Retraining schedule: `[e.g., quarterly or when performance drops below X]`
- Champion/challenger process: `[ ] Required` / `[ ] Optional`
- Retraining owner: `[name]`

---

## Output Format

A structured document (Markdown or Word) reviewed and signed off by data science, engineering, and business owners before launch. Attach or link to the Model Card, Decision Memo, and Monitoring Plan.

## Quality Checks

- [ ] Input contract is field-level — not "whatever is in the table"
- [ ] Output contract specifies semantics, not just field names
- [ ] Training-serving skew review is documented with pass/fail for each check
- [ ] All artifacts are versioned with locations
- [ ] At least one monitoring metric has an alert threshold and a named owner
- [ ] Rollback plan is defined with a named owner and estimated time
- [ ] Escalation path is named — not a team inbox only

## Common Mistakes

- Completing this report based on planned pipeline rather than tested pipeline
- Input schema documented as "see the database" — field-level specification is required
- No artifact versioning — cannot reproduce or roll back
- Monitoring noted as "to be added after launch"
- Rollback plan references an artifact version that no longer exists

## Related Workflow Stage / Gate

- **Stage:** 9 — Deployment Readiness
- **Gate:** Production Gate — must pass before Stage 10 (Monitoring and Iteration) begins

## Related References / Checklists

- `workflow/lifecycle.md` — Stage 9 exit criteria
- `workflow/quality-gates.md` — Production Gate
- `templates/production-pipeline-template.md` — pipeline implementation guide
- `templates/model-card-template.md` — companion artifact
- `templates/monitoring-plan-template.md` — companion artifact
- `checklists/deployment-checklist.md`
- `checklists/responsible-ai-checklist.md`
