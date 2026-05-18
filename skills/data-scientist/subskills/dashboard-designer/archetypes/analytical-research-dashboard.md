# Archetype: Analytical Research Dashboard

## Purpose

A structured, evidence-first dashboard layout for presenting analytical findings, model results, or research conclusions to a technically informed audience. The viewer is expected to evaluate evidence, not just read a summary — so the layout leads with the verdict but keeps the supporting evidence visible and organized.

Use this archetype when the dashboard communicates the output of an analysis, model evaluation, experiment, or multi-entity assessment.

## When to Use

- Analysis results across multiple entities (models, families, segments, cohorts, strategies)
- Research output shared with analysts, data scientists, or technical stakeholders
- Multi-family or multi-model status summaries with comparison and stability checks
- Baseline or benchmark assessment deliverables

## Design System Default

`clean-saas-analytics` — unless the audience or format calls for another. Override by loading the appropriate `../../design-systems/<name>/DESIGN.md` tokens.

---

## Section Composition

### 1. Page Header

```
H1: Dashboard name — descriptive, tells the viewer what this analysis covers
Metadata line: date · source · scope · denominator
Verdict band: top-level recommendation or analysis status (verdict-warning / verdict-success / verdict-danger)
```

**Component:** `components/verdict-band.md`

The verdict band is required in this archetype. Analytical research dashboards always have an overall assessment.

---

### 2. KPI Strip

5 cards following the recommended slot composition:

| Slot | Role | Example |
|---|---|---|
| 1 | Scale / volume | Total eligible rows, sample size, observation count |
| 2 | Primary outcome | Number of entities passing the target threshold |
| 3 | Readiness / status | Entities ready for next step (with semantic color) |
| 4 | Risk / exception | Entities needing review, flagged, or blocked |
| 5 | Data quality | Coverage, freshness, or completeness indicator |

**Component:** `components/kpi-strip.md`

---

### 3. Family / Entity Status Table

The primary evidence section. Shows the current assessment of each entity (model, family, segment, approach) with status chips, metric values, and warning flags.

**Section header (takeaway-first):**  
Example: "5 of 6 families have usable baselines — Points OVER needs enrichment before promotion"

**Component:** `components/status-chips.md` + table base + `components/section-header.md`

Table columns (adapt to context):
- Entity name
- Rule or selector
- Pool / row count
- Primary metric (color-coded with metric-color-cell)
- Retention %
- Out-of-time / holdout result
- Status chip
- Warning flags (chips)

**Limit to 10 rows in the primary view.** If there are more entities than this, put the full table in a secondary section or appendix.

---

### 4. Comparison / Benchmark Section

Shows how the primary approach compares to alternatives, baselines, or historical benchmarks. This is the "why the approach was chosen" section.

**Section header (takeaway-first):**  
Example: "Primary approach matches market-aware WR without using odds — basketball signal exists independently of pricing"

**Component:** `components/comparison-table.md`

Recommended column structure:
- Entity / group
- Raw / unadjusted baseline
- Primary approach: rows, metric, rule (highlighted)
- Benchmark A: rows, metric, rule
- Benchmark B: rows, metric (if applicable)

Keep to 3 approach columns maximum. Additional approaches go in an appendix table.

---

### 5. Stability / Segment Heatmap

Shows where the primary metric holds across time or segments, and where it breaks down. This is the uncertainty section — it answers "can we trust this?"

**Section header (takeaway-first):**  
Example: "April weakness is the dominant risk — all 6 entities carry a month instability flag"

**Components:** `components/stability-heatmap.md` + `components/filter-bar.md`

Heatmap structure:
- Rows: time periods (months, quarters) or segments
- Columns: entities (families, models, cohorts) — filtered by the filter bar
- Cells: metric value + row count
- Color coding: metric-strong / metric-ok / metric-marginal / metric-weak

Filter bar (if > 4 columns): group selector above the heatmap (e.g., All | Group A | Group B | Group C)

Footnote: threshold definitions; partial-month or small-sample caveat.

---

### 6. Recommended Actions / Next Steps

The action section closes the decision loop. States what the viewer should do based on the findings above.

**Section header (takeaway-first):**  
Example: "Two entities are ready for promotion — four require monitoring or enrichment before use"

Content:
- Recommended action per entity status class (ready → promote; monitor → observe; partial → enrich first)
- Specific next ticket or next step if known
- Who owns the decision

This section should be 1–2 short paragraphs or a 3-row action table. It is not a new data section — it synthesizes the sections above.

---

