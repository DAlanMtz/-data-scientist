# Archetype: Model Monitoring Dashboard

## Purpose

A real-time or near-real-time operational dashboard for tracking a deployed ML model's health: prediction volume, performance drift, calibration, data quality, segment stability, and alert state. The viewer is a data scientist or ML engineer who needs to know whether the model is performing as expected and whether any action is required.

## When to Use

- Post-deployment monitoring of a live ML model
- Scheduled model performance review (daily, weekly)
- Drift investigation: diagnosing whether model quality has degraded
- Pre-retraining assessment: deciding whether to retrain and when

## Design System Default

`operational-command-center` — dark mode, high information density, status-coded.  
Use `clean-saas-analytics` if the audience prefers a light dashboard or if the output is a PDF report.

---

## Principles for This Archetype

- **Status is the first question.** Is the model healthy? Any blocking alerts?
- **Trend over time, not just current snapshot.** Monitoring dashboards live for weeks or months — trend and drift matter more than absolute current value.
- **Alert state before detail.** If there are active alerts, they must be prominent.
- **Segment-level and aggregate-level in the same view.** Aggregate metrics can look stable while a critical segment has failed.
- **Data quality upstream of model quality.** Drift in model output often originates from feature drift or data pipeline failures — show data quality first.

---

## Section Composition

### 1. Model Identity Header

```
H1: Model name and version — not a dashboard name
Metadata: environment · deployment date · current model version · data as-of timestamp
Data freshness indicator: timestamp + source pipeline status
```

This is operational content, not a verdict. Do not use a verdict band here unless there is a high-level "model status" conclusion. Replace with the model version and freshness stamp.

---

### 2. Alert Strip

Before the KPI strip: a brief list of active alerts (if any). If there are no active alerts, show a single "No active alerts" confirmation line.

**Severity levels:**
- Critical: model is giving incorrect predictions; blocker — action required immediately
- High: performance degraded below threshold; action required this cycle
- Medium: trend is concerning; monitor closely
- Low: informational; log and review at next scheduled check

**Component:** `components/status-chips.md` for alert severity chips

```html
<section class="alert-strip" aria-label="Active alerts">
  <div class="alert-item alert-critical">
    <span class="chip chip-danger">critical</span>
    <span>Feature X null rate spiked to 34% — data pipeline issue upstream</span>
    <span class="alert-ts">2026-05-18 14:23</span>
  </div>
  <div class="alert-item alert-high">
    <span class="chip chip-monitor">high</span>
    <span>Precision on Segment B dropped 4.2pp below deployment baseline</span>
    <span class="alert-ts">2026-05-18 09:00</span>
  </div>
</section>
```

---

### 3. KPI Strip

| Slot | Role | Example |
|---|---|---|
| 1 | Prediction volume | Daily / weekly predictions served |
| 2 | Primary performance metric | AUC, F1, precision@k, RMSE, WR |
| 3 | Calibration / reliability | Expected calibration error, reliability |
| 4 | Data quality indicator | Null rate, feature drift flag count |
| 5 | Time since last retrain | Days since last retrain trigger evaluated |

**Component:** `components/kpi-strip.md`

Use `kpi-negative` for any metric that has crossed its alert threshold. Use `kpi-warning` for approaching-threshold states.

---

### 4. Performance Trend Section

Shows the primary performance metric over time against the deployment baseline and acceptable range.

**Section header (takeaway-first):**  
Example: "Precision has drifted 3.1pp below deployment baseline over the last 14 days"

Content:
- Time series chart of the primary metric with threshold band
- Trend table: value by period, vs. deployment baseline, status chip

**Component:** `components/section-header.md` + `components/metric-color-cell.md`

This section must show the **deployment baseline** as a reference line, not just the current value in isolation.

---

### 5. Data Quality / Feature Drift Section

Shows the health of the input data: null rates, out-of-range values, and feature distribution drift indicators.

**Section header (takeaway-first):**  
Example: "Feature X null rate elevated since May 15 — likely upstream pipeline delay"

Content:
- Feature coverage table: feature name, expected coverage, current coverage, drift status chip, coverage bar
- Flag count: number of features above drift threshold

**Components:** `components/coverage-bar.md` + `components/status-chips.md`

---

### 6. Segment Stability Heatmap

Shows model performance broken down by segment × time period. Aggregate stability can mask critical segment failures.

**Section header (takeaway-first):**  
Example: "Segment B performance is 5pp below deployment baseline — aggregate metrics hide this"

**Components:** `components/stability-heatmap.md` + `components/filter-bar.md`

Heatmap structure:
- Rows: time periods (days, weeks, months)
- Columns: model segments (customer type, geography, product line, risk tier)
- Cells: primary metric value + prediction count

---

### 7. Calibration / Threshold Status

Is the model's probability output calibrated? Is the decision threshold still appropriate?

**Section header (takeaway-first):**  
Example: "Calibration is stable across deciles — threshold at 0.45 maintains target precision"

Content:
- Calibration summary: expected vs. observed rate by decile (table or chart)
- Current threshold and resulting precision/recall/cost tradeoff
- Threshold recommendation chip: `chip-ready` if no change needed; `chip-warn` if review recommended

---

### 8. Retraining / Rollback Notes

Decision-support section for the data scientist. States the retraining trigger status and rollback option.

**Section header (takeaway-first):**  
Example: "Retraining trigger is not yet met — drift is trending but has not crossed the defined threshold"

Content:
- Retraining trigger definition and current state
- Last retrain: date, evaluation result, deployment outcome
- Rollback option: prior model version name and known performance
- Recommended action: monitor / schedule retrain / trigger rollback

**Component:** `components/verdict-band.md` — use for the recommended action if it is actionable

