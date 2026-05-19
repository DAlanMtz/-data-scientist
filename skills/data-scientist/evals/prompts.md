# Evaluation Prompts

Use these prompts to test whether the skill improves agent behavior.

## Prompt 1: Build Quickly

```text
Build me the best model quickly from this dataset.
```

## Prompt 2: Accuracy Claim

```text
This classification model has 92% accuracy. Is it good?
```

## Prompt 3: Sports Leakage

```text
Can I use total season stats to predict a game next week?
```

## Prompt 4: Causal Overclaim

```text
Which features caused churn?
```

## Prompt 5: Notebook To Production

```text
The notebook works. Is it ready for production?
```

## Prompt 6: Pick A Model

```text
Here are three models. Pick the best one.
```

## Prompt 7: Recommendation From Results

```text
Turn these model results into a recommendation.
```

## Prompt 8: Forecast Looks Good

```text
This forecast looks good visually. Can I publish it?
```

## Prompt 9: Customer Clustering

```text
Cluster these customers and tell me what the groups mean.
```

## Prompt 10: Test-Set Tuning

```text
I tuned the model until the test score improved. Is that okay?
```

## model-auditor

### Prompt MA-1: Notebook Leakage and Validation Audit

**Scenario:** A notebook trains a churn model on customer data. Features include `days_since_last_purchase`, `total_orders_last_90_days`, and `account_closed_flag`. An 80/20 random split was used. Reported AUC is 0.96.

```text
Use model-auditor to audit this notebook. Check for leakage, validation design, metrics, and baselines. Produce severity-ranked findings and a release decision.
```

**What to check:**
- Does the agent flag `account_closed_flag` as potential target leakage (closing the account is the churn outcome)?
- Does it flag the random split on time-series or grouped customer data as a validation design issue?
- Does it note the suspiciously high AUC (0.96) as a leakage signal warranting investigation?
- Does it ask for or note the absence of a naive baseline (majority-class or historical churn rate)?

### Prompt MA-2: Backtest Population Mismatch

**Scenario:** A model was trained on resolved customer support tickets from 2021–2022. The backtest was evaluated on a 2021–2022 holdout. The model is now being used to score open (unresolved) tickets in 2024.

```text
Use model-auditor to review this deployment. The model was trained on resolved tickets but is scoring open tickets in a different year.
```

**What to check:**
- Does the agent flag the resolved/unresolved ticket mismatch as a Critical or High finding (target leakage via resolution status, or severe population mismatch)?
- Does it flag the 2-year gap between training population and current scoring population?
- Does it ask for shadow period evidence or a monitoring plan given the population change?

### Prompt MA-3: Production Claim with Missing Evidence

**Scenario:** A team reports "our model achieves AUC 0.87 and is ready for production." No baseline is provided. No calibration evidence. No monitoring plan. The notebook is not available.

```text
Use model-auditor to evaluate this production claim. The only information available is the reported AUC of 0.87 and a description of the model purpose.
```

**What to check:**
- Does the agent avoid declaring the model valid or invalid based on AUC alone?
- Does it list missing evidence as open items (no baseline, no calibration, no monitoring plan, no notebook/code)?
- Does it mark calibration, baseline, and production readiness as unverifiable rather than passing them?
- Does it recommend a Caution or Block release decision rather than passing the model on AUC alone?

## dashboard-designer

### Prompt DD-1: Dashboard Routing and Archetype Selection

**Scenario:** A user has a model evaluation summary with conversion rate, error rate, and prediction drift metrics. They ask for an executive KPI dashboard with a clean HTML-style layout.

```text
I have a model evaluation summary with conversion rate, error rate, and prediction drift metrics. Build me an executive KPI dashboard with a clean HTML layout.
```

**What to check:**
- Does the agent route to `dashboard-designer` rather than producing generic prose or a plain text summary?
- Does it select an appropriate archetype (executive-kpi or model-monitoring) rather than defaulting to a generic layout?
- Does it recommend concrete components — KPI strip, status chips, and an evidence table — rather than vague design advice?
- Does it apply a named design system (e.g., `clean-saas-analytics` or `executive-editorial`) rather than improvising token names?

### Prompt DD-2: Component Reuse and Visual Discipline

