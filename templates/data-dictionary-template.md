# Data Dictionary Template

Use this template to document datasets used for analysis, modeling, dashboards, scoring, or production pipelines.

## Dataset Summary

| Field | Value |
| --- | --- |
| Dataset name | `[name]` |
| Business description | `[what this dataset represents]` |
| Grain | `[one row per ...]` |
| Primary key | `[field or composite key]` |
| Refresh frequency | `[daily/weekly/monthly/ad hoc/streaming]` |
| Source system | `[system/table/file/API]` |
| Owner | `[team/person]` |
| Time zone | `[timezone]` |
| Date coverage | `[start-end]` |
| Retention policy | `[policy]` |
| Known limitations | `[notes]` |

## Column Dictionary

| Column name | Data type | Description | Allowed values/ranges | Missing value rules | Transformation notes | Sensitive/protected status | Quality checks |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `[column]` | `[type]` | `[meaning]` | `[values/range]` | `[allowed/not allowed/default]` | `[derived/source/raw]` | `[none/sensitive/protected/proxy]` | `[checks]` |

## Required Inputs

- Source schema or sample data.
- Business definitions.
- Key fields and grain.
- Refresh rules.
- Quality expectations.
- Privacy/sensitivity classification.

## Expected Outputs

- Dataset-level metadata.
- Column-level definitions.
- Missing value rules.
- Quality checks.
- Sensitive/protected status.
- Transformation notes for derived fields.

## Step-By-Step Workflow

1. Confirm dataset grain and primary key.
2. List all columns with source data types.
3. Write plain-language descriptions.
4. Define allowed values or valid ranges.
5. Document missing-value meaning and handling.
6. Identify derived fields and transformations.
7. Flag sensitive, protected, or proxy variables.
8. Add quality checks for required fields.
9. Review with data owner or stakeholder.
10. Version the dictionary when schema changes.

## Quality Check Examples

Use checks such as:

- Required column is present.
- Primary key is unique and not null.
- Date is within expected range.
- Numeric value is within valid min/max.
- Category value appears in allowed list.
- Missing rate is below threshold.
- Referential key matches dimension table.
- Refresh timestamp is within SLA.
- No future timestamps relative to extraction.

## Validation And Evaluation Guidance

- Reconcile dictionary against actual schema.
- Check row grain with key uniqueness.
- Confirm units for numeric fields.
- Verify date/time semantics.
- Validate sensitive/protected labels with policy owner where relevant.

## Interpretation Guidance

- Descriptions should explain business meaning, not repeat the column name.
- Missingness rules should distinguish unknown, not applicable, and not collected.
- Transformation notes should be enough to reproduce derived fields.
- Sensitive/protected status should warn model builders and report authors.

## Common Failure Modes

- Grain omitted.
- IDs documented as numeric when leading zeros matter.
- Allowed values stale.
- Missing value codes not explained.
- Derived fields lack formulas or source logic.
- Sensitive or proxy variables not flagged.

## Tool-Flexible Notes

- Python/R: generate initial column inventory from data frames.
- SQL: pull schema from information schema and add business definitions.
- Excel/Sheets: maintain a reviewable table with protected headers.
- Notebooks: link dictionary to EDA and data quality checks.
- Production pipelines: convert critical dictionary rules into data contract tests.

