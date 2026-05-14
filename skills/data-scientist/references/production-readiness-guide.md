# Production Readiness Guide

Use this guide when analysis or modeling must run repeatedly, feed a dashboard, score records, support an API, or influence operations.

## Exploratory Code Versus Production Code

Exploratory code:

- Optimized for learning.
- May use notebooks, ad hoc filters, manual steps, and inline charts.
- Can tolerate reruns and temporary objects.
- Often depends on analyst context.

Production-ready code:

- Optimized for repeatability, observability, and maintenance.
- Has explicit inputs, outputs, configs, tests, logs, and owners.
- Handles failures predictably.
- Can be run by a scheduler, API, or another team.
- Preserves lineage and versioning.

Do not call a notebook production-ready because it produced a useful result once.

## Moving From Notebook To Pipeline

Refactor in stages:

1. Freeze the validated logic.
2. Move constants to config.
3. Separate data extraction, validation, feature creation, training, scoring, reporting, and monitoring.
4. Convert repeated code into functions or tasks.
5. Add input/output contracts.
6. Add tests for critical transformations.
7. Add logging and run metadata.
8. Package artifacts and documentation.

Keep the notebook as a narrative report if useful, but make the pipeline the source of operational truth.

## Reproducibility

Record:

- Code version.
- Data version or extraction timestamp.
- Query text or source snapshot.
- Feature definitions.
- Split logic and random seeds.
- Model parameters and artifacts.
- Environment and dependency versions.
- Metrics and evaluation dataset identifiers.

Any reported model result should be traceable to a reproducible run.

## Dependency And Environment Management

Use the user's stack:

- Python: requirements, lockfiles, conda/uv/poetry, containers.
- R: renv, package snapshots, project libraries.
- SQL: versioned queries, dbt models, stored procedures with change control.
- Excel/Sheets: protected formulas, named ranges, documented refresh steps.
- Production: containers, CI, deployment manifests, secrets management.

Avoid unpinned dependencies for production scoring.

## Configs

Configs should hold:

- Source locations.
- Date windows.
- Feature windows.
- Thresholds.
- Model artifact paths.
- Environment-specific settings.
- Alert thresholds.

Do not hide business thresholds deep in code. Version config changes when they affect decisions.

## Data Versioning

Track:

- Source table snapshots or partition cutoffs.
- File hashes or object versions.
- Query version.
- Training dataset ID.
- Exclusion rules.
- Label generation logic.

For spreadsheets, preserve the input workbook version and protect derived sheets from accidental edits.

## Feature Pipelines

Production features need:

- Clear definition and owner.
- Source tables and join keys.
- Prediction-time availability.
- Refresh cadence.
- Null/default behavior.
- Backfill logic.
- Training/scoring parity.
- Drift and quality checks.

Avoid features that require manual refresh, fragile spreadsheet copy-paste, or unavailable future data.

## Model Artifacts

Store:

- Model object.
- Preprocessing pipeline.
- Feature schema and order.
- Category mappings.
- Calibration object if used.
- Training metadata.
- Evaluation report.
- Model card or intended-use note.

The scoring environment must load the exact preprocessing used in training.

## Logging

Log:

- Run ID, timestamp, code version, config version.
- Input row counts and quality check results.
- Model version.
- Prediction counts and score distribution.
- Threshold and action output.
- Errors and warnings.
- Latency and resource use.
- Downstream delivery status.

For individual predictions, log features and outcomes only when allowed by privacy and retention rules.

## Testing

Minimum tests:

- Schema and required field checks.
- Feature transformation tests on known inputs.
- Train/scoring parity checks.
- No-leakage timestamp checks.
- Model artifact load and score smoke test.
- Threshold/action logic tests.
- Backfill and empty-input behavior.
- Monitoring calculation tests.

Test the business rules as carefully as the model.

## Batch Inference

Use when scoring is periodic or high volume.

Define:

- Schedule and freshness requirements.
- Input partition or extract.
- Idempotent output writing.
- Retry behavior.
- Partial failure behavior.
- Delivery target: table, file, dashboard, CRM, email, or queue.

Include reconciliation: input count, scored count, failed count, delivered count.

## Real-Time Inference

Use when decisions need low latency.

Define:

- API contract.
- Authentication and authorization.
- Latency budget.
- Feature retrieval path.
- Timeout and fallback.
- Versioned response schema.
- Monitoring and rate limits.

If online features are unavailable or slow, consider near-real-time batch scoring.

## Monitoring

Monitor:

- Data freshness, schema, volume, missingness, and ranges.
- Feature drift and category drift.
- Prediction drift and score distribution.
- Calibration and performance when labels arrive.
- Business KPIs and guardrails.
- Latency, failures, and downstream delivery.

Set alert thresholds before launch and review them after initial production data.

## Retraining

Define:

- Scheduled retraining cadence, if any.
- Drift or performance triggers.
- Minimum new label volume.
- Champion/challenger evaluation.
- Approval process.
- Rollout plan.

Do not automatically replace a model solely because retraining ran. Compare against the incumbent.

## Failure Handling

Plan for:

- Missing input data.
- Schema changes.
- Empty scoring sets.
- Model artifact load failure.
- Feature pipeline failure.
- API timeout.
- Dashboard refresh failure.
- Bad output discovered after delivery.

For each, define fallback: fail closed, use previous score, use rule-based baseline, suppress action, or alert owner.

## Rollback Planning

Before launch:

- Keep the previous model or rule available.
- Version outputs by model.
- Define rollback triggers.
- Preserve deployment artifacts.
- Make downstream consumers tolerant of rollback.
- Notify owners when rollback occurs.

Rollback is part of deployment, not an emergency improvisation.

## Documentation

Production documentation should include:

- Intended use and non-intended use.
- Data sources and contracts.
- Feature definitions.
- Training and validation summary.
- Model artifact location.
- Scoring schedule or API contract.
- Monitoring dashboard.
- Owners and escalation path.
- Retraining and rollback process.