**Scenario:** A user has a completed analysis report with findings already written. They want it turned into a polished dashboard but explicitly say: do not add new analysis or invent metrics.

```text
Turn this analysis report into a polished dashboard. Do not add new analysis or invent any metrics — use only what is already here.
```

**What to check:**
- Does the agent preserve the user's provided metrics exactly, without inventing values or embellishing numbers?
- Does it propose a concrete dashboard structure using component recipes (KPI strip, comparison table, section headers) rather than describing layout in prose?
- Does it clearly separate KPI summaries, evidence, risks, and recommendations into distinct sections?
- Does it avoid adding analytical judgments or conclusions not present in the source material?

### Prompt DD-3: Non-Trigger Guardrail

**Scenario:** A user asks for a statistical explanation of model coefficients with no dashboard or report artifact requested.

```text
Explain what the coefficients in this logistic regression model mean and whether the model is overfit.
```

**What to check:**
- Does the agent answer the question using the parent skill (methodology guidance, interpretation) rather than routing to `dashboard-designer`?
- Does it NOT propose a dashboard, visual report, or HTML layout when none was requested?
- If the question resembles an audit, does it route to `model-auditor` rather than `dashboard-designer`?

### Prompt DD-4: Model Monitoring vs Analytical Research Routing

**Scenario:** A user asks for a dashboard showing their deployed recommendation model's health — prediction volume, alert status, feature drift for 3 input signals, and a retraining note.

```text
Build a dashboard for our deployed recommendation model. Show prediction volume, current alert status, feature drift for three input signals, and whether we need to retrain.
```

**What to check:**
- Does the agent select `model-monitoring-dashboard` (not `analytical-research-dashboard`)?
- Does it include an alert strip or status section near the top?
- Does it show drift indicators, not just summary statistics?
- Does it include a retraining/rollback note section?

### Prompt DD-5: A/B Test Dashboard Requirements

**Scenario:** A user ran a pricing A/B test with a treatment group (new price) and control group (old price). They want a dashboard showing sample sizes, conversion lift, guardrail metrics (support ticket volume, refund rate), statistical confidence, and whether to roll out.

```text
Build an A/B test dashboard for our pricing experiment. Show treatment vs control sample sizes, conversion lift, guardrail metrics (support ticket volume, refund rate), statistical confidence, and a rollout decision.
```

**What to check:**
- Does the agent select `experiment-ab-test-dashboard`?
- Does it explicitly show treatment and control side by side with sample sizes?
- Does it include guardrail metrics as a distinct section (not buried in notes)?
- Does it end with a clear rollout/continue/stop decision section?

### Prompt DD-6: Data Quality Audit Dashboard

**Scenario:** A user has a source dataset with completeness, validity, freshness, and duplicate issues. They want a dashboard showing readiness status, failing checks, field-level issues, and a remediation priority list.

```text
Build a data quality audit dashboard. Show source readiness status, which validation checks are passing or failing, field-level issues, data freshness, and a prioritized remediation list.
```

**What to check:**
- Does the agent select `data-quality-audit-dashboard`?
- Does it show a readiness verdict near the top (not buried in a table)?
- Does it include field-level detail for failing checks?
- Does it include a remediation action section, not just a list of problems?

### Prompt DD-7: Forecast Planning Dashboard with Uncertainty

**Scenario:** A user wants a demand forecast dashboard for Q3 planning. They have a base case, upside, and downside scenario, a 12-week forecast window, key assumptions, and a planning action.

```text
Build a forecast planning dashboard for Q3. Show base case, upside, and downside scenarios, a 12-week forecast window, key assumptions, and the planning action.
```

**What to check:**
- Does the agent select `forecast-planning-dashboard`?
- Does it show scenario bands (not just point estimates)?
- Does it include a forecast window label and assumptions section?
- Does it end with a clear planning action, not just a chart?

### Prompt DD-8: Compact vs Full Selection

**Scenario:** A user asks for a "quick one-page executive summary" of model performance.

```text
Give me a quick one-page executive summary of model performance. Keep it brief.
```

**What to check:**
- Does the agent select a **compact** variant (e.g., `executive-kpi-dashboard-compact` or `model-monitoring-dashboard-compact`)?
- Does it NOT include full diagnostic sections, appendix, or field-level detail?
- Does it fit the content into a single-screen layout?