### 7. Appendix (Collapsible)

Move all diagnostic and verbose content here. Typical appendix sections for this archetype:

- Feature coverage table (with coverage bars and present/not-present chips)
- Signal diagnostics (mutual information, correlation by entity)
- Stability and concentration checks (player, line, price concentration by entity)
- Raw / unadjusted baseline table
- Methodology notes and exclusion rules
- Assumptions log

**Component:** `components/collapsible-appendix.md`

Each appendix section is a separate `<details>` element with a descriptive `<summary>` label.

---

## Layout Structure

```html
<div class="page">

  <!-- 1. Header -->
  <div class="page-header">
    <h1>[Dashboard Name]</h1>
    <div class="page-meta">[date · source · scope]</div>
    <div class="verdict-band verdict-warning" role="status">
      <span>⚠</span>
      <span class="verdict-label">[overall_status_code]</span>
    </div>
  </div>

  <!-- 2. KPI strip -->
  <section class="kpi-strip" aria-label="Key performance indicators">
    <!-- 5 kpi-card elements -->
  </section>

  <!-- 3. Entity status table -->
  <section class="section-card">
    <header class="section-header">
      <h2 class="section-title">[Finding: how many entities clear the threshold and why]</h2>
      <p class="section-meta">[population · method · date range]</p>
    </header>
    <div class="tbl-wrap">
      <table><!-- status table --></table>
    </div>
    <p class="footnote">[Metric definitions, OOT explanation]</p>
  </section>

  <!-- 4. Comparison / benchmark -->
  <section class="section-card">
    <header class="section-header">
      <h2 class="section-title">[Finding: what the comparison reveals about approach quality]</h2>
      <p class="section-meta">[approaches compared · metric · scope]</p>
    </header>
    <div class="tbl-wrap">
      <table class="compare-table"><!-- comparison table --></table>
    </div>
    <p class="compare-footnote">[Approach definitions and data difference caveats]</p>
  </section>

  <!-- 5. Stability heatmap -->
  <section class="section-card">
    <header class="section-header">
      <h2 class="section-title">[Finding: when and where does the metric break down]</h2>
      <p class="section-meta">[time range · groups · threshold rules]</p>
    </header>
    <div class="filter-bar" role="group" aria-label="Filter by group">
      <!-- filter buttons -->
    </div>
    <div class="hm-legend"><!-- legend --></div>
    <div class="heatmap-wrap">
      <table class="heatmap-table" id="heatmap"><!-- built by JS --></table>
    </div>
    <p class="footnote">[Threshold definitions; small-sample caveat]</p>
  </section>

  <!-- 6. Recommended actions -->
  <section class="section-card">
    <header class="section-header">
      <h2 class="section-title">[Finding: decision and recommended next actions]</h2>
      <p class="section-meta">[ownership · timing]</p>
    </header>
    <!-- action table or short prose -->
  </section>

  <!-- 7. Appendix -->
  <details class="appendix">
    <summary>Diagnostics — Feature Coverage</summary>
    <div class="appendix-body"><!-- ... --></div>
  </details>

  <details class="appendix">
    <summary>Diagnostics — Signal Associations</summary>
    <div class="appendix-body"><!-- ... --></div>
  </details>

  <details class="appendix">
    <summary>Reference — Raw Baseline</summary>
    <div class="appendix-body"><!-- ... --></div>
  </details>

</div>
```

---

## Self-Critique Checks for This Archetype

Before delivering:

- [ ] **Decision Clarity:** Can a viewer state the supported decision from the first screen?
- [ ] **Analytical Integrity:** Are all metric values in the status table defined in the metric contract? Are denominators visible? Are OOT / holdout rows labeled and explained?
- [ ] **Visual Hierarchy:** Is the verdict band above the KPI strip? Is the status table the first section? Is diagnostic content in the appendix?
- [ ] **Design Craft:** Are all status codes replaced with chips? Are all metric values color-coded? Are section titles findings, not labels?
- [ ] **Usability:** Do filter buttons update the heatmap? Is the heatmap scrollable on narrow screens? Are appendix sections collapsed by default?

## Related Components and Parent Files

- `components/verdict-band.md`
- `components/kpi-strip.md`
- `components/status-chips.md`
- `components/metric-color-cell.md`
- `components/comparison-table.md`
- `components/stability-heatmap.md`
- `components/filter-bar.md`
- `components/collapsible-appendix.md`
- `../../workflow/design-preflight.md`
- `../../checklists/dashboard-self-critique-checklist.md`
