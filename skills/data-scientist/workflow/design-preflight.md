# Design Preflight

Run this protocol before generating a stakeholder dashboard or visual report. It replaces guesswork with explicit decisions that make the deliverable correct and usable the first time.

---

## Proportionality Gate

Do not run the full preflight for every request. Choose the level that matches the work:

| Request type | Protocol |
|---|---|
| Single chart, internal or exploratory | Answer directly — no preflight required |
| Polished chart for a presentation or report | Apply chart style only (Steps 5 and 11) |
| Stakeholder dashboard or visual report | Full 11-step preflight |
| Dashboard already in progress, needs QA | Start at Step 10 (self-critique) |

**Key operating rule:** Do not ask every discovery question by default. If enough context exists, choose sensible defaults, state the assumptions, and proceed. If required information is missing, apply the closest default from the selection table below, state the assumption explicitly, and flag it for review.

---

## Default Design System Selection

| Situation | Default design system |
|---|---|
| Dashboard, no stated preference | `clean-saas-analytics` |
| Stakeholder / PDF-style visual report | `executive-editorial` |
| Monitoring / alerting dashboard | `operational-command-center` |
| Academic / research-heavy report | `research-paper` |
| Finance / risk / trading dashboard | `financial-terminal` |
| Narrative / explanatory nontechnical report | `warm-narrative` |

---

## 11-Step Protocol

### Step 1 — Identify audience and decision cadence

- Who will use this? (executive, analyst, operator, customer, technical reviewer)
- How often? (one-time, weekly, daily, real-time)
- What action does this support?

If the decision cannot be stated after Step 1, do not proceed to Step 2. Surface the gap and resolve it first.

### Step 2 — Identify the decision supported

Write one sentence: "This dashboard/report helps [audience] decide [decision]."

If this sentence cannot be completed, the deliverable is not ready to design. A chart collection without a supported decision is not a dashboard.

### Step 3 — Choose artifact type

Select one:

| Artifact | When |
|---|---|
| Dashboard | Recurring, interactive, filter-driven, operational |
| Visual report | One-time or periodic narrative, static, stakeholder-facing |
| HTML report | Polished PDF-ready static output |
| Notebook visual section | Embedded in an analysis notebook |
| Slide deck | Presentation to a live audience |

### Step 4 — Choose dashboard archetype

Route to `templates/dashboards/README.md` for the full mapping. Quick reference:

| Need | Template |
|---|---|
| General metric exploration | `analytics-dashboard-template.md` |
| Leadership status summary | `executive-kpi-dashboard-template.md` |
| ML model monitoring | `model-performance-dashboard-template.md` |
| Forecast and planning | `forecasting-dashboard-template.md` |
| Retention and cohort analysis | `cohort-retention-dashboard-template.md` |
| Alert and exception triage | `anomaly-monitoring-dashboard-template.md` |
| Static HTML prototype | `html-dashboard-starter-template.md` |

### Step 5 — Choose design system

Use the default-selection table above or confirm the user's stated preference.

Open `design-systems/<name>/DESIGN.md`. It is standalone and copy-paste complete — no other file is needed to apply the theme.

### Step 6 — Define KPI hierarchy

Order metrics by decision impact:

1. Primary KPIs — the 1–3 metrics that directly answer the decision question
2. Secondary metrics — supporting context and trend
3. Diagnostic metrics — data quality, pipeline health, anomaly indicators

Primary KPIs go on the first screen. Diagnostic metrics go last. Do not put more than 5 metrics in the KPI strip.

### Step 7 — Define chart sequence

Plan the visual story in this order: **context → status → driver → uncertainty → action**

- Context: what population, time window, and baseline? (Sets the frame)
- Status: what is the current state vs. target? (Answers the decision)
- Driver: why is it this way? Segment or factor decomposition.
- Uncertainty: what is missing, incomplete, or low-sample?
- Action: what does the audience do next?

Every chart must answer a question in this sequence. If a chart does not fit, remove it.

### Step 8 — Define filters, date range, and refresh cadence

- What is the default date range? (Match the decision cadence)
- What filters are required? (Segment, product, region, status)
- Do filters affect metric definitions? (If yes, document and label visibly)
- Refresh: real-time, hourly, daily, weekly, on-demand?
- Freshness indicator: where does it appear? What does it show?

### Step 9 — Confirm metric definitions, data grain, and freshness

Fill out the Metric/Data Contract block from `templates/dashboard-discovery-brief-template.md`:

- Metric definitions (one line per metric)
- Data grain (entity, row level)
- Refresh cadence
- Data freshness indicator
- Metric owner or source of truth
- Known caveats

Do not proceed to Step 10 without confirmed metric definitions. Undefined metrics at this stage become analytical integrity failures at delivery.

### Step 10 — Select output format

Route to `references/dashboard-output-formats.md` to confirm format-specific constraints.

| Output format | Key constraint |
|---|---|
| HTML dashboard | CSS token overrides, no external dependencies |
| PDF visual report | Print media query, static charts |
| Markdown spec | Prose + tables, no CSS |
| Notebook section | rcParams + markdown takeaway cells |
| Streamlit / Shiny | Map tokens to theme config |
| Excel / Sheets | Named styles, conditional formatting |
| BI tool | Tool theme + field descriptions |

### Step 11 — Apply self-critique before delivery

Run `checklists/dashboard-self-critique-checklist.md`.

Score each of the five dimensions (Decision Clarity, Visual Hierarchy, Analytical Integrity, Design Craft, Usability) on a 1–5 scale.

**Delivery rules:**
- Any dimension below 4 → fix before sharing.
- Analytical Integrity below 4 → **blocking issue** — do not share until resolved.
- Decision Clarity cannot score above 3 if the supported decision cannot be stated.

---

## Summary Card

```
1. Audience + decision cadence
2. Decision supported (one sentence — required)
3. Artifact type
4. Dashboard archetype
5. Design system
6. KPI hierarchy (primary / secondary / diagnostic)
7. Chart sequence (context → status → driver → uncertainty → action)
8. Filters + date range + refresh cadence
9. Metric definitions + data grain + freshness (data contract)
10. Output format
11. Self-critique (score ≥ 4 on all 5 dimensions; Analytical Integrity is blocking)
```
