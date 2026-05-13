# EDA Notebook Template

Use this template when the task is to understand a dataset, assess modeling readiness, identify data quality risks, or produce an exploratory analysis narrative.

## Required Inputs

- Business question or project objective.
- Dataset paths, database tables, APIs, spreadsheets, or extracts.
- Data dictionary or schema notes if available.
- Time window and population scope.
- Target variable definition if modeling is planned.
- Known quality issues, exclusions, or stakeholder assumptions.

## Expected Outputs

- Reproducible notebook or analysis script.
- Data inventory and schema summary.
- Data quality findings.
- EDA visuals and summary tables.
- Initial feature ideas.
- Modeling-readiness assessment.
- Recommended next steps.

## Notebook Narrative Structure

1. Objective and scope.
2. Data inventory.
3. Load and validation checks.
4. Schema and grain inspection.
5. Missingness, duplicates, and quality flags.
6. Descriptive statistics and distributions.
7. Relationships and segments.
8. Target variable analysis, if applicable.
9. Initial feature ideas.
10. Modeling-readiness assessment.
11. Recommendations and next steps.

## Step-By-Step Workflow

### 1. Project Objective

Write:

- Decision or question being answered.
- Population and time window.
- Unit of analysis.
- Expected user of the output.
- Success criteria.

If the objective is vague, produce an EDA that clarifies possible targets and decision paths rather than pretending the task is already modeled.

### 2. Data Inventory

Create a table:

| Source | Grain | Rows | Date range | Key fields | Owner | Notes |
| --- | --- | ---: | --- | --- | --- | --- |
| [table/file] | [grain] | [n] | [range] | [keys] | [owner] | [issues] |

Check whether sources can be joined without changing grain.

### 3. Load Data

Load data reproducibly:

- Python/R: parameterize paths, queries, and date windows.
- SQL: save source queries or view definitions.
- Excel/Sheets: preserve raw sheets and create derived sheets separately.
- Notebooks: keep load cells deterministic; avoid manual copy-paste.
- Production-facing work: use the same extraction logic planned for pipelines.

Record row counts immediately after loading.

### 4. Schema Inspection

Inspect:

- Column names and types.
- Key uniqueness.
- Grain and duplicate implications.
- Date parsing and time zone.
- Numeric units.
- Category levels and unexpected values.
- ID fields that must remain strings.

Flag columns whose type or meaning is ambiguous.

### 5. Missingness

Summarize:

- Missing count and rate by column.
- Missingness by time/source/segment.
- Co-missingness patterns.
- Missingness relationship with target, if available.

Interpret missingness as one of: not applicable, unknown, not collected, delayed, suppressed, or data error.

### 6. Duplicates

Check:

- Exact duplicate rows.
- Duplicate primary or composite keys.
- Near-duplicates in text/event data.
- Duplicate entities across sources.
- Row multiplication after joins.

Do not drop duplicates until the grain and business meaning are clear.

### 7. Descriptive Statistics

Produce:

- Numeric summary: count, mean, median, standard deviation, quantiles, min, max.
- Category frequency: count, share, rare levels.
- Date coverage: first, last, gaps, row count by period.
- Segment summaries for major business groups.

Include denominators for percentages.

### 8. Distribution Analysis

Use:

- Histograms or ECDFs for numeric fields.
- Bar charts for categories.
- Box/violin plots for numeric by category.
- Time plots for temporal fields.

Look for spikes, long tails, impossible values, and business thresholds.

### 9. Relationship Analysis

Analyze:

- Numeric-numeric relationships with scatter/hexbin/correlation.
- Category-numeric relationships with grouped summaries.
- Category-category relationships with contingency tables.
- Time trends by segment.
- Cohort or funnel patterns when relevant.

Avoid causal language unless the design supports it.

### 10. Target Variable Analysis

If a target exists:

- Confirm target definition and outcome window.
- Measure target prevalence/distribution.
- Check target availability and delay.
- Review target by time and segment.
- Check for label leakage candidates.
- Identify class imbalance or skew.

If the target is not valid, stop and recommend target redesign.

### 11. Data Quality Flags

Create a quality issue table:

| Severity | Issue | Affected fields | Scope | Impact | Recommended action |
| --- | --- | --- | --- | --- | --- |
| [high/medium/low] | [issue] | [fields] | [rows/time] | [risk] | [fix] |

High-severity issues should block modeling claims.

### 12. Initial Feature Ideas

List feature candidates by family:

- Numeric transformations.
- Categorical encodings.
- Date/time features.
- Aggregations and ratios.
- Lags and rolling windows.
- Text/geospatial/event features.

For each, note source, prediction-time availability, refresh feasibility, and leakage risk.

### 13. Modeling-Readiness Assessment

Assess:

- Valid target exists.
- Enough rows and positive cases.
- Reliable train/test split possible.
- Key features available at prediction time.
- Data quality risks are manageable.
- Business metric and baseline are defined.
- Production path is plausible if needed.

Use status: ready, conditionally ready, not ready.

### 14. Recommended Next Steps

Provide:

- Data fixes.
- Additional data needed.
- Baseline model or analysis path.
- Validation strategy.
- Reporting or dashboard path.
- Stakeholder decisions needed.

## Validation And Evaluation Guidance

- Reconcile row counts after every join/filter.
- Verify key uniqueness and grain.
- Validate date windows and target timing.
- Use holdout thinking even during EDA: do not let future data inform feature rules for predictive work.
- Compare EDA findings across time and core segments.

## Interpretation Guidance

- Translate patterns into implications: data defect, business pattern, modeling signal, or open question.
- State uncertainty when samples are small.
- Separate predictive association from causal claims.
- Summarize what should change in the next analysis step.

## Common Failure Modes

- Notebook has charts but no decision-relevant findings.
- Grain is wrong after joins.
- Target is analyzed before target timing is validated.
- Missingness is imputed without interpretation.
- Outliers are removed without business review.
- EDA uses the full dataset to design features that later leak into validation.
- Notebook cannot be rerun top to bottom.

## Tool-Flexible Notes

- Python/R: use reusable profiling functions and deterministic seeds.
- SQL: profile large data in-database before extracting.
- Excel/Sheets: use pivots, filters, and data validation, but preserve raw data.
- Notebooks: write markdown conclusions under every major output.
- Scripts/pipelines: convert repeated checks into assertions when analysis becomes recurring.

