# Stage Model

Each stage defines what the assistant should do, what it should not do yet, its inputs, its outputs, and which supporting files are most relevant. Stages map directly to the lifecycle in `lifecycle.md` and connect to gates in `quality-gates.md`.

---

## Stage 0: Intake and Framing

### What to Do
- Ask clarifying questions about the decision, stakeholder, cost of error, and success metric
- Restate the problem as a decision-support task with a named unit of analysis and time window
- Identify constraints: interpretability, latency, fairness, regulatory, or data access
- Draft or outline a project brief
- Surface scope risks and ambiguities for stakeholder alignment

### What Not to Do Yet
- Do not profile data or review schemas
- Do not suggest model families or algorithms
- Do not write code
- Do not define features or splits

### Inputs
- User's problem statement or request
- Any available business context, stakeholder goals, or prior analyses

### Outputs
- **Project Brief** (minimum: decision statement, unit of analysis, success metric, constraints)
- List of open questions for stakeholder

### Relevant Supporting Files
- `references/methodology-guide.md` — framing section
- `templates/project-brief-template.md`
- `checklists/pre-modeling-checklist.md` — Business and Decision Clarity section

---

## Stage 1: Data Understanding and Quality Audit

### What to Do
- Inventory all data sources needed for the target and features
- Profile each source: row count, date range, field types, missingness, duplicates, and key distributions
- Identify join key structure and confirm grain of analysis
- Review candidate leakage fields and document disposition
- Classify data quality issues by severity using `severity-levels.md`
- Produce or draft a data audit

### What Not to Do Yet
- Do not engineer features
- Do not define the training split or run models
- Do not interpret relationships between features and the target
- Do not skip to EDA until the audit is complete

### Inputs
- Project brief from Stage 0
- Access to data sources or schema documentation

### Outputs
- **Data Audit** (field-level profile, quality issues, leakage candidates, sufficiency statement)

### Relevant Supporting Files
- `references/validation-and-leakage-checklist.md`
- `references/diagnostics-guide.md` — data quality section
- `checklists/pre-modeling-checklist.md`
- `templates/data-audit-report-template.md`

---

## Stage 2: Exploratory Analysis

### What to Do
- Analyze target distribution overall, over time, and across segments
- Examine candidate feature distributions and their relationship to the target
- Identify confounders, collinear features, and data collection artifacts
- Explore cohort, segment, and time-based patterns
- Review anomalies and outliers
- Generate and document hypotheses with supporting evidence

### What Not to Do Yet
- Do not define the final feature set — EDA generates candidates, not the production list
- Do not fit models (even informal ones) and present results as validated
- Do not finalize the validation strategy — that comes in Stage 3
- Do not discard EDA observations because they complicate the narrative

### Inputs
- Data Audit from Stage 1
- Project Brief from Stage 0

### Outputs
- **EDA Summary** (target distribution, candidate signals, anomalies, hypotheses)

### Relevant Supporting Files
- `references/methodology-guide.md` — EDA section
- `references/diagnostics-guide.md`
- `references/visualization-guide.md`
- `templates/visual-analysis-workflow.md`
- `examples/` — EDA patterns for the relevant language

---

## Stage 3: Target, Feature, and Validation Design

### What to Do
- Write the formal target definition: event, grain, outcome window, exclusions
- Specify the prediction point precisely
- Confirm every candidate feature is available at the prediction point without future information
- Select and justify the split strategy (random, time-aware, group-aware)
- Define the baseline approach (naive rule, majority class, historical rate, current process)
- Select primary and secondary evaluation metrics with business rationale
- Produce or draft the validation plan

### What Not to Do Yet
- Do not train any model — this stage produces the plan, not the output
- Do not adjust the target definition after seeing model results
- Do not use a split strategy that is convenient rather than correct

### Inputs
- EDA Summary from Stage 2
- Project Brief from Stage 0

### Outputs
- **Validation Plan** (target definition, prediction point, feature list with availability check, split strategy, baseline plan, metrics)

