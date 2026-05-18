# Verdict Band

## Purpose

A prominent visual element near the dashboard header that surfaces the top-level recommendation, model status, release decision, or overall conclusion. The verdict belongs near the top of the page where it cannot be missed — not buried in a KPI card, section header, or table footnote.

## When to Use

Use a verdict band when:
- The dashboard has a single primary recommendation or action (e.g., "ready to promote", "needs enrichment", "deploy with monitoring")
- A model, system, or analysis result has an overall status that gates downstream action
- The decision-maker needs to see the conclusion before reading any detail

Do not use a verdict band when:
- The dashboard has no single recommendation (use a summary section header instead)
- The verdict is a metric value — use a KPI card with the appropriate semantic variant
- The dashboard is purely exploratory — leave the conclusion to the body sections

## Variants

| Class | State | When |
|---|---|---|
| `verdict-warning` | Proceed with conditions | System is usable but has active caveats; review required before production |
| `verdict-success` | Cleared / approved | System passed all checks; ready to promote or deploy |
| `verdict-danger` | Blocked | A critical issue prevents use; must be resolved before proceeding |
| `verdict-neutral` | Status unknown / informational | Decision pending more information; no blocking issue but no clearance either |

## Structure

```
[icon/prefix]  [recommendation code or short label]
```

The label should be a machine-readable status code or a concise business phrase — not a sentence. Save explanation for the section below the band.

## Visual Rules

- Left border accent (4px) distinguishes it from a plain callout box.
- Monospace font for status codes; sans-serif for business phrases.
- Place immediately after the page title and metadata line, before the KPI strip.
- Do not place it inside a card — it should span the full content width.
- Maximum one verdict band per dashboard. If multiple systems need status, put them in a status table in the body.

## Accessibility Rules

- The verdict band uses `role="status"` so assistive technology announces it.
- Icon/emoji prefix must be accompanied by a text label — never icon alone.
- The band's meaning must not depend on color alone: the prefix symbol (✓, ⚠, ✕, ℹ) provides a secondary encoding.

## Common Mistakes

- Putting a verbose recommendation paragraph inside the verdict band — use a concise code or phrase; put explanation in the section below.
- Using a KPI card with a negative semantic variant as a de facto verdict — the verdict band has a distinct visual weight and position that makes it scannable at a glance.
- Creating multiple verdict bands for sub-findings — use one band for the overall conclusion, status chips for individual items.
- Using the `verdict-success` variant when the system is ready-but-monitor (use `verdict-warning` with a "proceed with monitoring" label instead).

## Copy-Paste CSS

```css
/* ── Verdict band ──────────────────────────────────────────────────── */
.verdict-band {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 9px 16px;
  border-radius: 0 var(--radius-sm) var(--radius-sm) 0;
  font-size: 13px;
  font-weight: 600;
  margin-bottom: 20px;
  max-width: 100%;
}

.verdict-band .verdict-label {
  font-family: var(--font-mono);
  letter-spacing: 0.01em;
}

.verdict-warning {
  background: var(--warning-bg);
  border-left: 4px solid var(--warning);
  color: var(--warning);
}

.verdict-success {
  background: var(--positive-bg);
  border-left: 4px solid var(--positive);
  color: var(--positive);
}

.verdict-danger {
  background: var(--negative-bg);
  border-left: 4px solid var(--negative);
  color: var(--negative);
}

.verdict-neutral {
  background: var(--surface-alt);
  border-left: 4px solid var(--border-strong);
  color: var(--text-secondary);
}
```

## Copy-Paste HTML

```html
<!-- Warning: proceed with conditions -->
<div class="verdict-band verdict-warning" role="status" aria-label="Overall status: partial, more enrichment needed">
  <span aria-hidden="true">⚠</span>
  <span class="verdict-label">nba_baseline_partial_more_enrichment_needed</span>
</div>

<!-- Success: cleared -->
<div class="verdict-band verdict-success" role="status" aria-label="Overall status: ready for promotion">
  <span aria-hidden="true">✓</span>
  <span class="verdict-label">baseline_ready_for_star_tiering</span>
</div>

<!-- Danger: blocked -->
<div class="verdict-band verdict-danger" role="status" aria-label="Overall status: blocked, critical issue">
  <span aria-hidden="true">✕</span>
  <span class="verdict-label">validation_gate_failed_retrain_required</span>
</div>

<!-- Neutral: status pending -->
<div class="verdict-band verdict-neutral" role="status" aria-label="Overall status: under review">
  <span aria-hidden="true">ℹ</span>
  <span class="verdict-label">pending_stakeholder_review</span>
</div>
```

## Placement in Page

```html
<div class="page-header">
  <h1>Six-Family NBA-First Clean Baseline Rebuild</h1>
  <div class="page-meta">2026-05-18 · 37,843 eligible rows</div>

  <!-- Verdict band: directly after metadata, before KPI strip -->
  <div class="verdict-band verdict-warning" role="status">
    <span aria-hidden="true">⚠</span>
    <span class="verdict-label">six_family_nba_first_baseline_partial_more_enrichment_needed</span>
  </div>
</div>

<!-- KPI strip follows -->
<section class="kpi-strip"> ... </section>
```

## Related Parent Files

- `components/kpi-strip.md` — KPI cards follow the verdict band
- `components/section-header.md` — Section-level findings use section titles, not verdict bands
- `../../workflow/design-preflight.md` — Step 2 (decision supported) produces the verdict
