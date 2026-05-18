# KPI Strip

## Purpose

A horizontal strip of 3–5 cards summarizing the decision-critical metrics at the top of the dashboard. The KPI strip is the first data the viewer encounters — every card must earn its place by directly supporting the dashboard decision.

## When to Use

Use on every stakeholder-facing dashboard. Place immediately after the verdict band (if present) and before any charts or tables.

## Data Required

For each card:
- **Label** — short, business-language name (not a field name)
- **Value** — the current metric value, formatted for humans
- **Context** — delta vs. prior period, vs. target, or vs. baseline; or a status note
- **Semantic variant** — which color treatment reflects the current state

## Recommended 5-Card Composition

| Slot | Role | Example |
|---|---|---|
| 1 | Scale / volume | "Eligible rows", "Active accounts", "Sample size" |
| 2 | Primary outcome | "Win rate", "Conversion rate", "Precision" |
| 3 | Readiness / status | "Families at target", "Models in production", "Tests passing" |
| 4 | Risk / exception | "Families needing review", "Open alerts", "Instability flags" |
| 5 | Data quality / completeness | "Feature coverage", "Data freshness", "Missing rate" |

Fewer than 5 is fine. More than 5 is not — split the excess into the body sections.

## CSS Class Naming

```
.kpi-strip          — wrapper grid
.kpi-card           — individual card
.kpi-card.kpi-neutral   — no directional signal (volume, scale)
.kpi-card.kpi-positive  — favorable state
.kpi-card.kpi-warning   — caution or monitor
.kpi-card.kpi-negative  — blocking or failed
.kpi-card.kpi-accent    — primary/highlighted metric
.kpi-label          — small caps metric name
.kpi-value          — large numeric value
.kpi-sub            — delta, status note, or context line
```

## Visual Rules

- Top border accent encodes semantic state (positive = green, warning = amber, negative = red, neutral = accent blue).
- Value font: 24–28px, weight 700.
- Label: 11px, uppercase, letter-spaced, `var(--text-muted)`.
- Sub: 11–12px, `var(--text-muted)`.
- Cards do not scroll or truncate. If the value is too wide, reduce font size to 20px before wrapping.

## Accessibility Rules

- Each card is an `<article>` with a descriptive `aria-label` if the label alone is ambiguous.
- Do not rely only on border-top color to convey state — the `.kpi-sub` line should also state the status in words.
- Contrast: positive/warning/negative value text on their background fills meets 4.5:1.

## Common Mistakes

- Using a KPI card to surface a top-level recommendation or verdict. Use the verdict band (`components/verdict-band.md`) for that.
- Using more than 5 cards. The strip becomes unreadable and loses hierarchy.
- Using the same neutral style for all cards, eliminating semantic signal.
- Writing field names as labels ("over_was_correct" instead of "Win rate").
- Omitting the context line — a KPI value without a comparison or status note provides no decision signal.

## Copy-Paste CSS

```css
/* ── KPI strip ─────────────────────────────────────────────────────── */
.kpi-strip {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 12px;
  margin-bottom: 20px;
}

.kpi-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 14px 16px;
  box-shadow: var(--shadow);
}

/* Semantic top-border variants */
.kpi-card.kpi-neutral  { border-top: 3px solid var(--accent); }
.kpi-card.kpi-positive { border-top: 3px solid var(--positive); }
.kpi-card.kpi-warning  { border-top: 3px solid var(--warning); }
.kpi-card.kpi-negative { border-top: 3px solid var(--negative); }
.kpi-card.kpi-accent   { border-top: 3px solid var(--accent); background: var(--accent-light); }

/* Value color follows state */
.kpi-card.kpi-neutral  .kpi-value { color: var(--accent); }
.kpi-card.kpi-positive .kpi-value { color: var(--positive); }
.kpi-card.kpi-warning  .kpi-value { color: var(--warning); }
.kpi-card.kpi-negative .kpi-value { color: var(--negative); }
.kpi-card.kpi-accent   .kpi-value { color: var(--accent); }

.kpi-label {
  font-size: 11px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--text-muted);
  margin-bottom: 6px;
}

.kpi-value {
  font-size: 26px;
  font-weight: 700;
  line-height: 1.1;
  color: var(--text); /* overridden by variant classes above */
}

.kpi-sub {
  font-size: 11px;
  color: var(--text-muted);
  margin-top: 4px;
  line-height: 1.4;
}

/* Responsive */
@media (max-width: 1024px) {
  .kpi-strip { grid-template-columns: repeat(3, 1fr); }
}

@media (max-width: 700px) {
  .kpi-strip { grid-template-columns: repeat(2, 1fr); }
}
```

## Copy-Paste HTML

```html
<section class="kpi-strip" aria-label="Key performance indicators">

  <!-- Slot 1: volume / scale — neutral -->
  <article class="kpi-card kpi-neutral" aria-label="Eligible rows">
    <div class="kpi-label">Eligible rows</div>
    <div class="kpi-value">37,843</div>
    <div class="kpi-sub">all 6 families combined</div>
  </article>

  <!-- Slot 2: primary outcome — positive or warning depending on state -->
  <article class="kpi-card kpi-positive" aria-label="Families at target">
    <div class="kpi-label">Families at target</div>
    <div class="kpi-value">5 / 6</div>
    <div class="kpi-sub">≥ 52% win rate in selected pool</div>
  </article>

  <!-- Slot 3: readiness / status — warning -->
  <article class="kpi-card kpi-warning" aria-label="Monitoring required">
    <div class="kpi-label">Monitoring required</div>
    <div class="kpi-value">4 / 6</div>
    <div class="kpi-sub">month instability flag active</div>
  </article>

  <!-- Slot 4: risk / exception — negative -->
  <article class="kpi-card kpi-negative" aria-label="Needs enrichment">
    <div class="kpi-label">Needs enrichment</div>
    <div class="kpi-value">1 / 6</div>
    <div class="kpi-sub">Points OVER · OOT fails</div>
  </article>

  <!-- Slot 5: data quality — neutral or warning -->
  <article class="kpi-card kpi-neutral" aria-label="Feature coverage">
    <div class="kpi-label">Feature coverage</div>
    <div class="kpi-value">76–100%</div>
    <div class="kpi-sub">7 fields missing from clean CSV</div>
  </article>

</section>
```

## Related Parent Files

- `../../references/visual-report-design-system.md` — token values
- `../../workflow/design-preflight.md` — Step 6 (KPI hierarchy)
- `components/verdict-band.md` — for top-level recommendations (not KPI cards)
