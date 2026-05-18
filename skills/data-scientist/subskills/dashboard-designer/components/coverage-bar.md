# Coverage Bar

## Purpose

A horizontal fill bar that shows the completeness, availability, or coverage of a resource — data fields, features, test cases, segments, or model readiness dimensions. Provides a fast at-a-glance reading of how complete something is.

## When to Use

Use a coverage bar when:
- A table lists items with varying data availability and you want the completeness to be immediately scannable
- A summary card needs to show overall readiness without listing every item
- You are showing feature availability across a dataset where many features are partially populated

Common use cases:
- Feature coverage table (percentage of rows with non-null values)
- Data completeness by field or source
- Model readiness dimensions (validation %, test coverage %, documentation %)
- Segment completeness (% of segments with sufficient sample)

Do not use coverage bars for:
- Metric values (use metric color cells instead)
- Progress that is not meaningful as a percentage (use a status chip instead)
- Performance metrics — a 75% model accuracy displayed as a coverage bar implies "75% complete" which is misleading

## Data Required

- A numeric coverage value between 0 and 100
- A label for the item being measured
- Optional: a color threshold to distinguish sufficient from insufficient coverage

## Threshold Logic

Define thresholds appropriate to the domain. Common patterns:

| Coverage | Suggested class |
|---|---|
| ≥ 85% | `cov-high` (accent blue fill) |
| 50–84% | `cov-partial` (warning amber fill) |
| 1–49% | `cov-low` (warning amber fill) |
| 0% | `cov-zero` (negative red fill) |

## CSS Class Naming

```
.cov-bar-wrap     — flex row container (label + bar + value)
.cov-bar-bg       — the grey background track
.cov-bar-fill     — the colored fill inside the track
.cov-bar-fill.cov-high    — accent blue (high coverage)
.cov-bar-fill.cov-partial — warning amber (partial)
.cov-bar-fill.cov-low     — warning amber (low)
.cov-bar-fill.cov-zero    — negative red (missing)
.cov-val          — the numeric label at the right
```

## Accessibility Rules

- The bar is decorative — the numeric value must also appear in text form.
- Use `aria-hidden="true"` on the bar graphic; the text value carries the meaning.
- Do not omit the numeric label — the bar width alone is not precise enough for users who need exact values.
- For the zero case, include the word "missing" or "not available" in the label so color is not the only indicator.

## Common Mistakes

- Using accent blue for all coverage levels regardless of completeness — only high coverage should use the accent color.
- Setting the bar width to a pixel value instead of a percentage — always use `width: <N>%`.
- Applying the bar to metric performance values — coverage bars imply "how complete is this", not "how good is this value".
- Omitting the text value and relying on bar width for precision.

## Copy-Paste CSS

```css
/* ── Coverage bar ──────────────────────────────────────────────────── */
.cov-bar-wrap {
  display: flex;
  align-items: center;
  gap: 8px;
  min-width: 140px;
}

.cov-bar-bg {
  flex: 1;
  height: 6px;
  background: var(--border);
  border-radius: 3px;
  overflow: hidden;
}

.cov-bar-fill {
  height: 100%;
  border-radius: 3px;
  background: var(--accent);     /* default: high coverage */
  transition: width 0.2s ease;
}

.cov-bar-fill.cov-high    { background: var(--accent); }
.cov-bar-fill.cov-partial { background: var(--warning); }
.cov-bar-fill.cov-low     { background: var(--warning); opacity: 0.7; }
.cov-bar-fill.cov-zero    { background: var(--negative); width: 6px !important; border-radius: 3px; }

.cov-val {
  font-size: 11px;
  color: var(--text-secondary);
  min-width: 38px;
  text-align: right;
  font-family: var(--font-mono);
  font-variant-numeric: tabular-nums;
}
```

## Copy-Paste HTML — Inline Usage

```html
<!-- High coverage -->
<div class="cov-bar-wrap" aria-label="stat_l10 coverage: 75.9%">
  <div class="cov-bar-bg" aria-hidden="true">
    <div class="cov-bar-fill cov-high" style="width:75.9%"></div>
  </div>
  <span class="cov-val">75.9%</span>
</div>

<!-- Partial coverage -->
<div class="cov-bar-wrap" aria-label="actual_value coverage: 86.5%">
  <div class="cov-bar-bg" aria-hidden="true">
    <div class="cov-bar-fill cov-partial" style="width:86.5%"></div>
  </div>
  <span class="cov-val">86.5%</span>
</div>

<!-- Zero — not available -->
<div class="cov-bar-wrap" aria-label="starter: not available">
  <div class="cov-bar-bg" aria-hidden="true">
    <div class="cov-bar-fill cov-zero" style="width:0%"></div>
  </div>
  <span class="cov-val" style="color:var(--negative)">—</span>
</div>
```

## Copy-Paste HTML — In a Feature Coverage Table

```html
<table>
  <thead>
    <tr>
      <th>Feature</th>
      <th>Present</th>
      <th class="num">Coverage</th>
      <th style="min-width:160px;">Coverage bar</th>
      <th>Source note</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="font-family:var(--font-mono);font-size:12px;">stat_l10</td>
      <td><span class="chip chip-ready">yes</span></td>
      <td class="num">75.9%</td>
      <td>
        <div class="cov-bar-wrap" aria-hidden="true">
          <div class="cov-bar-bg">
            <div class="cov-bar-fill cov-high" style="width:75.9%"></div>
          </div>
          <span class="cov-val">75.9%</span>
        </div>
      </td>
      <td style="font-size:12px;color:var(--text-muted);">derived prior-only from clean CSV</td>
    </tr>
    <tr>
      <td style="font-family:var(--font-mono);font-size:12px;">starter</td>
      <td><span class="chip chip-partial">no</span></td>
      <td class="num">0.0%</td>
      <td>
        <div class="cov-bar-wrap" aria-hidden="true">
          <div class="cov-bar-bg">
            <div class="cov-bar-fill cov-zero" style="width:0%"></div>
          </div>
          <span class="cov-val" style="color:var(--negative)">—</span>
        </div>
      </td>
      <td style="font-size:12px;color:var(--text-muted);">not in clean CSV · future local enrichment</td>
    </tr>
  </tbody>
</table>
```

## JavaScript Helper

```javascript
/**
 * Returns the fill class based on coverage value and thresholds.
 * @param {number} coverage — 0–100
 * @param {number} highThreshold — minimum for "high" (default 85)
 * @param {number} partialThreshold — minimum for "partial" (default 50)
 * @returns {string} CSS class
 */
function coverageClass(coverage, highThreshold = 85, partialThreshold = 50) {
  if (coverage === 0) return 'cov-zero';
  if (coverage >= highThreshold) return 'cov-high';
  if (coverage >= partialThreshold) return 'cov-partial';
  return 'cov-low';
}
```

## Related Parent Files

- `components/status-chips.md` — chip for present/not-present status in the same table
- `components/collapsible-appendix.md` — feature coverage tables often live in appendix sections
- `../../workflow/design-preflight.md` — Step 9 (data contract covers feature completeness)
