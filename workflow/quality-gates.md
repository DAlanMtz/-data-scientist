# Quality Gates

Quality gates are explicit checkpoints between lifecycle stages. A gate defines what must be true before the project advances. Gates are not bureaucratic — they exist because the cost of fixing framing, leakage, or validation errors after modeling is orders of magnitude higher than fixing them before.

When a gate fails, the default action is to return to the prior stage and resolve the failure before advancing. Proceeding past an open gate while only noting the risk is not a pass — it is a deliberate exception that must be documented with explicit assumptions and use restrictions. See the fast-path pattern in `workflow/response-patterns.md` for how to handle constrained scenarios.

---

## Framing Gate

**Between Stage 0 and Stage 1**

### Pass Requirements
- Decision or question is documented in writing
- Named stakeholder or decision-maker identified
- Unit of analysis (grain) is defined
- Time window and population are defined
- Primary success metric is named with business rationale
- At least one constraint (interpretability, latency, fairness, regulatory) documented or explicitly noted as unconstrained

### Evidence Required
- Project brief (minimum version accepted)
- Stakeholder agreement (verbal or documented)

### Blocking Red Flags
- Problem stated only as a model type ("build a classifier")
- No decision or action tied to the output
- Scope is undefined or unbounded
- Success defined only in technical metric terms with no business translation
- Conflicting stakeholder goals not surfaced

### Recommended Artifact
**Project Brief** — see `artifacts.md`

### What to Do If the Gate Fails
Return to Stage 0. Ask the stakeholder: "What decision does this analysis support, who makes it, and what does a good outcome look like?" Do not profile data or suggest models until this gate passes.

---

## Data Readiness Gate

**Between Stage 1 and Stage 2**

### Pass Requirements
- All required data sources profiled at field level
- Grain of analysis confirmed with no unexpected fan-out
- Date ranges and coverage verified
- Missingness documented for all key fields
- Duplicate check completed
- Leakage candidates identified and dispositioned
- At least one data quality issue documented or "none found" confirmed
- Sufficiency statement produced: data is (or is not) sufficient for the defined scope

### Evidence Required
- Data audit artifact (minimum version accepted)
- Field-level profile tables
- Leakage candidate log

### Blocking Red Flags
- Data accepted without profiling
- Leakage candidates identified but not resolved before EDA
- Join keys have unexpected many-to-many structure
- Target field has implausible completeness or impossible values
- Date fields have gaps, future timestamps, or unresolved migrations

### Recommended Artifact
**Data Audit** — see `artifacts.md`

### What to Do If the Gate Fails
Return to Stage 1. Produce the missing profile, resolve the join key issue, or document the leakage disposition. If data is fundamentally insufficient, escalate to Stage 0 to revise the scope.

---

## Validation Gate

**Between Stage 3 and Stage 4**

### Pass Requirements
- Target definition is written and unambiguous (event, grain, outcome window, exclusions)
- Prediction point is defined and enforced in feature logic
- Every candidate feature confirmed as available at the prediction point
- Split strategy documented with rationale
- Baseline strategy agreed
- Primary and secondary evaluation metrics defined with business rationale
- No features allowed that depend on post-prediction-point information

### Evidence Required
- Validation plan artifact (minimum version accepted)
- Feature list with leakage confirmation for each field

### Blocking Red Flags
- Target definition remains informal
- No prediction point specified — features include any data in the table
- Random split applied to temporal or grouped data without justification
- Evaluation metrics chosen for familiarity rather than business cost alignment
- Baseline not defined

### Recommended Artifact
**Validation Plan** — see `artifacts.md`

### What to Do If the Gate Fails
Return to Stage 3. Writing the target definition and prediction point is not optional. Do not write modeling code until the gate passes. If the feature list cannot be confirmed, return to Stage 1 for additional data audit work. If proceeding under explicit time constraints, follow the fast-path pattern in `workflow/response-patterns.md`: produce a minimum viable target definition, document all assumptions, and flag every open gate item in the output.

---

## Baseline Gate

**Between Stage 4 and Stage 5**

### Pass Requirements
- At least one baseline model or rule trained and evaluated on the validation set
- Baseline metrics recorded in the experiment log
- Baseline implementation confirmed free of leakage
- Baseline evaluated on the holdout — not only on training data
- Calibration assessed if the output is a probability

### Evidence Required
- Experiment log — baseline entry
- Validation set performance metrics

### Blocking Red Flags
- Baseline skipped with no justification
- Baseline uses features not available at prediction time
- Baseline performance reported only on training data
- Preprocessing applied outside the validation fold

### Recommended Artifact
**Experiment Log** — baseline entry; see `artifacts.md`

### What to Do If the Gate Fails
Return to Stage 4. Implement the baseline defined in the validation plan. If the baseline reveals a problem with the feature pipeline or split, resolve it before advancing to complex models.

---

## Model Comparison Gate

**Between Stage 5 and Stage 6**

### Pass Requirements
- At least two candidate approaches evaluated (including the baseline)
- All evaluation performed on the pre-defined holdout
- Cross-validation or time-fold variance reported — not only point estimates
- Performance evaluated on at least one operational slice (segment, time period, geography)
- Preferred model selected with documented rationale including non-metric factors
- Model comparison report drafted

### Evidence Required
- Experiment log (full, all candidates)
- Model comparison report

### Blocking Red Flags
- Only one model evaluated
- Model selected on training-set performance
- No variance or interval reported
- Tuning performed before the split and metric were locked
- Interpretability or latency requirements ignored

