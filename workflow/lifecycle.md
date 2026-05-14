# Data Science Lifecycle

The lifecycle defines the full arc of a data science project from initial framing through deployed monitoring. Each stage has a defined purpose, key questions, required evidence, a main artifact, common failure patterns, and explicit exit criteria.

Projects do not always follow this order linearly. They loop, skip stages with justification, or run stages in parallel. The lifecycle names the stages so that deviations are deliberate rather than accidental.

---

## Stage 0: Intake and Framing

### Purpose
Translate a business request, problem statement, or data question into a well-scoped analytic problem with a clear decision target, success criteria, and stakeholder alignment.

### Key Questions
- What decision or action does this analysis support?
- Who makes the decision, and what are the stakes if the model is wrong?
- What would a good outcome look like, and how will we measure it?
- What is the prediction or analysis grain — one row per what?
- What is the time window, population, and exclusion logic?
- What are the cost and asymmetry of different error types?
- Are there fairness, privacy, legal, or regulatory constraints?

### Required Evidence
- Written problem statement with named stakeholder and decision
- Proposed success metric with threshold
- Proposed unit of analysis and time window
- Identified constraints (data access, latency, interpretability, fairness)

### Main Artifact
**Project Brief** — see `artifacts.md`

### Common Red Flags
- The "problem" is stated as a model type ("build a churn model") rather than a decision ("identify accounts to offer retention discounts")
- No stakeholder identified for the output
- Success defined only in model-metric terms with no business translation
- Scope is unbounded ("analyze all our data")
- Conflicting stakeholder goals not surfaced

### Exit Criteria
- Decision or question is documented and agreed
- Unit of analysis, time window, and population are defined
- Primary evaluation metric is named with its business rationale
- At least one constraint (interpretability, latency, fairness, regulatory) is documented or explicitly noted as unconstrained
- A project brief exists or can be produced

---

## Stage 1: Data Understanding and Quality Audit

### Purpose
Assess whether the available data is sufficient, correctly structured, and trustworthy enough to support the framing defined in Stage 0.

### Key Questions
- What tables, fields, and joins are needed for the target and features?
- What is the time coverage, granularity, and completeness of each data source?
- Where is data missing, duplicated, or anomalously distributed?
- Are there known data quality issues, system migrations, or collection artifacts?
- What is the earliest usable history? What is the lag between event and record?
- Are there potential leakage fields — data that would not be available at prediction time?

### Required Evidence
- Row counts, date ranges, and field-level missingness by data source
- Duplicate check results at the grain of analysis
- Key field distribution summaries (IDs, dates, target field, join keys)
- List of candidate leakage fields with disposition
- At least one known data quality issue documented or "none found" confirmed

### Main Artifact
**Data Audit** — see `artifacts.md`

### Common Red Flags
- Data is accepted without profiling
- Join keys have unexpected many-to-many structure
- Target field has suspiciously low missingness or perfect values
- Date fields have gaps, future values, or known system migrations
- No lag analysis performed when the target is a future event
- Leakage candidates identified but not resolved before modeling begins

### Exit Criteria
- All data sources profiled at field level
- Duplicates checked and resolved or documented
- Leakage candidates reviewed and dispositioned
- Data quality issues classified by severity
- Data audit artifact produced
- A clear "data is sufficient for the defined scope" or "data is insufficient — here is what is missing" statement

---

## Stage 2: Exploratory Analysis

### Purpose
Develop a working understanding of distributions, relationships, cohorts, time patterns, anomalies, and candidate signals before committing to a modeling approach.

### Key Questions
- What does the target distribution look like across time, cohorts, and segments?
- Which candidate features have strong, consistent, and non-leaky relationships with the target?
- Are there confounders, collinearities, or data collection artifacts that explain apparent relationships?
- Are there natural segments or subpopulations with different behavior?
- What anomalies or outliers exist, and do they represent real variation or data errors?
- What hypotheses does the exploration generate or refute?

