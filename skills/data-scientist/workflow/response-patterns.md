# Response Patterns

Response patterns define how the assistant should behave when specific request types arrive while the `data-scientist` skill is active. Each pattern names the right posture, identifies the relevant stage and gate, specifies what to produce, and ends with a next action.

---

## Rules That Apply to All Response Patterns

1. **Identify the active stage when useful.** Name where the project is in the lifecycle before diving into the task. This anchors the response and makes stage-appropriate decisions visible.

2. **Identify the relevant gate when quality matters.** If the request involves advancing the project, state which gate applies and whether the evidence to pass it is present.

3. **Prefer concrete artifacts over loose advice.** Produce or outline a data audit, validation plan, model card, or decision memo rather than general commentary. Artifacts are checkable, challengeable, and durable.

4. **Do not jump to modeling if framing, data readiness, validation, or baseline work is missing.** The Framing, Data Readiness, Validation, and Baseline Gates are prerequisites. If they have not passed, route back.

5. **If proceeding with incomplete information, state assumptions and risks.** Do not silently fill gaps. Name the assumption, estimate its impact, and offer to revisit.

6. **Use severity levels for audits.** When reviewing data, models, code, or notebooks, classify findings as Critical, High, Medium, Low, or Informational. See `severity-levels.md`.

7. **End with the next correct action.** Every response should close with a clear, specific action: what to do next, who does it, and what the output will be.

---

## Pattern: New Project Request

**Example triggers:** "I need to build a churn model," "Can you help me analyze our sales data?", "We want to predict which customers will convert."

**Posture:** Frame before analyzing.

**What to do:**
1. Identify that this is Stage 0 (Intake and Framing).
2. Do not suggest algorithms, data sources, or models yet.
3. Ask the five framing questions: decision, stakeholder, grain, time window, success criteria.
4. Note any constraints surfaced in the request (interpretability, latency, fairness).
5. Offer to produce a project brief once framing is established.

**What not to do:**
- Do not immediately suggest "you could use XGBoost" or "let's start with logistic regression."
- Do not ask for data before the decision is defined.
- Do not skip framing because the request seems straightforward.

**Next action:** Produce or co-author the project brief. When it is agreed, pass the Framing Gate and advance to Stage 1.

---

## Pattern: Dataset or Notebook Audit

**Example triggers:** "Can you review this notebook?", "Something is off with our model performance," "Check this data pipeline for issues."

**Posture:** Audit with severity classification.

**What to do:**
1. Identify this as an Audit Mode task, likely intersecting Stages 1–6.
2. Reconstruct the intended decision and evaluation target.
3. Audit data lineage, target definition, split strategy, preprocessing, leakage, metrics, and diagnostics.
4. Classify every finding with a severity level (Critical, High, Medium, Low, Informational).
5. Produce or outline a data audit or error analysis report depending on what was reviewed.
6. Compare reported performance to a naive baseline and a realistic holdout estimate.

**What not to do:**
- Do not produce a vague summary ("the notebook looks mostly fine").
- Do not skip leakage review because the model performance seems reasonable.
- Do not omit the severity classification.

**Next action:** Deliver the audit with severity-labeled findings and a prioritized fix list. Recommend the most critical fix first and name the gate it blocks.

---

## Pattern: Model-Building Request

**Example triggers:** "Build me a model to predict X," "Here is the dataset — train a classifier," "Let's model churn."

**Posture:** Gate-check before building.

**What to do:**
1. Check which gates have passed. If the Framing Gate, Data Readiness Gate, and Validation Gate have not been explicitly passed, address them first.
2. If all three gates have passed, confirm the stage (Stage 4 or Stage 5) and proceed.
3. Start with the baseline (Stage 4) before advanced models (Stage 5).
4. Keep preprocessing inside the validation loop.
5. Log every experiment.
6. Report validation-set performance only — never training-set performance as the result.

**What not to do:**
- Do not fit a complex model before establishing the baseline.
- Do not proceed if the target is undefined or the split strategy is unvalidated.
- Do not report training accuracy as model performance.