### Recommended Artifact
**Model Comparison Report** — see `artifacts.md`

### What to Do If the Gate Fails
Return to Stage 5. Add a second candidate, evaluate on the holdout, and document the rationale for model selection.

---

## Diagnostics Gate

**Between Stage 6 and Stage 7**

### Pass Requirements
- Error distribution analyzed for the full validation population
- Performance sliced by at least three subgroups or dimensions
- Top error cases reviewed and categorized
- Fairness slice analysis completed (if sensitive attributes are available and applicable)
- Stability assessed across at least one out-of-time or out-of-distribution sample
- Systematic error patterns either addressed, accepted with justification, or flagged as known risk
- Error analysis report produced

### Evidence Required
- Error analysis report
- Subgroup performance breakdown
- Stability check results

### Blocking Red Flags
- Diagnostics limited to aggregate metrics
- Subgroup analysis skipped
- Fairness review skipped when sensitive attributes are available
- Systematic error patterns noted but not investigated
- No out-of-time stability check

### Recommended Artifact
**Error Analysis Report** — see `artifacts.md`

### What to Do If the Gate Fails
Return to Stage 6. Perform the missing subgroup analysis or stability check. If error patterns reveal a modeling problem, loop back to Stage 5.

---

## Calibration/Decision Gate

**Between Stage 7 and Stage 8**

### Pass Requirements
- Calibration curve or reliability diagram produced
- Calibration quality assessed (acceptable, requiring correction, or poor)
- If calibration correction applied, post-correction curve produced
- Threshold analysis table built with precision, recall, volume, and business cost at candidate thresholds
- Final threshold selected with documented cost-tradeoff rationale and stakeholder agreement
- Decision policy documented: score ranges, actions, human review tier, fallback rule
- Review trigger for threshold revision defined

### Evidence Required
- Calibration report
- Threshold analysis table
- Decision memo

### Blocking Red Flags
- Threshold set at 0.5 by default without analysis
- Calibration never checked — only discrimination metrics reported
- Threshold chosen to maximize F1 when costs are asymmetric
- Decision policy implicit or undocumented
- No threshold review trigger defined

### Recommended Artifact
**Calibration Report** + **Decision Memo** — see `artifacts.md`

### What to Do If the Gate Fails
Return to Stage 7. Produce the calibration assessment. Engage the stakeholder on error costs before selecting the threshold.

---

## Interpretation Gate

**Between Stage 8 and Stage 9**

### Pass Requirements
- Global feature importance or driver analysis produced and validated against domain knowledge
- Model card drafted (intended use, performance, limits, fairness summary)
- Business-language summary or executive report produced
- Recommendations framed as actions with conditions and stated uncertainty
- Model limits explicitly documented

### Evidence Required
- Model card
- Business report or executive summary
- Stakeholder sign-off (or equivalent review)

### Blocking Red Flags
- Only technical metrics communicated — no business translation
- Feature importance presented as causal without qualification
- Model limits omitted from the report
- Recommendations stated without uncertainty or conditions
- Model card not produced

### Recommended Artifact
**Model Card** + business report — see `artifacts.md` and `templates/`

### What to Do If the Gate Fails
Return to Stage 8. Produce the model card and business summary. Do not advance to production readiness without stakeholder understanding of what the model does, where it applies, and where it does not.

---

## Production Gate

**Between Stage 9 and Stage 10**

### Pass Requirements
- Input contract documented (field names, types, ranges, missing-value handling, freshness)
- Output contract documented (score semantics, threshold, downstream consumers)
- Scoring pipeline reviewed for training-serving skew
- Model artifact, feature definitions, and scoring code versioned and stored
- At least one monitoring metric defined with alert threshold
- Owner and escalation path documented
- Rollback or fallback plan documented
- Production-readiness report completed and reviewed

### Evidence Required
- Production-readiness report
- Input and output contract documentation
- Monitoring plan (minimum version)

### Blocking Red Flags
- Input or output schema not formalized
- Model artifact not versioned or stored
- Training environment differs from serving environment without resolution
- No monitoring plan
- No rollback or fallback plan
- No named owner

### Recommended Artifact
**Deployment Readiness Report** — see `artifacts.md`

### What to Do If the Gate Fails
Return to Stage 9. Do not deploy until input and output contracts are documented, the artifact is versioned, and a monitoring plan exists. Partial deployment (shadow mode, limited rollout) is acceptable if this gate passes for the shadow scope.

---

## Monitoring Gate

**Active from Stage 10 onward — reviewed on a defined cadence**

### Pass Requirements
- Monitoring is live and producing results on the agreed cadence
- At least one alert threshold is set and has been tested
- Data quality, drift, calibration, and business-outcome metrics are tracked
- Retraining trigger or review schedule is documented and owned
- At least one monitoring alert has been reviewed and responded to (at first review cycle)

### Evidence Required
- Monitoring dashboard or report
- Monitoring plan (current version)
- Alert response log (at first review)

### Blocking Red Flags
- No monitoring active after deployment
- Monitoring tracks only technical availability
- No retraining trigger defined
- No scheduled review date
- Concept drift detected but not escalated

### Recommended Artifact
**Monitoring Plan** — see `artifacts.md`

### What to Do If the Gate Fails
Return to Stage 10. Activate the minimum viable monitoring: data quality check, prediction distribution check, and business-outcome tracking. Define a review date. If the model has been running unmonitored, perform a retrospective audit before the next review cycle.