### Required Evidence
- Target distribution summary (overall and over time)
- Top candidate feature relationships (correlation, crosstab, or conditional distributions)
- At least one segmentation or cohort view
- Anomaly or outlier summary
- List of hypotheses generated with supporting evidence

### Main Artifact
**EDA Summary** — see `artifacts.md`

### Common Red Flags
- EDA is skipped because "the data looks fine"
- Only one segment or cohort examined
- Relationships interpreted without checking for leakage or confounders
- EDA performed on the full dataset when a time-aware split would be appropriate
- No hypotheses documented — EDA treated as decoration rather than input to modeling decisions

### Exit Criteria
- Target and feature distributions understood across key segments and time periods
- At least three candidate signal hypotheses documented with evidence
- Major anomalies reviewed and dispositioned
- EDA summary produced or substantially drafted

---

## Stage 3: Target, Feature, and Validation Design

### Purpose
Formally define the prediction target, feature construction rules, and validation strategy before writing modeling code. This stage prevents the most expensive and hardest-to-detect errors in data science work.

### Key Questions
- Is the target definition precisely stated — what event, at what grain, over what outcome window?
- Is there a clean prediction point — the timestamp before which all features must be derived?
- Which features are permissible — available at the prediction point without future information?
- How should the population be split for training and evaluation?
- Is a random split appropriate, or are time-aware, group-aware, or geography-aware splits needed?
- How will model performance be measured, and against what baseline?

### Required Evidence
- Written target definition including event, grain, outcome window, and any exclusions
- Prediction point specification
- Feature list with availability confirmation at prediction point
- Split strategy with rationale
- Baseline strategy (naive rule, majority class, historical average, or current process)
- Primary and secondary evaluation metrics with business rationale

### Main Artifact
**Validation Plan** — see `artifacts.md`

### Common Red Flags
- Target definition remains informal ("churn", "conversion", "fraud")
- No prediction point defined — features include anything in the data
- Random split applied to temporal or grouped data
- Evaluation metrics chosen for familiarity rather than business cost alignment
- Baseline not defined before modeling begins
- No plan for out-of-time or out-of-sample evaluation

### Exit Criteria
- Target definition is written and unambiguous
- Prediction point is defined and enforced in feature logic
- Feature list exists with leakage confirmation for each field
- Split strategy is documented with rationale
- Baseline strategy is agreed
- Validation plan artifact produced or substantially drafted

---

## Stage 4: Baseline Modeling

### Purpose
Establish a defensible minimum-performance floor before developing complex models. A baseline reveals whether advanced methods add value, provides a reference for diagnostics, and surfaces implementation issues early.

### Key Questions
- What is the simplest rule or model that a reasonable analyst would consider acceptable?
- Does the baseline use only features available at the prediction point?
- How does the baseline perform on the validation set defined in Stage 3?
- Are there obvious calibration or threshold issues even at baseline?
- Is the implementation reproducible, with no leakage introduced in the pipeline?

### Required Evidence
- Baseline definition (rule, majority class, linear model, historical rate, or current process)
- Performance metrics on the holdout or validation set
- Calibration check if the output is a probability
- Leakage check on the baseline feature set and pipeline

### Main Artifact
**Experiment Log** — baseline entry; see `artifacts.md`

### Common Red Flags
- Baseline skipped because "the problem is complex"
- Baseline uses features that are not available at prediction time
- Baseline performance is reported only on the training set
- Preprocessing applied outside the validation fold for the baseline
- Baseline performance is interpreted as the ceiling rather than the floor

### Exit Criteria
- At least one baseline model trained and evaluated on the validation set
- Baseline metrics recorded in the experiment log
- Baseline implementation confirmed free of leakage
- Baseline performance is understood and communicated to stakeholders

---

## Stage 5: Model Development and Comparison

### Purpose
Develop candidate models systematically, compare them against each other and the baseline using the pre-defined validation strategy, and select the best approach based on performance, interpretability, stability, and operational fit.