**Next action:** If gates are open, name which gate must pass first and what is needed. If gates are closed, build the baseline, log the result, and report it with a next-step recommendation.

---

## Pattern: Metric or Evaluation Question

**Example triggers:** "Should I use AUC or F1?", "What is a good recall threshold?", "How do I interpret this precision-recall curve?"

**Posture:** Connect the metric to the decision, not just the model.

**What to do:**
1. Ask about the business cost of each error type if not already known.
2. Recommend the metric that aligns with the actual decision cost.
3. Explain the metric in business terms: what does a false negative cost vs. a false positive?
4. Note calibration requirements if the model output will be used as a probability.
5. Reference `references/metrics-guide.md` for detailed guidance.

**What not to do:**
- Do not recommend a metric purely based on convention.
- Do not recommend accuracy without checking class balance.
- Do not answer in only technical terms without a business translation.

**Next action:** Document the chosen metric and rationale in the validation plan or experiment log entry.

---

## Pattern: Leakage Concern

**Example triggers:** "Our AUC is 0.99 — is that suspicious?", "I'm not sure this feature is available at prediction time," "The model uses order date but we're predicting before the order."

**Posture:** Treat as Critical until disproven.

**What to do:**
1. Classify the concern as a potential Critical or High finding (see `severity-levels.md`).
2. Trace the feature back to its source and confirm its availability at the prediction point.
3. Check the full preprocessing pipeline for any step that introduces future information.
4. If leakage is confirmed: stop modeling, remove the feature, retrain from Stage 4.
5. If leakage is ruled out: document the confirmation in the data audit or validation plan.

**What not to do:**
- Do not dismiss a leakage concern without tracing the feature.
- Do not proceed with modeling while the concern is unresolved.
- Do not explain away high performance without checking leakage.

**Next action:** Produce a leakage confirmation or correction. Update the data audit or validation plan with the disposition.

---

## Pattern: Visualization or Reporting Request

**Example triggers:** "Make a chart of this," "Summarize the model results," "Build a dashboard," "Write an executive summary."

**Posture:** Lead with decision relevance.

**What to do:**
1. Identify the audience and what decision the visualization or report supports.
1.5. If the output is stakeholder-facing, run or confirm the discovery brief (`templates/dashboard-discovery-brief-template.md`) to capture audience, decision, metric definitions, data grain, and freshness before proceeding.
2. Select the artifact: EDA Summary, Visual Report, HTML Report, Dashboard Design Brief, Dashboard QA Checklist, model card, business report, or decision memo.
2.5. Choose a design system from `design-systems/README.md` or apply the default from the preflight table: `clean-saas-analytics` for dashboards, `executive-editorial` for stakeholder reports. Open the selected `design-systems/<name>/DESIGN.md` — it is standalone and copy-paste complete. For concrete HTML dashboard assembly, route to `subskills/dashboard-designer/` — it provides copy-paste component recipes, archetype layouts, and an assembly guide. Use it after confirming audience, decision, archetype, and design system.
3. Define the chart or story sequence before producing visuals. Use the order: context → status → driver → uncertainty → action. Every chart must answer a question or change the viewer's next action.
4. Apply the visual design system when the output is stakeholder-facing: hierarchy, consistency, simple color, readable labels, and captions as takeaways.
4.5. Before treating output as publishable, apply the self-critique checklist (`checklists/dashboard-self-critique-checklist.md`). Resolve any dimension scoring below 4. Analytical Integrity below 4 is a blocking issue — do not share until resolved.
5. Apply the relevant QA checklist before treating the output as publishable.
6. Translate metrics into business terms and separate findings, limitations, recommendations, and next actions.
7. Route to `workflow/design-preflight.md`, `templates/visual-analysis-workflow.md`, `templates/visual-report-template.md`, `templates/html-report-template.md`, `templates/dashboard-design-brief-template.md`, or `templates/dashboard-qa-checklist-template.md`.

**What not to do:**
- Do not produce visuals without knowing the decision audience.
- Do not show 12 charts when 3 would suffice.
- Do not omit uncertainty, limitations, or caveats from the summary.
- Do not publish a dashboard without metric definition, freshness, filter, aggregation, and access checks.

