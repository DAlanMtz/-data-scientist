# Artifacts

Artifacts are the concrete deliverables of data science work. They create shared understanding, enable review, and provide a basis for handoff. Producing a well-defined artifact is more durable than giving general commentary.

Each artifact has a minimum version (enough to advance or communicate) and a strong version (complete, auditable, stakeholder-ready). Always produce at least the minimum version before advancing through a quality gate.

---

## Project Brief

### Purpose
Document the framing of the work: the decision it supports, the stakeholder, the success criteria, and the constraints. The project brief is the reference document for all subsequent decisions.

### When to Produce It
At the end of Stage 0. Update it if scope, success criteria, or constraints change.

### Minimum Contents
- Problem statement (as a decision, not a model type)
- Named stakeholder or decision-maker
- Unit of analysis (grain) and time window
- Primary success metric and threshold
- At least one identified constraint (interpretability, latency, fairness, regulatory, or "none")
- Open questions list

### Strong Version Contents
- Full decision hierarchy (primary decision, sub-decisions, downstream actions)
- Business context: current process, cost of errors, expected volume
- Stakeholder map: who produces output, who consumes it, who approves it
- Fairness, privacy, and regulatory review
- Out-of-scope items explicitly listed
- Assumptions log
- Success metric with decomposition into model metric + business outcome

### Related Templates/Checklists
- `templates/project-brief-template.md`
- `checklists/pre-modeling-checklist.md` — Business and Decision Clarity section

---

## Data Audit

### Purpose
Document the quality, coverage, and trustworthiness of the data that will support the analysis. The data audit is the primary defense against leakage, silent quality failures, and scope mismatch.

### When to Produce It
At the end of Stage 1. Update it if new data sources are introduced or data quality issues surface during EDA or modeling.

### Minimum Contents
- List of data sources with row counts, date ranges, and grain
- Field-level missingness summary for all key fields
- Duplicate check results at the grain of analysis
- Join key validation results
- Leakage candidate list with disposition for each field
- Sufficiency statement: data is (or is not) adequate for the defined scope

### Strong Version Contents
- Full data lineage (source system → transformation → analytic table)
- Time coverage analysis including gaps and migrations
- Field-level distribution summaries for all modeling inputs
- Known data quality issues with severity classification (see `severity-levels.md`)
- Lag analysis: time between event and data availability
- Data access and refresh cadence documentation
- Recommended data exclusions with rationale

### Related Templates/Checklists
- `references/validation-and-leakage-checklist.md`
- `templates/data-audit-report-template.md`
- `checklists/pre-modeling-checklist.md`

---

## EDA Summary

### Purpose
Communicate the key findings from exploratory analysis: what the target looks like, which features are candidate signals, what the anomalies are, and what hypotheses are supported or refuted.

### When to Produce It
At the end of Stage 2. May be an annotated notebook section, a structured document, or a slide deck depending on the audience.

### Minimum Contents
- Target distribution overall and over at least one dimension (time, segment, or cohort)
- Top 3–5 candidate feature relationships with supporting evidence
- At least one anomaly or outlier reviewed and dispositioned
- List of hypotheses generated with evidence for each

### Strong Version Contents
- Target distribution across all key segments and time periods
- Full candidate feature evaluation with correlation, conditional distributions, and leakage review
- Confounder and collinearity analysis
- Cohort and segment-level behavioral differences
- Anomaly analysis with severity classification
- Visual portfolio with annotated interpretation
- Revised scope or framing recommendations if EDA reveals new constraints

### Related Templates/Checklists
- `templates/eda-summary-template.md`
- `templates/visual-analysis-workflow.md`
- `references/visualization-guide.md`
- `references/diagnostics-guide.md`

---

## Validation Plan

### Purpose
Lock in the target definition, feature construction rules, split strategy, baseline approach, and evaluation metrics before any modeling begins. The validation plan prevents the most common and most expensive data science errors.

### When to Produce It
At the end of Stage 3. The validation plan is not updated after modeling begins — changes to the plan must be documented and justified.

### Minimum Contents
- Target definition (event, grain, outcome window, exclusions)
- Prediction point specification
- Feature list with availability confirmation at prediction point
- Split strategy with rationale
- Baseline strategy
- Primary evaluation metric with business rationale