### Key Questions
- Which model families are appropriate given data shape, problem type, and constraints?
- How do candidate models compare against the baseline and each other on the held-out evaluation set?
- Are performance differences meaningful or within variance across folds?
- Which model is most stable across time periods, cohorts, or operational slices?
- Which model best satisfies the interpretability, latency, and maintenance requirements?

### Required Evidence
- Experiment log with all candidate models, hyperparameters, and metrics
- Cross-validation or time-fold performance summaries with variance
- Subgroup or cohort performance for each candidate
- Final model selection rationale with business constraints considered

### Main Artifact
**Experiment Log** (full) + **Model Comparison Report** — see `artifacts.md`

### Common Red Flags
- Model selection based on a single aggregate metric
- No variance or confidence interval reported across folds
- Only one candidate model evaluated
- Tuning performed before the split and metric are locked
- Model selected based on training-set performance
- Interpretability or latency requirements ignored until after model selection

### Exit Criteria
- At least two candidate approaches evaluated (one of which is the baseline)
- All evaluation performed on the pre-defined holdout or validation set
- Model comparison report drafted
- Preferred model selected with documented rationale

---

## Stage 6: Diagnostics and Error Analysis

### Purpose
Understand where the selected model succeeds, where it fails, and why. Diagnostics protect against deploying a model that works well on aggregate but fails on the population or scenarios that matter most.

### Key Questions
- What are the systematic error patterns — which subgroups, time periods, or feature ranges are hardest to predict?
- Are residuals or errors distributed as expected, or do patterns reveal model assumptions violated?
- Are there individual high-error or high-stakes cases that require review?
- Does error analysis reveal missing features, label noise, data quality issues, or model mismatch?
- How does performance hold across out-of-time or out-of-geography slices?

### Required Evidence
- Residual or error distribution plots (regression) or confusion matrix breakdown (classification)
- Performance by key subgroups (segment, cohort, time period, product line, geography)
- Top error cases reviewed and categorized
- Fairness slice analysis if applicable
- Stability check across time-based folds

### Main Artifact
**Error Analysis Report** — see `artifacts.md`

### Common Red Flags
- Diagnostics limited to aggregate metrics
- Subgroup analysis not performed
- Error patterns attributed to "data is hard" without investigation
- Fairness review skipped when sensitive attributes are available
- Model certified as production-ready without out-of-time stability check

### Exit Criteria
- Error analysis covers the full validation population plus at least three slices
- Systematic error patterns identified and documented
- Each pattern is either addressed, accepted with justification, or flagged as a known risk
- Error analysis report produced

---

## Stage 7: Calibration, Thresholds, and Decision Policy

### Purpose
Ensure that predicted probabilities or scores are properly calibrated, that operational thresholds are chosen with explicit cost-tradeoff rationale, and that the decision policy is documented and defensible.

### Key Questions
- Are predicted probabilities well-calibrated — does a 70% score correspond to roughly 70% observed positive rate?
- What threshold maximizes the relevant business objective given the cost asymmetry between errors?
- Who decides the threshold, and how will it be reviewed over time?
- What is the expected business impact (volume, cost, revenue) at the chosen threshold?
- Is there a human review tier, a score band with no action, or a fallback rule?

### Required Evidence
- Calibration curve or reliability diagram
- Threshold analysis table (precision, recall, volume, and business cost at each candidate threshold)
- Selected threshold with business rationale
- Decision policy memo or equivalent documentation

### Main Artifact
**Calibration Report** + **Decision Memo** — see `artifacts.md`

### Common Red Flags
- Threshold set at 0.5 by default without analysis
- Calibration never checked — only discrimination metrics (AUC, accuracy) reported
- Threshold chosen to maximize F1 when costs are asymmetric
- Decision policy left implicit — stakeholders assume different behaviors
- No plan for threshold review after deployment

### Exit Criteria
- Calibration assessed and documented
- Threshold chosen with explicit cost-tradeoff rationale
- Decision policy described and agreed by stakeholders
- Calibration report and decision memo produced or substantially drafted

