# Data Quality Checklist

Use for dataset, extract, table, spreadsheet, API payload, feature table, dashboard source, or scoring input review.

## Schema

- [ ] Expected columns are present.
- [ ] Unexpected missing columns are flagged.
- [ ] Unexpected new columns are reviewed.
- [ ] Column names are stable.
- [ ] Nested fields or JSON keys are validated where relevant.
- [ ] Schema changes have owner approval.

## Data Types

- [ ] Numeric fields parse as numeric.
- [ ] Date/time fields parse correctly.
- [ ] Boolean values are consistent.
- [ ] IDs are strings when leading zeros matter.
- [ ] Categorical fields are not accidentally numeric.
- [ ] Type coercion failures are counted.

## Required Fields

- [ ] Primary key is present.
- [ ] Required business fields are present.
- [ ] Required modeling/scoring fields are present.
- [ ] Required fields have defined missing behavior.
- [ ] Critical missing required fields fail the run or block conclusions.

## Missingness

- [ ] Missing rate is measured by column.
- [ ] Missingness is measured by time, source, and segment.
- [ ] Missingness spikes are flagged.
- [ ] Null, blank, zero, unknown, and not applicable are distinguished.
- [ ] Missingness impact on analysis/model is documented.

## Duplicates

- [ ] Exact duplicate rows are counted.
- [ ] Primary key duplicates are counted.
- [ ] Composite key duplicates are counted.
- [ ] Near-duplicates are considered for text/events.
- [ ] Join-induced row multiplication is checked.
- [ ] Duplicate handling is documented.

## Valid Ranges

- [ ] Numeric min/max values are plausible.
- [ ] Business rule ranges are enforced.
- [ ] Percentages/probabilities are within valid bounds.
- [ ] Negative values are valid only where meaningful.
- [ ] Impossible values are flagged.
- [ ] Range violations are reported by source/time.

## Category Consistency

- [ ] Allowed categories are defined.
- [ ] Unexpected categories are flagged.
- [ ] Missing expected categories are flagged.
- [ ] Rare category behavior is defined.
- [ ] Renamed or recoded categories are detected.
- [ ] Category frequency drift is monitored.

## Date And Time Consistency

- [ ] Start dates are before end dates.
- [ ] Event dates are not after extraction date unless valid.
- [ ] Outcome dates follow prediction dates.
- [ ] Time zones are consistent.
- [ ] Daylight-saving or local-time issues are considered.
- [ ] Future timestamps are flagged.
- [ ] Date coverage has no unexplained gaps.

## Unit Consistency

- [ ] Currency is consistent.
- [ ] Measurement units are consistent.
- [ ] Time units are consistent.
- [ ] Percent versus decimal is clear.
- [ ] Gross/net definitions are clear.
- [ ] Unit changes over time are checked.

## Referential Integrity

- [ ] Foreign keys match dimension/reference tables.
- [ ] Join match rate is measured.
- [ ] Orphan records are counted.
- [ ] Many-to-many joins are expected or resolved.
- [ ] Slowly changing dimension validity is respected.
- [ ] Row counts before and after joins are reconciled.

## Freshness And Volume

- [ ] Latest event timestamp is within SLA.
- [ ] Latest ingestion timestamp is within SLA.
- [ ] Expected partitions/files are present.
- [ ] Row counts are within expected range.
- [ ] Entity counts are within expected range.
- [ ] Sudden volume changes are explained.

## Outliers And Drift

- [ ] Extreme values are reviewed.
- [ ] Distribution shifts are measured.
- [ ] Feature drift is checked for model inputs.
- [ ] Target/label drift is checked when labels exist.
- [ ] Source-specific drift is reviewed.
- [ ] Outliers are classified as real, error, or separate population.

## PII And Sensitive Data

- [ ] PII fields are identified.
- [ ] Sensitive/protected fields are identified.
- [ ] Proxy fields are considered.
- [ ] Access and sharing rules are followed.
- [ ] Reports and logs avoid unnecessary sensitive details.
- [ ] Data retention requirements are known.

## Data Contract Compliance

- [ ] Contract owner is identified.
- [ ] Contract includes grain, schema, required fields, freshness, ranges, categories, and quality thresholds.
- [ ] Contract checks are executable in SQL, Python, R, spreadsheet formulas, or pipeline tests.
- [ ] Contract failures have severity levels.
- [ ] Contract changes are versioned.

## Reporting

- [ ] Quality report includes check, expected value, actual value, severity, affected rows, impact, and owner.
- [ ] Critical issues are surfaced before modeling/reporting.
- [ ] Known issues are included in analysis limitations.
- [ ] Dashboard users can see freshness and major quality warnings.

## Minimum Acceptable Standard

- [ ] Schema, required fields, keys, freshness, missingness, duplicates, ranges, and referential integrity are checked before conclusions are trusted.

## Strong Practice

- [ ] Data quality checks run automatically.
- [ ] Quality trends are monitored over time.
- [ ] Quality issues are linked to owners and remediation status.
- [ ] Critical checks fail pipelines rather than silently warning.

## Red Flags

- [ ] No one can state the dataset grain.
- [ ] Joins change row counts without explanation.
- [ ] Missingness spikes align with target or model errors.
- [ ] Unit change looks like model drift.
- [ ] Dashboard or model runs despite stale data.
- [ ] Sensitive data appears in unrestricted output.