### Strong Version Contents
- Full target definition including edge cases and known ambiguities
- Prediction point with timestamp column and lag specification
- Feature-by-feature availability audit (available at prediction point: yes/no/conditional)
- Split strategy with implementation details (fold count, time boundaries, group keys)
- Baseline implementation specification
- Primary and secondary metrics with formulas and business translation
- Holdout set specification (size, time period, exclusion rules)
- Pre-registered hypotheses for model comparison

### Related Templates/Checklists
- `references/validation-and-leakage-checklist.md`
- `references/metrics-guide.md`
- `templates/validation-plan-template.md`
- `checklists/pre-modeling-checklist.md`

---

## Modeling Plan

### Purpose
Document the intended modeling approach before building it — which model families to explore, why, in what order, and how they will be compared.

### When to Produce It
Optionally at Stage 3 or the start of Stage 5 for complex projects. Most valuable when multiple stakeholders have opinions on approach or when the experiment scope is large.

### Minimum Contents
- Rationale for candidate model families
- Hyperparameter search strategy
- Expected experiment count and compute budget
- Stopping criteria for the experiment phase

### Strong Version Contents
- Model family selection rationale tied to data shape, interpretability, and operational constraints
- Feature engineering plan (transformations, interactions, embeddings)
- Hyperparameter search method (grid, random, Bayesian) and budget
- Evaluation plan (same as validation plan, cross-referenced)
- Model complexity ladder (start simple, add complexity with evidence)
- Risk review: overfitting risk, instability risk, interpretability risk

### Related Templates/Checklists
- `templates/modeling-plan-template.md`
- `references/model-selection-guide.md`
- `templates/experiment-log-template.md`

---

## Experiment Log

### Purpose
Track every model experiment — configuration, results, and observations — so that model selection is reproducible and auditable.

### When to Produce It
Starting at Stage 4 (baseline entry) and maintained throughout Stage 5. Updated whenever a new experiment is run.

### Minimum Contents
- Experiment ID or name
- Model family and key hyperparameters
- Training data version and date
- Validation strategy used
- Primary metric result on validation set
- Notes on any anomaly or observation

### Strong Version Contents
- Full hyperparameter configuration
- All metrics (primary, secondary, calibration, stability)
- Cross-fold or time-fold variance
- Subgroup performance summary
- Feature set version or hash
- Code commit or artifact reference
- Decision notes: why advanced, modified, or rejected

### Related Templates/Checklists
- `templates/experiment-log-template.md`
- `references/metrics-guide.md`

---

## Model Comparison Report

### Purpose
Communicate the results of the model development phase — which candidates were evaluated, how they compared, and why the preferred model was selected.

### When to Produce It
At the end of Stage 5.

### Minimum Contents
- List of candidates with model family and key configuration
- Primary metric comparison (validation set)
- Baseline performance for reference
- Selected model with rationale

### Strong Version Contents
- Full metric comparison table (primary, secondary, calibration)
- Cross-fold or time-fold variance for each candidate
- Subgroup performance comparison
- Interpretability and operational fit assessment
- Non-metric selection criteria (maintenance, latency, explainability)
- Risk summary for the selected model
- Recommendation and next steps (diagnostics, calibration)

### Related Templates/Checklists
- `templates/model-comparison-report-template.md`
- `templates/experiment-log-template.md`
- `references/model-selection-guide.md`
- `references/metrics-guide.md`

---

## Error Analysis Report

### Purpose
Document where the selected model fails, which subgroups are most affected, and what the failure patterns reveal about model limitations, data quality, or scope mismatch.

### When to Produce It
At the end of Stage 6.

### Minimum Contents
- Error distribution summary (regression: residual distribution; classification: confusion matrix)
- Performance on at least three subgroups or dimensions
- Top error cases reviewed and categorized
- Summary of systematic error patterns with disposition

### Strong Version Contents
- Residual or error distribution plots (overall and by segment)
- Full subgroup performance breakdown
- Top-N error case review with error categorization (label noise, missing feature, model mismatch, data quality)
- Fairness slice analysis (if applicable)
- Out-of-time or out-of-distribution stability check
- Error-driven model improvement recommendations
- Known risks and accepted limitations

### Related Templates/Checklists
- `references/diagnostics-guide.md`
- `references/responsible-ai-guide.md`
- `checklists/responsible-ai-checklist.md`
- `templates/error-analysis-report-template.md`

---

## Calibration Report

### Purpose
Document whether predicted probabilities or scores are well-calibrated and whether correction was applied.

### When to Produce It
At Stage 7. May be embedded in the decision memo for simpler projects.

