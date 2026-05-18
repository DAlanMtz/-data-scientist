# Stability Heatmap

## Purpose

A matrix visualization that shows metric values across two dimensions, with cells color-coded using metric color classes. Common use cases: metric stability over time by group, segment performance across dimensions, model results across conditions, or cohort behavior across time periods.

Rows and columns can be any two categorical or temporal dimensions — this component is generic. The most common form is time period × group.

## When to Use

Use a stability heatmap when:
- You need to show whether a metric is stable or volatile across time periods and groups simultaneously
- The matrix has 5–40 cells (too few = use a table; too many = use small multiples or a BI tool)
- The viewer's question is "where does the pattern break down?" rather than "what is the aggregate?"

Do not use a stability heatmap for:
- Single-dimension lists (use a table with metric color cells)
- More than ~8 groups or ~12 time periods — readability collapses
- Continuous axes — use a scatter or line chart instead

## Data Required

- Row dimension: time periods, cohorts, horizons, or conditions
- Column dimension: groups, segments, families, models, or categories
- Cell value: the metric (shown as text inside the cell)
- Cell sub-value (optional): sample count, row count, or confidence context
- Null indicator: how to display missing or insufficient-sample cells

## Structure

```
[Optional group filter bar]
[Legend row]
[Heatmap table]
  [Row header] [Cell] [Cell] ... 
  ...
[Footnote: threshold definitions, sample size caveat]
```

## CSS Class Naming

```
.heatmap-wrap       — overflow-x: auto wrapper
.heatmap-table      — the <table> element
.heatmap-table th   — column headers
.hm-row-head        — row header cell
.hm-cell            — content flex container inside each td
.hm-value           — primary metric value text
.hm-sub             — sample count or subtext

/* Cell background colors (same as metric-color-cell.md) */
metric-strong background  → var(--positive-bg)  text → var(--positive)
metric-ok background      → #d4f1e2              text → #1d6040
metric-marginal background→ var(--warning-bg)   text → var(--warning)
metric-weak background    → var(--negative-bg)  text → var(--negative)
metric-na background      → var(--surface-alt)  text → var(--text-muted)
```

## Accessibility Rules

- Provide a `<caption>` on the table describing the matrix dimensions.
- Row headers use `scope="row"`; column headers use `scope="col"`.
- Each cell's full meaning should be readable as screen reader output: "Nov 2025: Group A: 55.3%, 282 rows".
- The legend must be visible and explain the threshold rules in text — not color alone.
- Do not use red/green as the only distinguisher between states; the numeric value inside each cell provides redundant encoding.

## Common Mistakes

- Coloring cells based on rank within the matrix rather than against a fixed threshold — this makes all datasets look balanced.
- Showing raw counts without the metric value — the viewer cannot tell if a high count cell is favorable.
- Omitting the sample size subtext — small-sample cells should be visually discounted.
- Building the heatmap with inline styles per cell — use `data-` attributes and JavaScript to apply classes programmatically.
- Not providing a legend — threshold rules must be visible on the dashboard.

## Copy-Paste CSS

```css
/* ── Stability heatmap ─────────────────────────────────────────────── */
.heatmap-wrap { overflow-x: auto; }

.heatmap-table {
  border-collapse: collapse;
  font-size: 12px;
  width: 100%;
  min-width: 480px;
}

.heatmap-table th {
  padding: 7px 10px;
  background: var(--surface-alt);
  font-size: 11px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.04em;
  color: var(--text-secondary);
  border-bottom: 1px solid var(--border);
  text-align: center;
  white-space: nowrap;
}

.heatmap-table th.hm-row-head { text-align: left; }

.heatmap-table td {
  padding: 6px 8px;
  border-bottom: 1px solid var(--border);
  border-right: 1px solid var(--border);
  text-align: center;
  vertical-align: middle;
  min-width: 80px;
}

.heatmap-table td.hm-row-head {
  text-align: left;
  font-weight: 600;
  color: var(--text);
  background: var(--surface-alt);
  border-right: 2px solid var(--border);
  white-space: nowrap;
  padding: 6px 12px 6px 10px;
}

/* Cell content layout */
.hm-cell {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2px;
}

.hm-value {
  font-weight: 700;
  font-size: 12px;
  font-variant-numeric: tabular-nums;
  line-height: 1.2;
}

.hm-sub {
  font-size: 10px;
  color: var(--text-muted);
  line-height: 1.2;
}

/* Cell state backgrounds — applied inline via JS or data attributes */
.hm-strong   { background: var(--positive-bg); }
.hm-ok       { background: #d4f1e2; }
.hm-marginal { background: var(--warning-bg); }
.hm-weak     { background: var(--negative-bg); }
.hm-na       { background: var(--surface-alt); }

/* Legend */
.hm-legend {
  display: flex;
  gap: 14px;
  flex-wrap: wrap;
  margin-bottom: 10px;
}

.hm-legend-item {
  display: flex;
  align-items: center;
  gap: 5px;
  font-size: 11px;
  color: var(--text-secondary);
}

.hm-swatch {
  width: 12px;
  height: 12px;
  border-radius: 2px;
  flex-shrink: 0;
}
```

## Copy-Paste HTML (Static)