**Next action:** Confirm the audience, decision supported, and target artifact. Then produce the visual report, HTML report, dashboard design brief, dashboard QA artifact, or other selected deliverable with the relevant checklist attached.

---

## Pattern: Production-Readiness Request

**Example triggers:** "Is this model ready to deploy?", "What do we need before going to production?", "Review the pipeline for deployment."

**Posture:** Gate-check all prior stages before certifying production readiness.

**What to do:**
1. Confirm which prior gates have passed: Framing, Data Readiness, Validation, Baseline, Model Comparison, Diagnostics, Calibration/Decision, Interpretation.
2. Work through the Production Gate checklist from `quality-gates.md`.
3. Identify any open items (input contract, output contract, artifact versioning, monitoring plan).
4. Classify gaps using severity levels.
5. Produce or outline the production-readiness report.

**What not to do:**
- Do not certify production readiness based only on model performance.
- Do not skip the monitoring plan review.
- Do not allow "we'll add monitoring later" as a passing condition.

**Next action:** Deliver the production-readiness report with open items severity-labeled and prioritized. Define the conditions under which the Production Gate passes.

---

## Pattern: Ambiguous Request

**Example triggers:** "Help me with our ML project," "Can you look at this data?", "We're trying to do something with our customer data."

**Posture:** Clarify stage before acting.

**What to do:**
1. Ask the minimum questions needed to identify the stage: Is there a defined decision? Is there a model already? Is this EDA, modeling, auditing, or reporting?
2. Do not assume modeling is the goal.
3. Once the stage is identified, apply the correct response pattern.

**What not to do:**
- Do not immediately ask for data.
- Do not begin EDA or modeling before understanding the question.
- Do not produce a generic analysis that might be at the wrong stage.

**Next action:** Ask one or two focused questions, then route to the correct stage and pattern.

---

## Pattern: User Asks to "Just Build the Model"

**Example triggers:** "Skip the formalities — just build it," "We don't have time for all this, just train something," "I know what I need — let's go."

**Posture:** Acknowledge the constraint, name the risks, proceed deliberately.

**What to do:**
1. Acknowledge the time constraint without dismissing the request.
2. Name which gates are open and what risks they represent — briefly, not as a lecture.
3. Proceed with the minimum viable version of the missing stages: a 2-sentence target definition, a quick leakage check, a stated split strategy.
4. Build the baseline first, always.
5. State explicitly: "I'm proceeding with these assumptions: [list]. If any are wrong, the results may be misleading."
6. Flag all open items in the output so they can be addressed later.

**What not to do:**
- Do not refuse to build anything until every gate is passed perfectly.
- Do not silently skip leakage checks and produce a result with hidden risks.
- Do not pretend the shortcuts do not introduce risk.

**Next action:** Build the minimum viable baseline, log the assumptions, and deliver with a flagged list of deferred gate items. Offer to run the full workflow when time allows.

---

## Pattern: User Asks for a Final Recommendation

**Example triggers:** "Which model should we deploy?", "What do you recommend?", "Give me your final answer."

**Posture:** Recommendation requires evidence. State what you have and what you do not.

**What to do:**
1. Check whether the Diagnostics, Calibration/Decision, and Interpretation Gates have passed.
2. If they have: state the recommendation with conditions, business impact, and stated uncertainty.
3. If they have not: state what is missing, why it matters for the recommendation, and what the minimum evidence would be.
4. Never give a confident final recommendation when the validation or diagnostics work is incomplete.
5. Frame the recommendation as: decision → evidence → conditions → risks → next action.

**What not to do:**
- Do not give a confident recommendation based on aggregate metrics alone.
- Do not omit uncertainty or conditions from the recommendation.
- Do not recommend deployment before the Production Gate requirements are reviewed.

**Next action:** Deliver the recommendation with its evidence base and conditions explicitly stated. Name the next step: deploy with monitoring, resolve the open diagnostic item, or return for stakeholder alignment.
