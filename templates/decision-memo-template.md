# Decision Memo Template

## Purpose

Document the operational decision policy that flows from the model: the selected threshold, the error cost assumptions used to choose it, the actions at each score range, and the human review and fallback rules. The decision memo translates model output into a business operating procedure — it is the bridge between data science and operations.

> **Relationship to `analysis-report-template.md`:** That template is a general stakeholder-facing analysis report with a recommendation section. This template is a standalone operational artifact — the formal specification of the decision policy that operations will implement. More structured, more specific, and co-owned by the business stakeholder.

## When to Use

At **Stage 7: Calibration, Thresholds, and Decision Policy**. Produced in tandem with the Calibration Report. Must be reviewed and agreed by the decision stakeholder before production.

## Required Inputs

- Calibration Report (Stage 7)
- Error Analysis Report (Stage 6)
- Business cost-of-error information from the Project Brief (Stage 0)
- Volume and capacity information from the operational team

## Minimum Contents

### 1. Memo Header

- Project: `[name]`
- Memo date: `[date]`
- Analyst: `[name]`
- Stakeholder / decision owner: `[name and role]`
- Model: `[name / experiment ID]`
- Status: `[ ] Draft for review` / `[ ] Agreed — approved for production`

### 2. Decision Context

- Decision being made: `[what action this model informs]`
- Decision frequency: `[e.g., weekly batch / real-time per event]`
- Decision volume: `[e.g., ~2,000 customers per week scored]`
- Cost of false positive (acting on a non-case): `[$ / operational description]`
- Cost of false negative (missing a true case): `[$ / operational description]`
- Cost asymmetry: `[FP cost : FN cost = X : Y]`

### 3. Threshold Analysis

| Threshold | Precision | Recall | Volume flagged | Est. true positives | Est. false positives | Net business value |
|---|---:|---:|---:|---:|---:|---|
| `[0.3]` | `[%]` | `[%]` | `[n]` | `[n]` | `[n]` | `[$]` |
| `[0.5]` | `[%]` | `[%]` | `[n]` | `[n]` | `[n]` | `[$]` |
| `[0.7]` | `[%]` | `[%]` | `[n]` | `[n]` | `[n]` | `[$]` |
| **`[selected]`** | **`[%]`** | **`[%]`** | **`[n]`** | **`[n]`** | **`[n]`** | **`[$ — selected]`** |

### 4. Selected Threshold and Rationale

- **Selected threshold:** `[value]`
- **Selection rationale:** `[plain-language explanation of why this threshold — tie to the cost asymmetry and business objective]`
- **Who agreed to this threshold:** `[stakeholder name and role]`
- **Agreement date:** `[date]`

### 5. Decision Policy

Define exactly what happens at each score range:

| Score range | Label | Action | Owner | Notes |
|---|---|---|---|---|
| `≥ [threshold]` | High risk | `[e.g., trigger retention outreach]` | `[team/person]` | `[volume: ~n per week]` |
| `[lower] – [threshold)` | Review band | `[e.g., queue for manual review]` | `[team/person]` | `[optional — only if warranted by capacity]` |
| `< [lower]` | Low risk | `[e.g., no action / standard care]` | `[team/person]` | — |

### 6. Fallback Rule

If the model is unavailable (system failure, data delay, or data quality failure):

- Fallback action: `[e.g., use prior week's scores / apply simple rule: flag all accounts <90 days tenure / no action]`
- Who triggers the fallback: `[person/team]`
- Fallback notification: `[who is notified when the model is unavailable]`

### 7. Threshold Review Trigger

- Scheduled review date: `[e.g., 90 days after production launch]`
- Metric-based trigger: `[e.g., if precision drops below X% or volume changes by >20%, trigger threshold review]`
- Owner of review: `[person/team]`

---

## Strong Version Additions

### Expected Business Impact

Estimate the business impact of the selected threshold compared to current process:

| Metric | Current process | Selected model (at threshold) | Delta |
|---|---|---|---|
| True positive volume | `[n/week]` | `[n/week]` | `[+n]` |
| False positive volume | `[n/week]` | `[n/week]` | `[-n]` |
| Estimated revenue / cost impact | `[$]` | `[$]` | `[+$]` |
| Contact rate | `[%]` | `[%]` | `[change]` |

### Human Review Tier Design

If a human review band is included:

- Review population: `[score range / volume / characteristics]`
- Review criteria: `[what the reviewer decides]`
- Reviewer capacity: `[n reviews per day/week]`
- Escalation path: `[what happens if reviewer cannot process in time]`

### Assumptions and Risks

| Assumption | Risk if Wrong | Monitoring Response |
|---|---|---|
| `[cost of FN = $200]` | `[threshold would shift lower]` | `[revisit if cost estimate changes]` |
| `[volume stays ~2K/week]` | `[operational capacity may be exceeded]` | `[monitor action volume in production]` |

---

## Output Format

A short, plain-language document (1–3 pages) shared with and signed off by the business stakeholder before production. Avoid data science jargon in the policy section — operations needs to implement it without translation.

## Quality Checks

- [ ] Threshold chosen with explicit cost-tradeoff rationale — not defaulted to 0.5
- [ ] Threshold analysis table shows at least three candidate thresholds
- [ ] Named stakeholder has agreed to the selected threshold
- [ ] Decision policy describes every score range with a concrete action
- [ ] Fallback rule is defined
- [ ] Review trigger is defined with a date and an owner

## Common Mistakes

- Setting threshold at 0.5 without examining the cost tradeoff
- Choosing the threshold that maximizes F1 when the error costs are asymmetric
- Leaving the decision policy implicit — "the operations team will figure it out"
- No fallback rule — model availability assumed to be 100%
- No review trigger — threshold runs indefinitely until someone escalates a complaint

## Related Workflow Stage / Gate

- **Stage:** 7 — Calibration, Thresholds, and Decision Policy
- **Gate:** Calibration/Decision Gate — must pass before Stage 8 (Interpretation and Reporting)

## Related References / Checklists

- `workflow/lifecycle.md` — Stage 7 exit criteria
- `workflow/quality-gates.md` — Calibration/Decision Gate
- `templates/calibration-report-template.md` — companion artifact
- `references/metrics-guide.md`
- `references/decision-science-guide.md`
