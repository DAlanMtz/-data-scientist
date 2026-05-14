# Data Audit Report Template

## Purpose

Document the quality, coverage, structure, and trustworthiness of the data that will support the project. The data audit is the primary defense against leakage, silent quality failures, and scope mismatch between the project brief and the available data.

## When to Use

At **Stage 1: Data Understanding and Quality Audit**. Produce this after the project brief is agreed and before EDA or modeling begins. Update it if new data sources are introduced or quality issues surface later.

## Required Inputs

- Project brief (Stage 0 output)
- Access to data sources, schemas, or documentation
- List of tables, files, APIs, or sheets expected to support the analysis

## Minimum Contents

### 1. Audit Summary

- Project: `[name]`
- Audit date: `[date]`
- Analyst: `[name]`
- Data sources reviewed: `[count]`
- Overall data sufficiency verdict: `[ ] Sufficient` / `[ ] Conditionally sufficient (see issues)` / `[ ] Insufficient for defined scope`

### 2. Data Source Inventory

| Source | Type | Grain | Row count | Date range | Owner | Refresh cadence | Notes |
|---|---|---|---:|---|---|---|---|
| `[table/file]` | `[DB/file/API]` | `[grain]` | `[n]` | `[start – end]` | `[owner]` | `[daily/weekly/etc.]` | `[notes]` |

### 3. Field-Level Profile (Key Fields)

Repeat per data source as needed.

| Field | Type | Non-null % | Distinct values | Min | Max | Notes |
|---|---|---:|---:|---|---|---|
| `[field]` | `[type]` | `[%]` | `[n]` | `[min]` | `[max]` | `[notes]` |

Flag: join keys, date fields, target field, candidate leakage fields.

### 4. Grain and Join Validation

- Expected grain: `[one row per X]`
- Confirmed grain: `[ ] Yes` / `[ ] No — explain: [detail]`
- Join key validation:

| Join | Left rows | Right rows | Match rate | Fan-out? | Notes |
|---|---:|---:|---:|---|---|
| `[left.key = right.key]` | `[n]` | `[n]` | `[%]` | `[ ] Yes / No` | `[notes]` |

### 5. Missingness Summary

| Field | Missing % | Pattern | Business interpretation | Recommended action |
|---|---:|---|---|---|
| `[field]` | `[%]` | `[random/by segment/by time]` | `[NA/unknown/delayed/error]` | `[impute/exclude/flag]` |

### 6. Duplicate Check

| Check | Result | Action |
|---|---|---|
| Exact duplicate rows | `[n found]` | `[none / deduplicate / investigate]` |
| Duplicate primary keys | `[n found]` | `[none / resolve / document]` |
| Entity overlap across train/test | `[checked / not applicable]` | `[clean / flag]` |

### 7. Leakage Candidate Review

| Field | Concern | Disposition | Evidence |
|---|---|---|---|
| `[field]` | `[why it may leak]` | `[ ] Safe` / `[ ] Excluded` / `[ ] Conditional` | `[how confirmed]` |

### 8. Data Quality Issues

Use severity levels from `workflow/severity-levels.md`.

| Severity | Issue | Fields affected | Scope | Business impact | Recommended action |
|---|---|---|---|---|---|
| `[Critical/High/Medium/Low/Info]` | `[issue description]` | `[fields]` | `[rows/time/segment]` | `[impact]` | `[fix/flag/accept]` |

---

## Strong Version Additions

### Data Lineage

For each key field, document the transformation path from source system to analytic table:

> `[source system]` → `[ETL/transform step]` → `[intermediate table]` → `[analytic field]`

### Lag Analysis

For event-based targets or time-sensitive features:

| Field | Event timestamp | Record availability delay | Impact on feature window |
|---|---|---|---|
| `[field]` | `[when event occurs]` | `[days/hours]` | `[describe impact]` |

### Coverage Gaps

| Source | Period with no data | Likely cause | Impact on analysis |
|---|---|---|---|
| `[source]` | `[gap period]` | `[system migration / collection change]` | `[describe]` |

### Data Access and Privacy Notes

- Permitted uses: `[what the data can be used for]`
- Restricted fields: `[PII, sensitive attributes, restricted-use fields]`
- Retention limits: `[if applicable]`

---

## Output Format

A structured document (Markdown, Word, or shared doc) with tables. Should be skimmable — summary at the top, detail in sections. Share with the team before modeling begins.

## Quality Checks

- [ ] All expected data sources inventoried
- [ ] Row counts and date ranges confirmed
- [ ] Grain confirmed or fan-out documented
- [ ] All join keys validated
- [ ] Missingness measured for all key fields
- [ ] Duplicate check completed
- [ ] Every candidate leakage field has a written disposition
- [ ] Every quality issue has a severity label
- [ ] Sufficiency verdict is stated explicitly

## Common Mistakes

- Auditing only the final analytic table, not the source tables — leakage often hides in upstream joins
- Accepting "no nulls" in a key field as a sign of quality without investigating why
- Skipping the leakage candidate review because it "seems unlikely"
- Treating a zero-row join result as an error rather than a data coverage gap
- Producing a data audit that notes issues but offers no recommended action or severity

## Related Workflow Stage / Gate

- **Stage:** 1 — Data Understanding and Quality Audit
- **Gate:** Data Readiness Gate — must pass before Stage 2 (Exploratory Analysis) begins

## Related References / Checklists

- `workflow/lifecycle.md` — Stage 1 exit criteria
- `workflow/quality-gates.md` — Data Readiness Gate
- `workflow/severity-levels.md` — severity classification
- `checklists/data-quality-checklist.md`
- `checklists/pre-modeling-checklist.md` — Data Sources and Leakage sections
- `references/validation-and-leakage-checklist.md`
