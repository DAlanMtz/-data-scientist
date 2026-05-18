# Dashboard Self-Critique Checklist

Use this checklist before sharing any stakeholder dashboard or visual report. Score each dimension on a 1–5 scale using the rubric below.

---

## Scoring Rules

- Score each dimension 1–5 using the rubric anchors.
- **Any dimension scoring below 4 requires a fix before delivery.**
- **Analytical Integrity below 4 is a blocking issue — do not share the dashboard or report until it is resolved.**
- Decision Clarity cannot score above 3 if the decision the dashboard supports cannot be stated.

**Delivery decision:**

| Score | Action |
|---|---|
| All dimensions ≥ 4 | Approved — deliver |
| Any dimension 3 | Fix required before delivery |
| Analytical Integrity ≤ 3 | Blocking — do not deliver |
| Decision Clarity and decision cannot be stated | Score ≤ 3, fix required |

---

## Dimension 1: Decision Clarity

**Can a first-time reader identify the decision, the answer, and the next action within 10 seconds?**

### Scoring Guide

| Score | Description |
|---|---|
| **5** | Decision is stated in the title or first screen. Answer is explicit. Next action has a named owner and timing. |
| **4** | Decision is clear. Answer requires minimal interpretation. Next action is strongly implied. |
| **3** | Decision can be inferred. Answer is buried or requires reading multiple sections. Cannot score above 3 if decision cannot be stated. **Fix required.** |
| **2** | Multiple conflicting readings of what the dashboard supports. Audience would ask "what am I supposed to do with this?" |
| **1** | No discernible decision. No implied action. Chart collection with no operating purpose. |

### Questions

- Can you write the supported decision in one sentence?
- Does the title or first screen state it?
- Is the recommended action or threshold visible without reading past the first view?
- Does a first-time reader know what to do after viewing?

### Pass Criteria (score ≥ 4)

- Decision is unambiguous from the first screen.
- Primary finding is visible without scrolling.
- Action or threshold is explicit or strongly implied.

### Red Flags

- No title or a title that names the chart type instead of the decision.
- Finding buried on page 3 or below the fold.
- "This dashboard shows metrics" is the implicit purpose.
- Decision requires reading a separate document.

### Fixes

- Add a decision statement to the dashboard title or header: "Weekly Revenue Health — [Status]."
- Add an executive summary block at the top: 2–3 sentences, current status, recommended action.
- Reorder visuals so the primary decision visual is first.

---

## Dimension 2: Visual Hierarchy

**Is the most important information visually dominant? Is there one clear focal point per view?**

### Scoring Guide

| Score | Description |
|---|---|
| **5** | One dominant element per section. KPI strip leads with clear primary. Supporting detail is visually quieter. Reading path is obvious. |
| **4** | Clear hierarchy. Main finding is findable without scanning. Minor inconsistencies in secondary elements are acceptable. |
| **3** | Hierarchy is present but uneven. Some sections compete for attention. Reader must scan to find the main point. **Fix required.** |
| **2** | Everything is the same visual weight. No focal point. Reader does not know where to look. |
| **1** | No hierarchy. Chart dump. Every element competing equally for attention. |

### Questions

- Is there one dominant element per view?
- Do KPI cards lead before charts?
- Are secondary metrics visually quieter than primary metrics?
- Is the reading path obvious without instructions?

### Pass Criteria (score ≥ 4)

- Primary metric or chart is visually largest or most prominent.
- Supporting detail is at a smaller scale or lower contrast.
- No more than one "loud" visual element per view.

### Red Flags

- Six charts in the same size grid with no clear primary.
- KPI cards and charts the same visual weight.
- Decorative colors drawing attention away from the decision visual.
- Header and body text the same size.

### Fixes

- Increase primary KPI card size or font size.
- Reduce visual weight of supporting metrics (smaller font, muted color).
- Apply a consistent size grid: primary > secondary > diagnostic.
- Remove visuals that add no decision value.

---

## Dimension 3: Analytical Integrity

**Are metrics defined, denominators correct, leakage absent, uncertainty visible, and causal claims avoided?**

> **This dimension is blocking. Scores below 4 mean the dashboard must not be delivered.**

### Scoring Guide

| Score | Description |
|---|---|
| **5** | Every metric has a definition, denominator, time window, and freshness indicator. Uncertainty is shown where it affects decisions. No causal overclaiming. |
| **4** | Metrics defined. Denominators present. Time windows consistent. No obvious integrity gaps. Minor documentation gaps are acceptable. |
| **3** | One or more primary metrics lack a definition or denominator. Uncertainty is absent where it materially affects the decision. **Blocking — do not deliver.** |
| **2** | Multiple metric gaps. Potential leakage or causal overclaiming present. Results are unverifiable from source data. **Blocking.** |
| **1** | Metrics undefined. No validation evident. Findings cannot be reproduced or trusted. **Blocking.** |

### Questions

- Can every primary KPI be reproduced from source data?
- Are denominators explicit? (Rate metrics: what is the denominator? Count metrics: what is included/excluded?)
- Are date windows consistent across related visuals?
- Is data freshness visible?
- Are incomplete current periods labeled or excluded?
- Is uncertainty shown where it changes the decision?
- Are causal claims avoided unless the study design supports causal inference?

### Pass Criteria (score ≥ 4)