```html
<!-- Legend -->
<div class="hm-legend" aria-label="Color legend">
  <div class="hm-legend-item">
    <div class="hm-swatch" style="background:var(--positive-bg)"></div> ≥ 54% Strong
  </div>
  <div class="hm-legend-item">
    <div class="hm-swatch" style="background:#d4f1e2"></div> 52–53.9% OK
  </div>
  <div class="hm-legend-item">
    <div class="hm-swatch" style="background:var(--warning-bg)"></div> 50–51.9% Marginal
  </div>
  <div class="hm-legend-item">
    <div class="hm-swatch" style="background:var(--negative-bg)"></div> &lt; 50% Weak
  </div>
  <div class="hm-legend-item">
    <div class="hm-swatch" style="background:var(--surface-alt);border:1px solid var(--border)"></div> No data
  </div>
</div>

<!-- Heatmap table (static, 3 groups × 4 periods) -->
<div class="heatmap-wrap">
  <table class="heatmap-table">
    <caption class="sr-only">Metric stability by time period and group. Values shown as metric percentage with row count below.</caption>
    <thead>
      <tr>
        <th class="hm-row-head" scope="col">Period</th>
        <th scope="col">Group A</th>
        <th scope="col">Group B</th>
        <th scope="col">Group C</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td class="hm-row-head" scope="row">Nov 2025</td>
        <td class="hm-strong">
          <div class="hm-cell">
            <span class="hm-value" style="color:var(--positive)">55.3%</span>
            <span class="hm-sub">282</span>
          </div>
        </td>
        <td class="hm-ok">
          <div class="hm-cell">
            <span class="hm-value" style="color:#1d6040">52.7%</span>
            <span class="hm-sub">1,487</span>
          </div>
        </td>
        <td class="hm-marginal">
          <div class="hm-cell">
            <span class="hm-value" style="color:var(--warning)">50.7%</span>
            <span class="hm-sub">2,045</span>
          </div>
        </td>
      </tr>
      <tr>
        <td class="hm-row-head" scope="row">Dec 2025</td>
        <td class="hm-strong">
          <div class="hm-cell">
            <span class="hm-value" style="color:var(--positive)">54.8%</span>
            <span class="hm-sub">566</span>
          </div>
        </td>
        <td class="hm-ok">
          <div class="hm-cell">
            <span class="hm-value" style="color:#1d6040">53.7%</span>
            <span class="hm-sub">609</span>
          </div>
        </td>
        <td class="hm-ok">
          <div class="hm-cell">
            <span class="hm-value" style="color:#1d6040">52.1%</span>
            <span class="hm-sub">1,415</span>
          </div>
        </td>
      </tr>
    </tbody>
  </table>
</div>
```

## JavaScript — Build Matrix from Data

```javascript
/**
 * Builds a heatmap table from structured data.
 *
 * @param {HTMLElement} container — the element to render into
 * @param {string[]} rows — row labels (e.g., months)
 * @param {string[]} cols — column labels (e.g., group names)
 * @param {Object} data — { [row]: { [col]: { value: number, sub: number|null } } }
 * @param {Function} classifyFn — (value) => 'hm-strong'|'hm-ok'|'hm-marginal'|'hm-weak'|'hm-na'
 * @param {Function} formatFn — (value) => string (e.g., v => v.toFixed(1) + '%')
 * @param {Function} colorFn — (cls) => CSS color string for the value text
 */
function buildHeatmap(container, rows, cols, data, classifyFn, formatFn, colorFn) {
  const table = document.createElement('table');
  table.className = 'heatmap-table';

  // Header row
  const thead = document.createElement('thead');
  const hr = document.createElement('tr');
  const th0 = document.createElement('th');
  th0.className = 'hm-row-head';
  th0.scope = 'col';
  hr.appendChild(th0);
  cols.forEach(col => {
    const th = document.createElement('th');
    th.scope = 'col';
    th.textContent = col;
    hr.appendChild(th);
  });
  thead.appendChild(hr);
  table.appendChild(thead);

  // Body rows
  const tbody = document.createElement('tbody');
  rows.forEach(row => {
    const tr = document.createElement('tr');
    const rowHead = document.createElement('td');
    rowHead.className = 'hm-row-head';
    rowHead.scope = 'row';
    rowHead.textContent = row;
    tr.appendChild(rowHead);

    cols.forEach(col => {
      const entry = (data[row] || {})[col];
      const td = document.createElement('td');

      if (!entry || entry.value === null || entry.value === undefined) {
        td.className = 'hm-na';
        td.innerHTML = `<div class="hm-cell"><span class="hm-value" style="color:var(--text-muted)">—</span></div>`;
      } else {
        const cls = classifyFn(entry.value);
        const color = colorFn(cls);
        td.className = cls;
        const sub = entry.sub != null
          ? `<span class="hm-sub">${entry.sub.toLocaleString()}</span>`
          : '';
        td.innerHTML = `<div class="hm-cell">
          <span class="hm-value" style="color:${color}">${formatFn(entry.value)}</span>
          ${sub}
        </div>`;
      }
      tr.appendChild(td);
    });
    tbody.appendChild(tr);
  });
  table.appendChild(tbody);
  container.innerHTML = '';
  container.appendChild(table);
}

// Example threshold function (higher-is-better, 4-tier):
function classifyWR(value) {
  if (value >= 54) return 'hm-strong';
  if (value >= 52) return 'hm-ok';
  if (value >= 50) return 'hm-marginal';
  return 'hm-weak';
}

// Color map for text inside cells:
const hmColorMap = {
  'hm-strong':   'var(--positive)',
  'hm-ok':       '#1d6040',
  'hm-marginal': 'var(--warning)',
  'hm-weak':     'var(--negative)',
  'hm-na':       'var(--text-muted)'
};
```

## Related Parent Files

- `components/filter-bar.md` — group filter buttons to show subsets of columns
- `components/metric-color-cell.md` — inline metric cells outside the heatmap
- `../../workflow/design-preflight.md` — Step 7 (uncertainty section shows stability heatmap)
