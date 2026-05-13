# Excel Data Cleaning Patterns

## Use Case

Clean and validate smaller datasets in Excel or Google Sheets for analysis, stakeholder review, or lightweight reporting.

## Expected Inputs

- Raw tabular data.
- Expected columns, key fields, data types, allowed values, and required fields.
- Business rules for missing values and duplicates.

## Expected Outputs

- Preserved raw sheet.
- Cleaned working sheet.
- Data quality issue log.
- Validation rules and lookup checks.

## Concise Workflow

1. Keep raw data unchanged.
2. Create a cleaned copy or Power Query step.
3. Standardize text, dates, numbers, and categories.
4. Check missingness, duplicates, valid ranges, and lookups.
5. Document every manual rule.

## Spreadsheet Patterns

### Preserve Raw Data

- Keep `raw_data` locked or read-only.
- Create `clean_data` for formulas or Power Query output.
- Create `quality_checks` for issue counts.

### Trim And Clean Text

```text
=TRIM(CLEAN(A2))
```

Use for names, categories, IDs, and imported text. Do not apply blindly to free text where spacing may matter.

### Standardize Case

```text
=UPPER(TRIM(A2))
=LOWER(TRIM(A2))
=PROPER(TRIM(A2))
```

Use for controlled categories only.

### Type Conversion

```text
=VALUE(A2)
=DATEVALUE(A2)
=--A2
```

After conversion, check failures instead of hiding errors.

### Missing Value Flags

```text
=IF(ISBLANK(A2),"missing","present")
```

For required fields:

```text
=IF(ISBLANK(A2),"FAIL: required field missing","OK")
```

### Duplicate Checks

```text
=COUNTIF($A:$A,A2)>1
```

For composite keys:

```text
=COUNTIFS($A:$A,A2,$B:$B,B2)>1
```

### Lookup/Referential Checks

```text
=IF(ISNA(MATCH(A2,valid_customer_ids,0)),"missing reference","OK")
```

Or:

```text
=XLOOKUP(A2,dim_customers[customer_id],dim_customers[segment],"missing")
```

### Valid Range Checks

```text
=IF(OR(A2<0,A2>1),"invalid rate","OK")
=IF(B2>TODAY(),"future date","OK")
```

### Data Validation Rules

- Use dropdowns for controlled categories.
- Use date validation for date fields.
- Use numeric min/max validation for rates, ages, quantities, and percentages.
- Use input messages to define expected values.

## Validation And Quality Checks

- Count rows before and after cleaning.
- Check required fields.
- Check duplicate keys.
- Check invalid categories.
- Check impossible dates and ranges.
- Compare totals against source/control totals.
- Use conditional formatting for failures.

## Interpretation Notes

- Spreadsheet cleaning should be traceable: formulas, Power Query steps, or documented manual changes.
- Manual edits are risks; preserve an issue log with old value, new value, reason, and owner.
- For recurring work, promote checks into scripts, SQL, or Power Query rather than repeated manual cleanup.

## Common Mistakes To Avoid

- Editing raw data directly.
- Sorting one column without sorting the full table.
- Converting IDs to numbers and losing leading zeros.
- Hiding errors with `IFERROR` before understanding them.
- Copy-paste overwriting formulas without review.
- Using inconsistent category labels across sheets.