### Relevant Supporting Files
- `references/validation-and-leakage-checklist.md`
- `references/metrics-guide.md`
- `references/methodology-guide.md` — validation section
- `templates/validation-plan-template.md`
- `templates/modeling-plan-template.md` — optional, for complex projects with large experiment scope
- `checklists/pre-modeling-checklist.md`

---

## Stage 4: Baseline Modeling

### What to Do
- Implement the baseline defined in Stage 3 using only permissible features
- Apply all preprocessing inside the validation loop
- Evaluate the baseline on the holdout or validation set
- Check calibration if the output is a probability
- Record results in the experiment log
- Communicate baseline performance to stakeholders

### What Not to Do Yet
- Do not tune the baseline — establish it as-is
- Do not report training-set performance as the result
- Do not advance to complex models until the baseline is confirmed and logged
- Do not interpret baseline performance as a model comparison (only one model exists yet)

### Inputs
- Validation Plan from Stage 3
- Clean data pipeline with confirmed train/test split

### Outputs
- **Experiment Log** — baseline entry (model type, hyperparameters, metrics, notes)
- Baseline code or notebook section

### Relevant Supporting Files
- `references/model-selection-guide.md`
- `references/metrics-guide.md`
- `references/validation-and-leakage-checklist.md`
- `templates/experiment-log-template.md`
- `examples/` — baseline patterns for the relevant language

---

## Stage 5: Model Development and Comparison

### What to Do
- Select candidate model families based on data shape, problem type, interpretability, and operational constraints
- Train each candidate using the same validation strategy as the baseline
- Record all experiments in the experiment log (hyperparameters, metrics, notes)
- Evaluate variance across folds or time windows, not just point estimates
- Compare candidates against each other and the baseline on the pre-defined holdout
- Select the preferred model and document the rationale including non-metric considerations

### What Not to Do Yet
- Do not tune aggressively before understanding baseline variance
- Do not evaluate on the final holdout more than once per candidate
- Do not select a model based only on a single aggregate metric
- Do not allow interpretability or latency requirements to be treated as optional

### Inputs
- Experiment Log baseline entry from Stage 4
- Validation Plan from Stage 3

### Outputs
- **Experiment Log** — full (all candidates)
- **Model Comparison Report** (candidates, metrics, variance, rationale, selection)

### Relevant Supporting Files
- `references/model-selection-guide.md`
- `references/metrics-guide.md`
- `references/validation-and-leakage-checklist.md`
- `templates/modeling-plan-template.md`
- `templates/experiment-log-template.md`
- `templates/model-comparison-report-template.md`
- `examples/` — modeling patterns for the relevant language

---

## Stage 6: Diagnostics and Error Analysis

### What to Do
- Compute error distribution for the selected model on the validation set
- Slice performance by key subgroups (segment, cohort, time, geography, product)
- Review top error cases for patterns (label noise, missing features, model mismatch)
- Check fairness slices if sensitive attributes are relevant
- Assess stability across out-of-time or out-of-distribution samples
- Produce or draft the error analysis report

### What Not to Do Yet
- Do not summarize error analysis as "model performs well overall"
- Do not skip subgroup analysis because the aggregate metric is good
- Do not accept systematic error patterns without investigation or documented justification
- Do not certify the model as production-ready before this stage is complete

### Inputs
- Selected model and experiment log from Stage 5
- Validation set with subgroup labels

### Outputs
- **Error Analysis Report** (error distribution, subgroup breakdowns, top error cases, fairness review, stability check)

### Relevant Supporting Files
- `references/diagnostics-guide.md`
- `references/responsible-ai-guide.md`
- `references/interpretation-templates.md`
- `templates/error-analysis-report-template.md`
- `checklists/responsible-ai-checklist.md`

---

## Stage 7: Calibration, Thresholds, and Decision Policy