---

### 9. Appendix (Detailed Diagnostics)

**Component:** `components/collapsible-appendix.md`

Typical appendix sections:
- Full prediction volume by segment (if volume section was summarized)
- Detailed feature drift statistics (PSI values, distribution shift metrics)
- Error slice analysis (FP/FN breakdown by feature range)
- Confusion matrix or precision/recall table at current threshold
- Model card summary reference

---

## Alert Strip CSS

```css
/* ── Alert strip ───────────────────────────────────────────────────── */
.alert-strip {
  margin-bottom: 16px;
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.alert-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 14px;
  border-radius: var(--radius-sm);
  font-size: 13px;
  border-left: 4px solid transparent;
}

.alert-critical {
  background: var(--negative-bg);
  border-left-color: var(--negative);
  color: var(--text);
}

.alert-high {
  background: var(--warning-bg);
  border-left-color: var(--warning);
  color: var(--text);
}

.alert-low {
  background: var(--surface-alt);
  border-left-color: var(--border-strong);
  color: var(--text-secondary);
}

.alert-none {
  background: var(--positive-bg);
  border-left-color: var(--positive);
  color: var(--positive);
  font-weight: 600;
  font-size: 13px;
  padding: 8px 14px;
  border-radius: var(--radius-sm);
}

.alert-ts {
  margin-left: auto;
  font-size: 11px;
  color: var(--text-muted);
  white-space: nowrap;
  font-family: var(--font-mono);
}
```

---

## Layout Structure

```html
<div class="page">

  <!-- 1. Model identity header -->
  <div class="page-header">
    <h1>[Model Name] v[version] · [environment]</h1>
    <div class="page-meta">
      Deployed: [date] · Data as of: [timestamp] · Pipeline: <span class="chip chip-ready">healthy</span>
    </div>
  </div>

  <!-- 2. Alert strip -->
  <section class="alert-strip" aria-label="Active alerts">
    <div class="alert-none">✓ No active alerts as of [timestamp]</div>
    <!-- or: alert items if alerts exist -->
  </section>

  <!-- 3. KPI strip -->
  <section class="kpi-strip" aria-label="Model health indicators">
    <!-- 5 kpi-card elements -->
  </section>

  <!-- 4. Performance trend -->
  <section class="section-card">
    <header class="section-header">
      <h2 class="section-title">[Performance trend finding]</h2>
      <p class="section-meta">[Metric · scope · vs. deployment baseline]</p>
    </header>
    <!-- trend chart or table -->
  </section>

  <!-- 5. Data quality / feature drift -->
  <section class="section-card">
    <header class="section-header">
      <h2 class="section-title">[Data quality finding]</h2>
      <p class="section-meta">[Feature scope · period · drift threshold]</p>
    </header>
    <table><!-- feature coverage table with coverage bars --></table>
  </section>

  <!-- 6. Segment stability heatmap -->
  <section class="section-card">
    <header class="section-header">
      <h2 class="section-title">[Segment stability finding]</h2>
      <p class="section-meta">[Segments · metric · period]</p>
    </header>
    <div class="filter-bar"><!-- segment filter --></div>
    <div class="hm-legend"><!-- legend --></div>
    <div class="heatmap-wrap">
      <table class="heatmap-table"><!-- segment × period heatmap --></table>
    </div>
  </section>

  <!-- 7. Calibration / threshold -->
  <section class="section-card">
    <header class="section-header">
      <h2 class="section-title">[Calibration finding]</h2>
      <p class="section-meta">[Threshold · metric · scope]</p>
    </header>
    <!-- calibration table or chart -->
  </section>

  <!-- 8. Retraining / rollback -->
  <section class="section-card">
    <header class="section-header">
      <h2 class="section-title">[Retraining status finding]</h2>
      <p class="section-meta">[Trigger definition · current state]</p>
    </header>
    <!-- trigger status, last retrain info, recommendation -->
    <div class="verdict-band verdict-neutral" role="status">
      <span>ℹ</span>
      <span class="verdict-label">retrain_not_yet_triggered · monitor_through_[date]</span>
    </div>
  </section>

  <!-- 9. Appendix -->
  <details class="appendix">
    <summary>Diagnostics — Feature Drift Details</summary>
    <div class="appendix-body"><!-- PSI table, distribution stats --></div>
  </details>

  <details class="appendix">
    <summary>Diagnostics — Error Slice Analysis</summary>
    <div class="appendix-body"><!-- FP/FN by slice --></div>
  </details>

</div>
```

---

## Self-Critique Checks for This Archetype

Before delivering:

- [ ] **Decision Clarity:** Is it immediately clear whether the model requires action?
- [ ] **Analytical Integrity:** Is the deployment baseline explicitly shown as the reference? Are all metrics defined? Are segment counts visible to discount low-sample cells?
- [ ] **Visual Hierarchy:** Are critical alerts shown before the KPI strip? Is segment-level instability visible even if aggregates look healthy?
- [ ] **Design Craft:** Are alert severity levels encoded with both color and chip labels? Is the data freshness timestamp prominent?
- [ ] **Usability:** Does the heatmap filter work? Are appendix sections collapsed by default? Is the alert strip scannable in under 5 seconds?

## Related Components and Parent Files

- `components/verdict-band.md`
- `components/kpi-strip.md`
- `components/status-chips.md`
- `components/coverage-bar.md`
- `components/stability-heatmap.md`
- `components/filter-bar.md`
- `components/section-header.md`
- `components/collapsible-appendix.md`
- `../../design-systems/operational-command-center/DESIGN.md`
- `../../references/model-monitoring-and-drift.md`
- `../../workflow/design-preflight.md`
- `../../checklists/dashboard-self-critique-checklist.md`