### Minimum Contents
- Calibration curve or reliability diagram
- Assessment: well-calibrated / requires correction / poorly calibrated
- Calibration method applied (if any)
- Post-correction curve (if correction applied)

### Strong Version Contents
- Calibration curve overall and by key subgroup
- Brier score or Expected Calibration Error (ECE)
- Comparison of pre- and post-correction calibration
- Rationale for calibration method selected
- Known limits of the calibration (population, time period)

### Related Templates/Checklists
- `templates/calibration-report-template.md`
- `references/metrics-guide.md` — calibration section
- `references/diagnostics-guide.md`

---

## Decision Memo

### Purpose
Document the operational decision policy derived from the model — the threshold, the actions at each score range, human review rules, and the escalation or fallback path.

### When to Produce It
At Stage 7. Must be reviewed and agreed by the decision stakeholder before production.

### Minimum Contents
- Selected threshold with rationale
- Error cost assumptions used to select the threshold
- Action at each score range (above threshold, below threshold, review band)
- Threshold review trigger

### Strong Version Contents
- Threshold analysis table (precision, recall, volume, business cost at each candidate)
- Cost-of-error assumptions with source
- Decision policy: score range → action → owner → review path
- Expected business impact at selected threshold (volume, cost, revenue)
- Human review tier definition and capacity
- Fallback rule if model is unavailable
- Threshold review schedule and owner

### Related Templates/Checklists
- `references/metrics-guide.md`
- `references/decision-science-guide.md`
- `templates/decision-memo-template.md`

---

## Model Card

### Purpose
Provide a structured, auditable summary of the model's intended use, performance, limitations, and responsible AI considerations. The model card is the canonical reference for anyone who uses, maintains, or audits the model.

### When to Produce It
At Stage 8. Updated when the model is retrained or materially changed.

### Minimum Contents
- Model name, version, and owner
- Intended use and target population
- Training data description (sources, time period, exclusions)
- Evaluation dataset and method
- Primary and secondary performance metrics
- Known limitations and out-of-scope uses

### Strong Version Contents
- Full model description (family, hyperparameters, feature set)
- Training and evaluation data lineage
- Complete performance table (overall and by subgroup)
- Fairness analysis summary
- Calibration summary
- Interpretability summary (top drivers, explanation method)
- Ethical considerations and responsible AI review
- Deployment conditions (input contract, output contract, monitoring)
- Version history

### Related Templates/Checklists
- `templates/model-card-template.md`
- `checklists/responsible-ai-checklist.md`
- `checklists/deployment-checklist.md`

---

## Deployment Readiness Report

### Purpose
Certify that the model, pipeline, and operational process meet the requirements for production deployment. This artifact is the formal sign-off before a model goes live.

### When to Produce It
At Stage 9. Must be completed and reviewed before deployment.

### Minimum Contents
- Input contract summary
- Output contract summary
- Training-serving skew review result
- Artifact versioning confirmation
- Monitoring plan reference
- Named owner and escalation path

### Strong Version Contents
- Full input contract (field-by-field)
- Full output contract (score semantics, downstream consumers, latency)
- Training-serving skew test results
- Artifact inventory (model file, feature definitions, scoring code, dependencies)
- Environment parity confirmation (training vs. serving)
- Monitoring plan summary with alert thresholds
- Rollback and fallback documentation
- Responsible AI and compliance review sign-off
- Deployment sign-off log

### Related Templates/Checklists
- `references/production-readiness-guide.md`
- `references/data-quality-and-contracts.md`
- `checklists/deployment-checklist.md`
- `checklists/responsible-ai-checklist.md`

---

## Monitoring Plan

### Purpose
Define how the deployed model will be observed, what degradation looks like, and what actions will be taken when issues are detected.

### When to Produce It
Drafted at Stage 9, activated at Stage 10. Updated when the model, data, or business context changes.

### Minimum Contents
- At least one monitoring metric with definition and alert threshold
- Review cadence (daily, weekly, monthly)
- Named owner for monitoring and alert response
- Retraining trigger definition

### Strong Version Contents
- Full monitoring metric set: data quality, feature drift, prediction drift, calibration, business outcomes
- Alert threshold table with response action for each
- Review cadence and escalation path
- Retraining trigger criteria (metric-based, schedule-based, or event-based)
- Rollback criteria
- Monitoring dashboard reference
- Incident log format
- Review schedule with dates and owner

