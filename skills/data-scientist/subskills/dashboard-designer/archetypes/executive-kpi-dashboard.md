# Archetype: Executive KPI Dashboard

## Purpose

A concise, scannable dashboard layout optimized for leadership decisions. Every pixel serves the decision. The viewer is a time-constrained executive or business stakeholder who needs to know: what is the current state, is it good or bad, what changed, and what action (if any) is required. They do not need to verify methodology.

## When to Use

- Business performance summaries presented to leadership or non-technical stakeholders
- Weekly / monthly operational reviews with a single primary metric
- Go / no-go or approve / escalate decisions based on KPI status
- Dashboards that will be printed, exported to PDF, or presented on a screen during a meeting

## Design System Default

`executive-editorial` — structured, restrained, high contrast typography.  
Override to `clean-saas-analytics` for a digital-first, lighter variant.  
Do not use `operational-command-center` or `financial-terminal` for this archetype.

---

## Principles for This Archetype

- **One screen, one decision.** The answer to the decision must fit within one visible screen.
- **No jargon on the first screen.** Field names, model names, and technical codes belong in the appendix.
- **Status before trend.** Show the current state first; trend explains it.
- **Recommended action must be visible.** If the viewer needs to act, the action must be stated explicitly.
- **Minimal appendix.** This audience does not need diagnostics. The appendix may contain method notes only.

---

## Section Composition

### 1. Page Header

```
H1: A business question or outcome statement — not a project name
Metadata: as-of date and data source (one line)
Verdict band: overall status (success / warning / danger / neutral)
```

**Component:** `components/verdict-band.md`

The H1 should answer the question "what is this dashboard about?" in business terms.  
- Good: "Q2 Customer Retention — On Track or At Risk?"  
- Bad: "Retention_Model_v2_Dashboard_2026Q2"

---

### 2. KPI Strip (3–5 cards)

Lead with the single most important metric. Keep the strip narrow — 3–4 cards is often stronger than 5.

| Slot | Role | Example |
|---|---|---|
| 1 | Primary KPI — the decision metric | Retention rate, revenue, conversion, accuracy |
| 2 | Target / benchmark comparison | % vs. target, vs. prior period |
| 3 | Trend signal | Direction: up/down/flat with delta |
| 4 | Risk or exception count | Number of failing units, alerts open |
| 5 | (Optional) Leading indicator | Early signal for next period |

**Component:** `components/kpi-strip.md`

Use semantic colors decisively. A positive `kpi-positive` card must mean the decision outcome is favorable. Do not use positive green for a metric that is merely increasing if the target has not been met.

---

### 3. Primary Status Section

One chart or table that shows current status vs. target. This section directly answers the supported decision.

**Section header (takeaway-first):**  
Example: "Retention is 2.1pp below Q2 target — concentrated in the Enterprise segment"

Content options (choose one):
- Status vs. target bar or single metric with threshold line
- Segment breakdown table with metric color cells
- Trend line with target band

**Components:** `components/section-header.md` + `components/metric-color-cell.md`

Keep this section to one visual or one short table. Do not add a secondary chart in the same section.

---

### 4. Trend Panel

Shows how the primary KPI has moved over time. Supports the context → status sequence.

**Section header (takeaway-first):**  
Example: "Improvement stalled in Q1 after two strong quarters — Q2 trajectory is now flat"

Content:
- Time series of the primary KPI with a target band
- Period-over-period change table if the trend has segment-level variation

This section may be a chart placeholder with a brief description if no charting library is available.

---

### 5. Top Drivers / Segment Decomposition

What is causing the current state? Which segments or dimensions account for most of the gap?

**Section header (takeaway-first):**  
Example: "Enterprise accounts drive 71% of the retention gap — Mid-market is on track"

Content:
- Ranked segment table: segment, value, vs. target, status chip
- Maximum 8 rows. If more segments exist, show top 5 by gap and link to full list in appendix.

**Components:** `components/status-chips.md` + `components/metric-color-cell.md`

---

### 6. Risk and Opportunity Callouts

2–4 brief callout items that flag the most important exceptions or opportunities. These are the items that require attention or monitoring before the next review.

**Section header (takeaway-first):**  
Example: "One enterprise account is at risk of churn — requires intervention by Friday"

Content format: Each callout is a short `insight-card` style block with:
- Bold header: the specific finding
- 1–2 sentence explanation: what happened, why it matters
- Responsible owner and timing

Do not exceed 4 callout items. More than 4 means the summary is doing too little work — escalate the most critical ones and move the rest to the appendix.

---

### 7. Recommended Action

A single clear recommendation or decision prompt.