### What to Do
- Plot the calibration curve or reliability diagram for the selected model
- Apply calibration correction if needed (Platt scaling, isotonic regression)
- Build a threshold analysis table showing precision, recall, volume, and business cost at each candidate cutoff
- Select a threshold with explicit cost-tradeoff rationale and stakeholder agreement
- Document the decision policy: what happens at each score range, who reviews, what the fallback is
- Produce the calibration report and decision memo

### What Not to Do Yet
- Do not default the threshold to 0.5 without analysis
- Do not choose the threshold without stakeholder input on error costs
- Do not present a final threshold as fixed — document the review trigger

### Inputs
- Selected model from Stage 5
- Error Analysis Report from Stage 6
- Business cost-of-error information from Stage 0

### Outputs
- **Calibration Report**
- **Decision Memo** (threshold, decision policy, business impact estimate, review trigger)

### Relevant Supporting Files
- `references/metrics-guide.md` — calibration and threshold sections
- `references/diagnostics-guide.md` — calibration diagnostics
- `references/decision-science-guide.md`
- `templates/calibration-report-template.md`
- `templates/decision-memo-template.md`

---

## Stage 8: Interpretation and Reporting

### What to Do
- Compute global feature importance or driver analysis and validate against domain knowledge
- Produce local explanations for high-stakes or representative predictions
- Write a model card with intended use, performance, limits, and fairness summary
- Produce a business-language summary or executive report
- Frame recommendations as actions with stated conditions and uncertainty
- Route to the appropriate report template from `templates/`

### What Not to Do Yet
- Do not present feature importance as causal without qualification
- Do not omit model limits from the report
- Do not remove uncertainty from the recommendation language
- Do not produce only technical output without a business translation

### Inputs
- All prior artifacts: project brief, validation plan, experiment log, error analysis, calibration report, decision memo
- Stakeholder audience and communication preferences

### Outputs
- **Model Card**
- Business report or executive summary
- Slide deck or dashboard narrative (if required)

### Relevant Supporting Files
- `references/interpretation-templates.md`
- `references/reporting-templates.md`
- `templates/model-card-template.md`
- `templates/analysis-report-template.md`
- `templates/visual-analysis-workflow.md`

---

## Stage 9: Deployment Readiness

### What to Do
- Define and document the input contract (fields, types, ranges, missing-value handling)
- Define and document the output contract (score semantics, thresholds, downstream consumers)
- Review the scoring pipeline for training-serving skew
- Version model artifacts, feature definitions, and scoring code
- Draft or review the production-readiness report
- Confirm owner, escalation path, and runbook

### What Not to Do Yet
- Do not consider deployment complete when only model performance has been verified
- Do not allow input or output schemas to remain informal
- Do not deploy without a monitoring plan (even a minimal one)

### Inputs
- All prior artifacts
- Engineering or platform requirements for production

### Outputs
- **Deployment Readiness Report**
- Input and output contract documentation
- Versioned artifacts

### Relevant Supporting Files
- `references/production-readiness-guide.md`
- `references/data-quality-and-contracts.md`
- `checklists/deployment-checklist.md`
- `checklists/responsible-ai-checklist.md`
- `templates/deployment-readiness-report-template.md`

---

## Stage 10: Monitoring and Iteration

### What to Do
- Activate data quality, drift, calibration, and business-outcome monitoring
- Review monitoring dashboards on the agreed cadence
- Document the retraining trigger, threshold review schedule, and owner
- Respond to alerts by investigating, escalating, or retraining
- Produce or update the monitoring plan when model or data changes occur

### What Not to Do Yet
- Do not treat deployment as the end of the project
- Do not monitor only technical availability — monitor prediction quality and business outcomes
- Do not allow retraining to happen without logging, versioning, and review

### Inputs
- Deployment Readiness Report from Stage 9
- Live scoring pipeline output and business outcome data

### Outputs
- **Monitoring Plan** (active and current)
- Monitoring dashboard or report
- Retraining log (when applicable)

### Relevant Supporting Files
- `references/model-monitoring-and-drift.md`
- `references/diagnostics-guide.md` — drift and degradation sections
- `templates/monitoring-plan-template.md`
- `checklists/deployment-checklist.md`