### Related Templates/Checklists
- `references/model-monitoring-and-drift.md`
- `templates/monitoring-plan-template.md`
- `checklists/deployment-checklist.md`

---

## Visual Report

### Purpose
Communicate analysis findings through a decision-first visual narrative. A visual report is for stakeholders who need a clear answer, evidence, limitations, and recommended action rather than a chart dump.

### When to Produce It
At Stage 8 when results need stakeholder communication, executive review, or a polished narrative output. It may also summarize Stage 2 EDA when the goal is exploratory communication rather than modeling.

### Minimum Contents
- Audience and decision supported
- Business question and data used
- Executive visual summary
- Key metrics with definitions and denominators
- Chart inventory mapping each visual to a question
- Findings with captions and takeaways
- Limitations and uncertainty
- Recommendation and next action

### Strong Version Contents
- Full visual story sequence with hierarchy and appendix separation
- Consistent design system for typography, layout, color, captions, and tables
- Stakeholder-ready captions that state implications
- Uncertainty visualized where it changes the decision
- Export/readability review for the target medium
- Quality checklist completed

### Related Templates/Checklists
- `templates/visual-report-template.md`
- `templates/html-report-template.md`
- `references/visual-report-design-system.md`
- `references/visual-storytelling-guide.md`
- `checklists/visual-report-checklist.md`

---

## Dashboard Design Brief

### Purpose
Define the decision, audience, metrics, layout, data dependencies, and operating workflow before building a dashboard.

### When to Produce It
Before creating or redesigning a dashboard, BI report, spreadsheet dashboard, notebook dashboard, or app-based analytics view.

### Minimum Contents
- Dashboard name and owner
- Audience/users and decisions supported
- Primary KPIs and metric definitions
- Data sources, grain, and refresh cadence
- Filters/slicers and default views
- Page/layout plan and visual hierarchy
- Access/privacy needs
- Success criteria and maintenance owner

### Strong Version Contents
- User workflows with drill-down and export needs
- Alerts, thresholds, and escalation actions
- Data quality dependencies and visible freshness/status requirements
- Explicit unsupported decisions and out-of-scope uses
- Stakeholder acceptance criteria
- QA plan linked to publish decision

### Related Templates/Checklists
- `templates/dashboard-design-brief-template.md`
- `templates/dashboard-qa-checklist-template.md`
- `references/visual-report-design-system.md`
- `references/visual-storytelling-guide.md`
- `checklists/dashboard-qa-checklist.md`

---

## Dashboard QA Checklist

### Purpose
Certify that a dashboard is accurate, readable, secure, performant, and usable before publication or material change.

### When to Produce It
Before publishing a new dashboard, after major metric or source changes, and during recurring dashboard audits.

### Minimum Contents
- Data freshness verification
- Metric definition checks
- Filter behavior checks
- Aggregation, grain, total, and subtotal checks
- Cross-visual consistency checks
- Permissions/privacy checks
- Performance and export/share checks
- Stakeholder signoff decision

### Strong Version Contents
- Source reconciliation evidence for primary KPIs
- User-group permission test results
- Mobile/screen-size review when relevant
- Severity-labeled issues with owners and due dates
- Publish decision: approve, approve with conditions, or reject
- Maintenance and review cadence confirmation

### Related Templates/Checklists
- `templates/dashboard-qa-checklist-template.md`
- `templates/dashboard-design-brief-template.md`
- `checklists/dashboard-qa-checklist.md`

---

## HTML Report

### Purpose
Provide a self-contained, dependency-light report format for polished browser review, PDF export, or static sharing when markdown is not enough.

### When to Produce It
When the user needs a polished visual report, PDF-ready output, browser-rendered artifact, or static handoff that should preserve layout and styling.

### Minimum Contents
- Report title, audience, decision supported, and data freshness
- Executive summary
- KPI cards
- Chart containers with takeaway titles/captions
- Findings table or section
- Limitations
- Recommendations and next action
- Print/export guidance

### Strong Version Contents
- Design tokens for typography, color, spacing, layout, and status colors
- Responsive and print-friendly CSS
- Accessible semantic HTML structure
- Readable table styling
- Export QA notes
- Links to visual design and storytelling references

### Related Templates/Checklists
- `templates/html-report-template.md`
- `templates/visual-report-template.md`
- `references/visual-report-design-system.md`
- `references/visual-storytelling-guide.md`
- `checklists/visual-report-checklist.md`
