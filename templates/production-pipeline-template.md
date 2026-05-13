# Production Pipeline Template

Use this template when an analysis, model, forecast, recommender, anomaly detector, or scoring process must run repeatedly outside a one-off notebook.

## Required Inputs

- Business owner and operational user.
- Data sources and contracts.
- Feature definitions.
- Model or scoring logic.
- Evaluation results and approval status.
- Runtime target: batch job, API, dashboard refresh, database procedure, or scheduled report.
- Monitoring and rollback requirements.

## Expected Outputs

- Production-ready project outline.
- Config and environment plan.
- Data validation and feature pipeline.
- Training/evaluation and inference flow.
- Model artifact storage plan.
- Monitoring, logging, testing, and documentation plan.
- Retraining and rollback process.

## Project Structure

Example structure:

```text
project/
├── configs/
│   ├── dev.yaml
│   ├── prod.yaml
│   └── thresholds.yaml
├── data_contracts/
│   └── input_contract.md
├── notebooks/
│   └── exploration_or_report.ipynb
├── src/
│   ├── ingest/
│   ├── validate/
│   ├── features/
│   ├── train/
│   ├── evaluate/
│   ├── inference/
│   └── monitoring/
├── tests/
├── artifacts/
├── reports/
└── docs/
```

Adapt to the user's stack. SQL/dbt, R projects, spreadsheets, or workflow tools can use the same logical separation.

## Config Management

Configs should include:

- Source locations.
- Date windows.
- Feature windows.
- Model artifact path.
- Thresholds and business rules.
- Environment-specific settings.
- Monitoring thresholds.

Rules:

- Do not hard-code production thresholds.
- Keep secrets out of config files.
- Version config changes that alter decisions.

## Data Ingestion

Define:

- Source tables, files, APIs, or sheets.
- Query or extract logic.
- Schedule and freshness SLA.
- Incremental versus full refresh.
- Backfill policy.
- Row-count reconciliation.

Outputs:

- Raw snapshot or validated input table.
- Ingestion metadata: run ID, timestamp, source version, row count.

## Data Validation

Validate:

- Schema.
- Required fields.
- Data types.
- Freshness.
- Primary key uniqueness.
- Missingness.
- Valid ranges.
- Category values.
- Referential integrity.
- No future timestamps.

Failure behavior:

- Critical checks fail the run.
- Warning checks log and notify owner.
- Informational checks appear in monitoring.

## Feature Generation

Feature pipeline must:

- Use prediction-time valid data.
- Match training and scoring definitions.
- Handle missing and unseen categories.
- Use trailing windows for temporal features.
- Version feature definitions.
- Record feature row counts and null rates.

Outputs:

- Feature table or matrix.
- Feature metadata.
- Quality check report.

## Train And Evaluate

Training flow:

1. Load validated training data.
2. Generate features.
3. Apply split logic.
4. Fit preprocessing inside training.
5. Train baseline and candidate model.
6. Evaluate on validation/holdout.
7. Run diagnostics and responsible-use checks.
8. Save approved artifact and report.

Evaluation must include baseline, validation design, metrics, diagnostics, and limitations.

## Model Artifact Storage

Store:

- Model object.
- Preprocessing pipeline.
- Feature schema and order.
- Category mappings.
- Calibration object if used.
- Thresholds or policy config.
- Training metadata.
- Evaluation report.
- Model card.

Use artifact version IDs that appear in logs and predictions.

## Batch Inference

Define:

- Schedule.
- Input population.
- Feature generation cutoff.
- Scoring artifact version.
- Output table/file/schema.
- Idempotency rule.
- Retry behavior.
- Delivery destination.

Batch output fields:

| Field | Description |
| --- | --- |
| entity_id | scored entity |
| score | model output |
| prediction | class/value/rank/alert |
| threshold_or_policy | decision rule used |
| model_version | artifact version |
| scored_at | timestamp |
| reason_codes | optional explanations |

## API Inference

Use API inference when low-latency decisions are required.

Define:

- Request schema.
- Response schema.
- Authentication.
- Feature retrieval path.
- Latency budget.
- Timeout and fallback behavior.
- Error responses.
- Rate limits.
- Model versioning.

If live features are unreliable, use precomputed batch scores instead.

## Monitoring

Monitor:

- Job success/failure.
- Runtime and latency.
- Input row count.
- Scored row count.
- Data freshness.
- Feature missingness and drift.
- Prediction drift.
- Threshold action volume.
- Performance when labels arrive.
- Calibration.
- Business KPIs.
- Subgroup metrics where relevant.

Monitoring should have owners and alert thresholds.

## Logging

Log:

- Run ID.
- Code version.
- Config version.
- Data version.
- Model version.
- Input/output counts.
- Validation results.
- Errors and warnings.
- Prediction summaries.
- Delivery status.

For individual-level logs, follow privacy and retention rules.

## Testing

Test:

- Data contract checks.
- Feature transformations on known examples.
- Split logic.
- No future leakage in feature windows.
- Model artifact load.
- Batch scoring smoke test.
- API request/response validation.
- Threshold and business-rule logic.
- Monitoring metric calculations.
- Empty input and failure paths.

Automated tests should cover both code and decision logic.

## Documentation

Document:

- Intended use and non-intended use.
- Owners and escalation.
- Data sources and contracts.
- Feature definitions.
- Training and evaluation method.
- Artifact location.
- Batch/API contract.
- Monitoring dashboard.
- Retraining and rollback process.
- Known limitations.

## Rollback And Retraining Process

Rollback:

- Keep previous artifact available.
- Define rollback triggers.
- Ensure downstream systems can accept previous output.
- Log rollback reason.
- Notify owners.

Retraining:

- Define cadence or triggers.
- Require champion/challenger comparison.
- Re-run validation and responsible-use checks.
- Require approval before promotion.
- Archive old artifacts.

## Step-By-Step Implementation Workflow

1. Convert notebook logic into modular tasks.
2. Write configs and contracts.
3. Implement ingestion and validation.
4. Implement feature generation.
5. Implement training/evaluation.
6. Save artifacts and reports.
7. Implement batch/API inference.
8. Add logging and monitoring.
9. Add tests.
10. Run dry run or shadow mode.
11. Approve launch.
12. Monitor and iterate.

## Validation And Evaluation Guidance

- Production training must reproduce validated notebook results within expected tolerance.
- Scoring must use the same preprocessing and feature order as training.
- Shadow test live data before high-impact launch.
- Verify monitoring works before relying on it.

## Interpretation Guidance

- Production outputs need score semantics, reason codes where possible, and clear action rules.
- Reports should identify model version and data freshness.
- Users must know what to do with the output and when to escalate.

## Common Failure Modes

- Notebook logic manually copied without tests.
- Training and scoring features diverge.
- Thresholds hard-coded in multiple places.
- No behavior for missing or delayed input data.
- Model artifact lacks preprocessing.
- Monitoring starts after launch instead of before.
- Retraining overwrites incumbent without comparison.
- No owner for failures.

## Tool-Flexible Notes

- Python/R: package reusable functions and pin dependencies.
- SQL/dbt: use versioned models and tests for feature tables.
- Excel/Sheets: production use requires locked formulas, refresh documentation, and ownership; avoid fragile manual scoring for high-risk decisions.
- Notebooks: keep for exploration/reporting, not as the only scheduler unless explicitly operationalized.
- APIs: version schemas and provide fallback behavior.
- Dashboards: show data freshness, model version, and definitions.

