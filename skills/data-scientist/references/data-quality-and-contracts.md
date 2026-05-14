# Data Quality And Contracts

Use this guide to define what data must look like before analysis, modeling, scoring, reporting, or monitoring can be trusted.

## Data Contracts

A data contract defines expectations between data producers and consumers.

Include:

- Dataset name and owner.
- Business meaning and grain.
- Primary key and uniqueness.
- Required fields.
- Field types and units.
- Valid ranges and allowed categories.
- Timestamp semantics and time zone.
- Freshness and delivery schedule.
- Backfill and late-arriving data policy.
- Change notification process.
- Quality checks and severity.

For production models, contracts should cover both training data and scoring data.

## Schema Expectations

Check:

- Required columns exist.
- No unexpected column removals or type changes.
- Field names are stable.
- Nested fields or JSON keys are present where expected.
- Column order only matters if the consuming system depends on it.

Example checks:

- SQL: query information schema and compare column names/types.
- Python/R: assert expected columns and dtypes/classes.
- Spreadsheet: protected header row plus validation formulas.

## Data Types

Validate:

- Numeric fields are numeric and use consistent precision.
- Dates parse correctly and use expected time zone.
- Booleans are encoded consistently.
- Categories are strings or controlled codes.
- IDs are strings when leading zeros matter.

Do not allow silent type coercion to create missing values without reporting it.

## Valid Ranges

Examples:

- Age >= 0 and within plausible maximum.
- Quantity >= 0 unless returns are represented as negatives.
- Probability between 0 and 1.
- Discount between 0 and configured maximum.
- Timestamp not before product launch or after extraction time.

Report violations by count, percentage, source, and time window.

## Required Fields

Define required fields by use:

- Hard required: cannot run without them.
- Soft required: can run with fallback but quality is degraded.
- Optional: useful when present.

For each required field, define missing-value behavior: fail, exclude, impute, use default, or route to manual review.

## Unique Keys

Check:

- Primary key uniqueness.
- Composite key uniqueness where grain uses multiple fields.
- Duplicate entity-event records.
- Duplicate labels for the same prediction point.
- Conflicting records with same key but different values.

Duplicates are not always errors, but unexplained duplicates invalidate joins and metrics.

## Freshness

Track:

- Latest event timestamp.
- Latest ingestion timestamp.
- Expected delay.
- Missing partitions.
- Source-specific lag.

Production rule:

- Fail or warn when data is older than the contract allows.
- Make dashboard freshness visible to users.

## Missingness

Check:

- Missing count and rate by field.
- Missingness by source, time, segment, and target.
- New missingness spikes.
- Co-missingness patterns.
- Difference between null, blank, zero, unknown, not applicable, and not collected.

Missingness can be signal, data defect, or process artifact. Decide before imputing.

## Duplicates

Check:

- Exact duplicate rows.
- Duplicate primary keys.
- Near-duplicate records with minor timestamp or text differences.
- Replayed events.
- Multiple source systems sending same event.

For modeling, check duplicate or near-duplicate entities across train and test.

## Outliers

Check:

- Extreme numeric values.
- Sudden spikes by period or source.
- Impossible combinations.
- High influence records.

Classify outliers:

- Real and important.
- Real but should be capped for objective.
- Data entry or processing error.
- Different population that should be modeled separately.

## Category Drift

Check:

- New categories.
- Missing expected categories.
- Category frequency shifts.
- Renamed or recoded values.
- Rare categories becoming common.

Production scoring must define behavior for unseen categories.

## Unit Consistency

Check:

- Currency.
- Measurement system.
- Time units.
- Quantity units.
- Percentage versus decimal.
- Gross versus net.

Unit changes can look like model drift. Validate before retraining.

## Date Consistency

Check:

- Start date <= end date.
- Event date <= extraction date.
- Birth date before activity date.
- Outcome date after prediction date.
- Time zones and daylight-saving transitions.
- Late-arriving updates.

Date errors are common sources of leakage and invalid durations.

## Referential Integrity

Check:

- Foreign keys match dimension tables.
- Join match rates by period and source.
- Orphan records.
- Many-to-many joins where one-to-one is expected.
- Slowly changing dimension validity periods.

Always measure row counts before and after joins.

## Data Quality Tests

Examples that work across SQL, Python, R, and spreadsheets:

- Row count within expected range.
- Required columns present.
- No nulls in primary key.
- Primary key unique.
- Date range complete.
- Numeric field within valid range.
- Category values in allowed list.
- Freshness within SLA.
- Join match rate above threshold.
- Target rate within plausible range.
- No future timestamps relative to extraction.

Express tests as assertions where possible.

## Data Quality Reporting

Report:

- Check name.
- Expected condition.
- Actual result.
- Severity.
- Affected rows.
- Affected time/source/segment.
- Impact on analysis or model.
- Recommended action and owner.

Severity guide:

- Critical: stop the pipeline or invalidate the analysis.
- Warning: run can continue with caveat or fallback.
- Info: track for context.

