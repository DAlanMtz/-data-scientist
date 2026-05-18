# Production Readiness

> Confirm that the model has a defined input/output contract, a monitoring plan, rollback criteria, and that the scoring population matches the training population.

> **Note:** Skip this checklist if the model is pre-production. Mark all items as "Not yet applicable — pre-production" rather than leaving them as open issues.

## What to inspect

- **Input contract** — is the input schema defined? what happens if expected features are missing, null, or outside the expected range? is there input validation at scoring time?
- **Output contract** — are score semantics documented? what do high and low scores mean? who are the downstream consumers, and how do they use the score?
- **Shadow period evidence** — did the model run in shadow mode (scoring silently alongside the existing system) before going live? if not, what evidence justifies skipping it?
- **Monitoring plan** — is there an active monitoring plan covering data quality, prediction drift, and business outcome tracking? are alerts defined?
- **Rollback criteria** — what conditions trigger a rollback? is there an automated or manual rollback path? is the previous model version still available?
- **Retraining triggers** — what conditions trigger retraining (time-based, performance-based, population shift)? who owns retraining? is there a documented retraining schedule or process?
- **Stale population risk** — is the training population representative of the current scoring population? how much time has passed since training? has the product, market, or user behavior changed?
- **Responsible AI gaps** — were fairness, disparate impact, or harm potential assessed before deployment? are affected populations identified?

## Red flags

- No input schema defined; missing features cause silent failures or unexpected behavior
- No monitoring in place; "we'll add monitoring later"
- No rollback plan and no prior model version available
- Model trained more than 12 months ago with no retraining review
- No shadow period for a consequential model with no precedent
- Responsible AI assessment never performed; no documentation of affected populations
- Scoring population has drifted substantially from training population with no documented assessment

## Required evidence

- Input contract: schema definition with feature names, types, expected ranges, and missing-value behavior
- Output contract: score semantics documentation, downstream consumer list, and usage description
- Monitoring dashboard or alert definitions covering data quality and prediction distribution
- Rollback runbook or documented rollback criteria and process
- Population comparison between the training period and the current production scoring population
- Responsible AI assessment or documented rationale for why one is not required

If any of these are missing, mark as an open item in the audit report.

## Fix / retest guidance

- If no input contract: define schema with types and valid ranges; add input validation to the scoring pipeline before re-deployment
- If no monitoring: define at minimum: data quality checks, score distribution monitoring, and business outcome tracking; instrument before expanding rollout
- If no rollback plan: document the rollback trigger conditions, the mechanism, and the responsible owner; confirm the prior model artifact is available
- If population drift is suspected: run a distribution comparison between training-period features and current-period features; compute PSI or equivalent drift metrics; flag features with high drift
- See parent skill `workflow/` Production Mode and `references/` production, monitoring, and data contract guides for detailed implementation guidance
