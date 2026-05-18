# Metric Color Cell

## Purpose

A table cell or inline value display that uses background color to encode where a metric falls relative to thresholds. Used in summary tables, stability heatmaps, and comparison grids where multiple values need quick visual scanning.

## When to Use

Use metric color cells when:
- A table contains many numeric values that viewers must scan to find good/bad states
- A heatmap requires color-coded matrix cells
- A comparison table needs at-a-glance differentiation across rows and columns

Do not use metric color cells for:
- Status classification of entities (use status chips instead)
- Single highlighted values outside a table context (use KPI variant coloring instead)

## Threshold Logic

The classes are generic — the threshold values are data-specific. Define the thresholds for your metric in the dashboard's metric contract, then apply the appropriate class.

| Class | Semantic | Typical use |
|---|---|---|
| `metric-strong` | Well above target; clearly favorable | Green fill |
| `metric-ok` | Above target; acceptable | Light green fill |
| `metric-marginal` | Near threshold; borderline | Amber fill |
| `metric-weak` | Below threshold; unfavorable | Red fill |
| `metric-na` | No data or insufficient sample | Grey fill |

### Higher-is-better metric example

```
≥ 54%  → metric-strong
≥ 52%  → metric-ok
≥ 50%  → metric-marginal
< 50%  → metric-weak
```

### Lower-is-better metric example (e.g., error rate, churn rate)

```
< 2%   → metric-strong
< 5%   → metric-ok
< 10%  → metric-marginal
≥ 10%  → metric-weak
```

### Target-band metric example (e.g., coverage, fill rate)

```
85–100%  → metric-strong
70–84%   → metric-ok
50–69%   → metric-marginal
< 50%    → metric-weak
```

Document the chosen thresholds in the metric/data contract so viewers can understand the coloring.

## CSS Class Naming

```
.metric-cell        — base wrapper (inline-block or table cell content)
.metric-strong      — green fill, green text
.metric-ok          — light green fill, dark green text
.metric-marginal    — amber fill, amber text
.metric-weak        — red fill, red text
.metric-na          — grey fill, muted text
```

## Accessibility Rules

- Never use color as the only encoding. Include the numeric value inside every cell.
- Use `title` attributes or a visible legend to explain the threshold rules.
- Ensure color/text contrast meets 4.5:1 in each variant.
- For the stability heatmap, also show row counts or sample size below the metric value so viewers can discount low-sample readings.

## Common Mistakes

- Defining thresholds from the data range (min–max) rather than business-meaningful targets — this makes everything "ok" or distributes colors artificially.
- Using the same green color for all "above zero" or "non-missing" values — green means favorable status, not presence.
- Applying metric-strong to cells that happen to have the highest value in a column but are still below target.
- Omitting the numeric value and relying on color alone.

## Copy-Paste CSS

```css
/* ── Metric color cells ────────────────────────────────────────────── */
.metric-cell {
  display: inline-block;
  font-weight: 700;
  font-size: 12px;
  font-variant-numeric: tabular-nums;
  padding: 3px 8px;
  border-radius: var(--radius-sm);
  white-space: nowrap;
  line-height: 1.5;
}

.metric-strong   { background: var(--positive-bg);  color: var(--positive); }
.metric-ok       { background: #d4f1e2;              color: #1d6040; }
.metric-marginal { background: var(--warning-bg);    color: var(--warning); }
.metric-weak     { background: var(--negative-bg);   color: var(--negative); }
.metric-na       { background: var(--surface-alt);   color: var(--text-muted); }
```

## Copy-Paste HTML — Inline Usage

```html
<!-- Higher-is-better: win rate example -->
<span class="metric-cell metric-strong">56.2%</span>
<span class="metric-cell metric-ok">52.4%</span>
<span class="metric-cell metric-marginal">50.8%</span>
<span class="metric-cell metric-weak">47.3%</span>
<span class="metric-cell metric-na">—</span>
```

## Copy-Paste HTML — Table Cell Usage

```html
<table>
  <thead>
    <tr>
      <th>Group</th>
      <th class="num">Value</th>
      <th class="num">vs target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Segment A</td>
      <td class="num"><span class="metric-cell metric-strong">56.2%</span></td>
      <td class="num" style="color:var(--positive)">+4.2pp</td>
    </tr>
    <tr>
      <td>Segment B</td>
      <td class="num"><span class="metric-cell metric-ok">52.4%</span></td>
      <td class="num" style="color:var(--positive)">+0.4pp</td>
    </tr>
    <tr>
      <td>Segment C</td>
      <td class="num"><span class="metric-cell metric-marginal">50.8%</span></td>
      <td class="num" style="color:var(--warning)">−1.2pp</td>
    </tr>
    <tr>
      <td>Segment D</td>
      <td class="num"><span class="metric-cell metric-weak">47.3%</span></td>
      <td class="num" style="color:var(--negative)">−4.7pp</td>
    </tr>
  </tbody>
</table>
```

## JavaScript Helper — Assign Class from Value

For higher-is-better metrics with configurable thresholds:

```javascript
/**
 * Returns the metric cell class for a higher-is-better metric.
 * @param {number} value — the metric value (e.g., 52.4)
 * @param {object} thresholds — { strong, ok, marginal }
 * @returns {string} CSS class name
 */
function metricClass(value, thresholds = { strong: 54, ok: 52, marginal: 50 }) {
  if (value === null || value === undefined) return 'metric-na';
  if (value >= thresholds.strong)   return 'metric-strong';
  if (value >= thresholds.ok)       return 'metric-ok';
  if (value >= thresholds.marginal) return 'metric-marginal';
  return 'metric-weak';
}

// Usage:
const cls = metricClass(52.4, { strong: 54, ok: 52, marginal: 50 });
cell.innerHTML = `<span class="metric-cell ${cls}">${value.toFixed(1)}%</span>`;
```

## Related Parent Files

- `components/stability-heatmap.md` — heatmap matrix uses metric color cells in each cell
- `components/status-chips.md` — for entity-level status (not metric values)
- `../../workflow/design-preflight.md` — Step 9 (metric definitions must be confirmed before thresholds are set)
