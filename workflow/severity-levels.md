# Severity Levels

Severity levels classify audit findings — in data quality reviews, model audits, notebook reviews, leakage checks, and production-readiness assessments. Using severity levels makes findings actionable, prevents burying blockers in a list of suggestions, and gives stakeholders a clear sense of priority.

Apply severity levels whenever a finding is identified. Every finding should have a severity label before it is communicated.

---

## Critical

### Meaning
The finding invalidates the analysis or model result. Results cannot be used, trusted, or reported until this is resolved. This is not a risk to be noted — it is a stop condition.

### Examples
- Feature leakage: the model uses information that would not be available at prediction time
- Target leakage: the target field encodes the outcome itself or is causally downstream of a feature
- Training-test contamination: the same rows appear in both training and evaluation sets
- Evaluation performed only on training data and reported as test performance
- Random split applied to temporal data in a way that allows future-looking features
- Model artifact is untrained or uses a different dataset than described
- A joining error inflates row count and produces spurious correlations
- The target variable is defined using post-prediction events (look-ahead bias)

### Recommended Action
Stop the current work. Fix the issue before any results are communicated or used. If results have already been shared, issue a correction.

### Whether Work Should Stop
**Yes.** Do not proceed with modeling, reporting, or deployment until resolved.

### How to Phrase It in Reports
> **[CRITICAL]** This finding invalidates the current results. The model [or analysis] cannot be used until this is resolved. [Specific issue]. [Recommended fix].

---

## High

### Meaning
The finding materially degrades the reliability, generalizability, or fairness of the result. Results may still be directionally useful but cannot be reported as validated or used for high-stakes decisions without resolution.

### Examples
- Significant missingness in a key feature with no imputation policy
- Class imbalance not addressed when the minority class is the decision target
- Validation strategy does not match deployment conditions (e.g., random split on grouped data)
- No baseline established — no way to know if the model adds value
- Subgroup analysis reveals material performance degradation for a key segment
- Model is uncalibrated and the output is used as a probability
- Feature encoding applied before splitting — data leakage through preprocessing
- Evaluation metric does not reflect the business cost of errors

### Recommended Action
Resolve before advancing to the next lifecycle stage or before using results to make decisions. If resolution is not feasible immediately, document the limitation explicitly and restrict the use of results accordingly.

### Whether Work Should Stop
**Conditionally.** Work may continue within the current stage, but the finding must be resolved before passing the relevant quality gate.

### How to Phrase It in Reports
> **[HIGH]** This finding materially affects the reliability of results. [Specific issue]. This should be resolved before [advancing to the next stage / reporting results / using for decisions]. [Recommended fix].

---

## Medium

### Meaning
The finding reduces the robustness, clarity, or completeness of the work but does not invalidate results. Results can be used with appropriate caveats. Resolution improves quality but is not a gate condition.

### Examples
- Outliers not reviewed or treated — may affect regression performance
- Moderate missingness handled with list-wise deletion without documenting the impact
- Only aggregate metrics reported — no subgroup breakdown
- Feature importance not validated against domain knowledge
- Model card missing certain fields (limits, fairness summary)
- No variance reported across cross-validation folds
- Threshold selected at 0.5 without analysis, but this is a lower-stakes use case
- Code is not reproducible but results can be reconstructed

### Recommended Action
Address in the current or next stage. Document if deferring. Include as a known limitation in reports or the model card.

### Whether Work Should Stop
**No.** Work may continue. The finding should be logged and tracked.

### How to Phrase It in Reports
> **[MEDIUM]** This finding reduces robustness or completeness. [Specific issue]. Recommended to address before [deployment / final reporting / next review]. [Recommended fix].

---

## Low

### Meaning
The finding represents a quality or clarity improvement that would strengthen the work but has minimal impact on conclusions or decisions. Useful to track but not a priority.

### Examples
- Variable names are unclear or inconsistent
- A chart is missing axis labels or units
- A comment in code describes the wrong function
- A metric is reported with more decimal places than is meaningful
- A section of the report could be more concisely written
- A feature is included in the model but contributes negligibly and could be removed for simplicity
- Documentation does not note a dependency version

### Recommended Action
Address if time permits. Log as a polish item. Do not let these findings delay gate passage or delivery.

### Whether Work Should Stop
**No.**

### How to Phrase It in Reports
> **[LOW]** Minor quality or clarity improvement available. [Specific issue]. [Optional recommended fix].

---

## Informational

### Meaning
An observation worth noting for context, learning, or future reference. Not a finding that requires action. Provides transparency about choices made, tradeoffs accepted, or patterns observed.

### Examples
- A model family was considered and deprioritized — noting the rationale
- A data source was available but excluded for a documented reason
- A feature showed an unexpected pattern that was investigated and found to be legitimate
- A preprocessing choice was made that is conventional but not unique
- Performance is comparable to industry benchmarks — noting this for context
- A visualization is included for completeness even though it does not change the conclusion

### Recommended Action
No action required. Include in reports where transparency is valuable.

### Whether Work Should Stop
**No.**

### How to Phrase It in Reports
> **[INFO]** Noted for context. [Observation]. [Optional implication or rationale].

---

## Severity Quick Reference

| Level | Blocks gate? | Work stops? | Report phrasing prefix |
|---|---|---|---|
| Critical | Yes | Yes | `[CRITICAL]` |
| High | Yes (conditionally) | Conditionally | `[HIGH]` |
| Medium | No | No | `[MEDIUM]` |
| Low | No | No | `[LOW]` |
| Informational | No | No | `[INFO]` |

---

## Applying Severity in Audits

When auditing a notebook, dataset, model, or pipeline:

1. List every finding.
2. Assign a severity to each.
3. Group by severity, highest first.
4. Address Critical and High findings before communicating results.
5. Include Medium findings in the artifact with resolution timeline.
6. Include Low and Informational findings at the end for completeness.

When in doubt between two severity levels, use the higher one and document the rationale. It is safer to flag a High finding that turns out to be Medium than to miss a Critical finding by classifying it as High.