**Section header (takeaway-first):**  
Example: "Action required: escalate enterprise retention intervention to Q2 plan owners by May 22"

Content:
- The specific action, who owns it, and by when
- What "done" looks like (the outcome of taking the action)
- What happens if action is not taken (the cost of inaction)

This section should not be longer than 3–4 lines. If more explanation is needed, it means the recommendation needs more upstream analytical work — return to the analysis stage.

---

### 8. Footer (Data Contract)

Not a section — a footer line at the bottom of the page.

```
Data as of [date] · Source: [system or table name] · Definitions: [link or one-line note]
Owner: [team or person] · Refresh: [cadence]
```

Metric definitions must be reachable from here — either linked or written in a brief glossary below the footer.

---

### 9. Appendix (Minimal, Optional)

For this archetype, the appendix should be used only for:
- Full segment breakdown (if the driver table was limited to top 5)
- Metric definition glossary
- Data notes and known caveats

**Component:** `components/collapsible-appendix.md`

Do not include methodology, diagnostics, or model details in this archetype's appendix. The executive audience does not need them in this view.

---

## Layout Structure

```html
<div class="page">

  <!-- 1. Header -->
  <div class="page-header">
    <h1>[Business outcome question]</h1>
    <div class="page-meta">As of [date] · Source: [system]</div>
    <div class="verdict-band verdict-warning" role="status">
      <span>⚠</span>
      <span class="verdict-label">Q2 target at risk — enterprise intervention required</span>
    </div>
  </div>

  <!-- 2. KPI strip -->
  <section class="kpi-strip" aria-label="Key performance indicators">
    <!-- 3–5 kpi-card elements -->
  </section>

  <!-- 3. Primary status -->
  <section class="section-card">
    <header class="section-header">
      <h2 class="section-title">[Current state vs. target finding]</h2>
      <p class="section-meta">[Metric · scope · date range]</p>
    </header>
    <!-- status chart or table -->
  </section>

  <!-- 4. Trend panel -->
  <section class="section-card">
    <header class="section-header">
      <h2 class="section-title">[Trend finding]</h2>
      <p class="section-meta">[Metric · period · comparison baseline]</p>
    </header>
    <!-- trend chart -->
  </section>

  <!-- 5. Segment decomposition -->
  <section class="section-card">
    <header class="section-header">
      <h2 class="section-title">[Driver finding]</h2>
      <p class="section-meta">[Segment · metric · denominator]</p>
    </header>
    <table><!-- segment table with metric-color-cell and status chips --></table>
  </section>

  <!-- 6. Risk and opportunity callouts (2x2 grid) -->
  <section class="section-card">
    <header class="section-header">
      <h2 class="section-title">[Exception / opportunity finding]</h2>
      <p class="section-meta">[scope]</p>
    </header>
    <div class="callout-grid">
      <!-- 2–4 callout cards -->
    </div>
  </section>

  <!-- 7. Recommended action -->
  <section class="section-card">
    <header class="section-header">
      <h2 class="section-title">[Action statement]</h2>
      <p class="section-meta">[Owner · timing]</p>
    </header>
    <!-- action description -->
  </section>

  <!-- 8. Footer -->
  <footer class="dash-footer">
    Data as of [date] · Source: [system] · Definitions: [note] · Owner: [team]
  </footer>

  <!-- 9. Appendix (optional) -->
  <details class="appendix">
    <summary>Full Segment Breakdown</summary>
    <div class="appendix-body"><!-- ... --></div>
  </details>

</div>
```

---

## Self-Critique Checks for This Archetype

Before delivering:

- [ ] **Decision Clarity:** Can an executive answer the dashboard decision without scrolling?
- [ ] **Analytical Integrity:** Are metric definitions in the footer? Is the target visible on the primary status section? Is the date range explicit?
- [ ] **Visual Hierarchy:** Is the verdict band the first prominent visual? Do the KPI cards encode state with semantic color? Are all callout items brief?
- [ ] **Design Craft:** No jargon on the first screen. Section titles are business language, not technical labels. No raw field names visible.
- [ ] **Usability:** Print styles applied? Navigation hidden in print? Content fits within a standard slide or letter-page width if PDF is expected?

## Related Components and Parent Files

- `components/verdict-band.md`
- `components/kpi-strip.md`
- `components/metric-color-cell.md`
- `components/status-chips.md`
- `components/section-header.md`
- `components/collapsible-appendix.md`
- `../../design-systems/executive-editorial/DESIGN.md`
- `../../workflow/design-preflight.md`
- `../../checklists/dashboard-self-critique-checklist.md`
