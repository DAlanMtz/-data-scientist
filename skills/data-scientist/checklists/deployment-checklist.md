# Deployment Checklist

Use before moving a model, forecast, recommender, anomaly detector, dashboard metric, or scoring rule into recurring operational use.

## Reproducible Pipeline

- [ ] Workflow runs without manual notebook cell ordering.
- [ ] Data ingestion, validation, feature generation, scoring, and reporting are separate steps.
- [ ] Run can be repeated with same inputs.
- [ ] Code version is recorded.
- [ ] Data version or extraction timestamp is recorded.
- [ ] Pipeline has a defined schedule or trigger.

## Environment And Dependencies

- [ ] Runtime environment is documented.
- [ ] Dependencies are pinned or otherwise controlled.
- [ ] System libraries and external services are documented.
- [ ] Secrets are managed outside code.
- [ ] Dev/staging/prod differences are explicit.
- [ ] Container or environment lock is used where appropriate.

## Config Management

- [ ] Source paths, date windows, feature windows, thresholds, and artifact paths are configurable.
- [ ] Business thresholds are not hard-coded in multiple places.
- [ ] Config changes are versioned.
- [ ] Environment-specific config is separated.
- [ ] Rollback config is available.

## Data Validation

- [ ] Input schema is checked.
- [ ] Required fields are checked.
- [ ] Data types are checked.
- [ ] Freshness is checked.
- [ ] Missingness thresholds are checked.
- [ ] Valid ranges and categories are checked.
- [ ] Referential integrity is checked.
- [ ] Critical failures stop the run.

## Feature Consistency

- [ ] Training and scoring feature definitions match.
- [ ] Feature order and schema are fixed.
- [ ] Missing and unseen category behavior is defined.
- [ ] Time-window features use correct cutoff.
- [ ] Feature pipeline is versioned.
- [ ] Feature drift monitoring is defined.

## Model Artifact Storage

- [ ] Model artifact is stored with version ID.
- [ ] Preprocessing artifact is stored with model.
- [ ] Feature schema and mappings are stored.
- [ ] Calibration artifact is stored if used.
- [ ] Evaluation report and model card are linked.
- [ ] Previous production artifact is retained for rollback.

## Batch Inference

- [ ] Input population is defined.
- [ ] Output schema is defined.
- [ ] Idempotency behavior is defined.
- [ ] Retry behavior is defined.
- [ ] Partial failure behavior is defined.
- [ ] Delivery destination is validated.
- [ ] Scored count is reconciled to input count.

## API Inference

- [ ] Request and response schemas are versioned.
- [ ] Authentication and authorization are defined.
- [ ] Latency budget is defined.
- [ ] Timeout and fallback behavior are defined.
- [ ] Rate limiting is considered.
- [ ] Error messages do not leak sensitive data.
- [ ] API logs include model version and request metadata allowed by privacy rules.

## Logging

- [ ] Run ID is logged.
- [ ] Code/config/data/model versions are logged.
- [ ] Input/output counts are logged.
- [ ] Validation results are logged.
- [ ] Errors and warnings are logged.
- [ ] Prediction summaries are logged.
- [ ] Individual prediction logs follow privacy and retention policy.

## Monitoring And Alerting

- [ ] Pipeline success/failure is monitored.
- [ ] Data freshness is monitored.
- [ ] Data quality is monitored.
- [ ] Feature drift is monitored.
- [ ] Prediction drift is monitored.
- [ ] Performance is monitored when labels arrive.
- [ ] Calibration is monitored when probabilities are used.
- [ ] Business KPIs and guardrails are monitored.
- [ ] Alerts have owners and response SLAs.

## Retraining And Rollback

- [ ] Retraining cadence or trigger is defined.
- [ ] Champion/challenger comparison is required before promotion.
- [ ] Approval gate is defined.
- [ ] Rollback trigger is defined.
- [ ] Rollback artifact and config are available.
- [ ] Downstream consumers can tolerate rollback.

## Security And Privacy

- [ ] Access controls are defined.
- [ ] PII/sensitive data handling is documented.
- [ ] Logs avoid unnecessary sensitive data.
- [ ] Retention policy is defined.
- [ ] Data sharing and API exposure are approved.
- [ ] Abuse or misuse risk is considered.

## Documentation And Ownership

- [ ] Intended use is documented.
- [ ] Input/output contracts are documented.
- [ ] Feature definitions are documented.
- [ ] Monitoring dashboard is documented.
- [ ] Runbook exists.
- [ ] Owner and backup owner are assigned.
- [ ] Incident response path is defined.

## Minimum Acceptable Standard

- [ ] Reproducible run, data validation, versioned artifact, logging, monitoring, owner, rollback path, and documentation exist.

## Strong Practice

- [ ] Shadow mode or dry run is completed before launch.
- [ ] Automated tests cover feature generation and scoring.
- [ ] Monitoring alerts are tested before production use.
- [ ] Model card and runbook are linked from the pipeline.

## Red Flags

- [ ] Production process is a manually run notebook.
- [ ] Training and scoring code use different feature logic.
- [ ] Model artifact lacks preprocessing.
- [ ] No owner for pipeline failure.
- [ ] No rollback plan.
- [ ] Monitoring is planned after launch rather than before.