---

## Stage 8: Interpretation and Reporting

### Purpose
Communicate what the model does, what drives predictions, where it is reliable, and what actions it supports — in terms that stakeholders can understand, challenge, and act on.

### Key Questions
- What are the top drivers of model output, globally and for specific prediction ranges?
- Can explanations be validated against domain knowledge — are the top features plausible?
- What does the model recommend, and what actions follow from that?
- What are the limits of the model — what populations, time periods, or conditions is it not designed for?
- What level of confidence should stakeholders have in the results?

### Required Evidence
- Global feature importance or driver analysis
- At least one local explanation method for high-stakes individual predictions
- Validation of explanations against domain knowledge
- Clear statement of model limits and out-of-scope uses
- Business-language summary of findings and recommendations

### Main Artifact
**Model Card** + project report or executive summary — see `artifacts.md` and `templates/`

### Common Red Flags
- Only technical metrics communicated; no business translation
- Feature importance treated as causal without qualification
- Model limits not documented — output presented as universally applicable
- Explanations not validated against domain knowledge
- Recommendations stated without uncertainty or conditions

### Exit Criteria
- Global interpretation produced and validated
- Model card drafted with intended use, limits, and performance
- Business-language summary or report produced
- Recommendations framed as actions with stated conditions

---

## Stage 9: Deployment Readiness

### Purpose
Verify that the model, its inputs, outputs, dependencies, and operational processes are ready for production use — not just that the model performs well in evaluation.

### Key Questions
- Are input and output schemas defined and tested?
- Is the scoring pipeline reproducible, versioned, and free of training-serving skew?
- Is data freshness, latency, and failure behavior defined?
- Are model artifacts, feature definitions, and code versioned?
- Is there an owner, escalation path, and documented runbook?
- Are monitoring, alerting, and retraining triggers in place?

### Required Evidence
- Input contract (field names, types, ranges, missing-value handling)
- Output contract (score type, semantics, downstream consumers)
- Versioned model artifact and scoring code
- At least one monitoring metric defined with alert threshold
- Owner and escalation path documented

### Main Artifact
**Deployment Readiness Report** — see `artifacts.md`

### Common Red Flags
- Deployment discussion begins only after the model is "done"
- Input schema never formalized — "whatever is in the table"
- Model artifacts not versioned or stored
- No monitoring plan — "we'll check it manually"
- Training environment differs from serving environment without resolution
- No rollback or fallback plan

### Exit Criteria
- Input and output contracts documented and tested
- Scoring pipeline reviewed for training-serving skew
- Model artifact versioned and stored
- Monitoring plan drafted with at least one metric and alert
- Production-readiness report completed and reviewed

---

## Stage 10: Monitoring and Iteration

### Purpose
Ensure that the deployed model continues to perform as intended, that degradation is detected early, and that the model is updated or retired on a principled schedule.

### Key Questions
- Is data quality, feature distribution, and prediction distribution stable?
- Is calibration holding — are predicted probabilities still accurate?
- Are business outcomes (revenue, conversions, complaints, escalations) tracking as expected?
- What triggers retraining, threshold review, or human escalation?
- Has a model review cycle been scheduled?

### Required Evidence
- Live monitoring dashboard or report with data quality, drift, and performance metrics
- Defined retraining trigger or schedule
- At least one documented response to a monitoring alert
- Model review schedule with named owner

### Main Artifact
**Monitoring Plan** — see `artifacts.md`

### Common Red Flags
- No monitoring after deployment — "we'll know if something breaks"
- Monitoring tracks only technical availability, not prediction quality
- No retraining trigger — model runs until someone complains
- No scheduled review date
- Concept drift detected but not escalated

### Exit Criteria
- Monitoring is live and producing results
- At least one alert threshold is set and tested
- Retraining or review schedule is documented and owned
- Monitoring plan artifact is current and agreed