- Every primary metric has a documented definition accessible from the dashboard.
- Denominators are explicit in metric labels or tooltips.
- Date windows are consistent across visuals on the same view.
- Freshness indicator is visible.
- No "increased X caused Y" language unless backed by a causal design.

### Red Flags

- Rates shown without denominators.
- "Conversion rate" without specifying which conversions and what denominator.
- Incomplete current period shown as a decline (e.g., current month with 3 days of data).
- Missing values silently dropped from denominators.
- "A led to B" language when only correlation exists.
- No freshness indicator.

### Fixes

- Add metric definitions to tooltips, footnotes, or a linked glossary.
- Label incomplete current periods: "Current month — partial data."
- Add freshness indicator to the dashboard header: "Data as of [timestamp]."
- Replace causal language with correlation language: "is associated with" instead of "caused."
- Confirm denominators by reconciling to source query.

---

## Dimension 4: Design Craft

**Are design system tokens applied consistently? Are chart defaults replaced? Are captions takeaways, not labels?**

### Scoring Guide

| Score | Description |
|---|---|
| **5** | Consistent design system applied throughout. No matplotlib defaults (tab10 colors, DejaVu Sans, box spines). Every chart title or caption states a finding, not a label. |
| **4** | Design system applied. Minor inconsistencies in secondary elements are acceptable. Most captions are takeaway-first. |
| **3** | Default chart styles present (tab10 colors, DejaVu Sans, box spines, or BI tool defaults). Captions describe chart content rather than interpreting findings. **Fix required.** |
| **2** | No design system applied. Significant visual inconsistency across charts. Raw defaults throughout. |
| **1** | Raw tool defaults. No color consistency. No typographic hierarchy. AI-generated-looking output. |

### Questions

- Are matplotlib/ggplot defaults replaced? (font, spines, color palette, grid)
- Are colors consistent across all charts using the same metric?
- Do chart titles state a finding ("Revenue declined 8% in Q3") rather than a label ("Revenue by Quarter")?
- Are chart backgrounds and text sizes consistent across the deliverable?
- Are axis labels descriptive and include units?

### Pass Criteria (score ≥ 4)

- All charts use the selected design system's `categorical_palette`, font, and grid style.
- No `tab10`/default matplotlib colors or `DejaVu Sans` font.
- Primary chart titles are takeaway-first.
- Axis labels include units.

### Red Flags

- Multiple charts using different color schemes.
- Charts with top/right spines still visible.
- All titles are label-style ("Metric by Dimension").
- Axis labels missing units ("Revenue" instead of "Revenue (USD M)").
- Inconsistent font sizes across the deliverable.

### Fixes

- Apply `HOUSE_RCPARAMS` + selected design system overrides to all charts.
- Rewrite chart titles: identify the finding, then write a sentence.
- Add units to axis labels.
- Remove box spines using `clean_axes()` helper from `references/chart-style-system.md`.

---

## Dimension 5: Usability

**Can a target-audience user operate the dashboard without reading documentation?**

### Scoring Guide

| Score | Description |
|---|---|
| **5** | Filter defaults match the most common workflow. All metric names are in business language. Active filters are visible. Actions are self-evident. Empty states are informative. |
| **4** | Usable with minimal orientation. Most labels are in plain language. One or two minor friction points are acceptable. |
| **3** | Requires explanation for filters, metric definitions, or available actions. Target audience would need a walkthrough. **Fix required.** |
| **2** | Multiple friction points. Likely to be misread or misused by the target audience without guidance. |
| **1** | Cannot be used without a guide. Filters unclear. Metric names are internal codes. Actions are not implied. |

### Questions

- Do filter defaults match the most common user workflow?
- Are active filters visible at all times?
- Are metric names in business language (not database column names)?
- Does the user understand what action to take after viewing?
- Are empty states informative ("No data for this filter" not a blank chart)?
- Is the reset filter behavior clear?

### Pass Criteria (score ≥ 4)

- Filters default to the most useful view.
- Metric names are audience-appropriate.
- A target-audience user can navigate and interpret without external help.

### Red Flags

- Filter defaults set to "All" when the audience always works within a specific time range.
- Metric names are database column names (`MTD_REV_USD` instead of "Revenue this month (USD)").
- Active filters are hidden.
- Blank charts with no explanation when the filter returns no data.
- Reset button absent or unclear.

### Fixes

- Change filter defaults to match the most common real-world use case.
- Rename metrics to business language.
- Add an active filter summary strip to the dashboard header.
- Add empty state messages to chart containers.

---

## Final Score Summary

| Dimension | Score (1–5) | Status | Fix required? |
|---|---|---|---|
| 1. Decision Clarity | | | |
| 2. Visual Hierarchy | | | |
| 3. Analytical Integrity | | **Blocking if < 4** | |
| 4. Design Craft | | | |
| 5. Usability | | | |

**Delivery decision:** Approve / Fix required / Blocking

---

## Related Files

- `workflow/design-preflight.md` — run before building; this checklist runs at Step 11
- `checklists/dashboard-qa-checklist.md` — publish-quality checklist for completed dashboards
- `design-systems/README.md` — choose a design system to address Design Craft gaps
- `references/design-craft-guide.md` — AI anti-patterns and craft principles for fixing Design Craft scores
- `references/chart-style-system.md` — paste-ready configurations to fix default chart styles
