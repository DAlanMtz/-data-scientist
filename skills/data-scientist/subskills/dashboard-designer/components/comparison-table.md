# Comparison Table

## Purpose

A structured table that places multiple approaches, models, strategies, or configurations side by side for direct comparison. The highlighted column shows the recommended or primary approach; other columns provide context and benchmarks.

## When to Use

Use a comparison table when:
- Two or more approaches produce the same type of output and the decision-maker needs to choose between them
- A primary result needs to be validated by comparing it to a known baseline or benchmark
- Multiple systems are being evaluated on the same metric set simultaneously

Common use cases:
- Model bakeoff: approach A vs. approach B vs. baseline
- Strategy benchmark: recommended rule vs. market-aware threshold vs. simple odds filter
- Cohort comparison: segment A vs. B vs. C on the same metrics
- Data source comparison: source 1 vs. source 2 vs. combined

## Data Required

- Row items: entities being evaluated (families, models, cohorts, segments)
- Column groups: approaches being compared
- Cell values: metrics, with appropriate color coding
- Status chips (optional): classification per item per approach
- Footnotes: caveats on methodology or data differences between approaches

## Structure

```
[Grouped column headers — approach names]
[Sub-headers — metric names within each approach]
[Row: entity | approach A metrics | approach B metrics | approach C metrics]
[Footnote row or paragraph]
```

## Highlighted Approach

The primary or recommended approach column should be visually distinguished:
- Light accent background (`var(--accent-light)` or similar)
- A visual separator (thicker left border or column group border)
- The column header should name the approach, not just the metric

Do not over-highlight — only one column group needs the accent treatment.

## CSS Class Naming

```
.compare-table      — the <table> element
.compare-highlight  — applied to <td> and <th> cells in the highlighted column group
.compare-group-head — the top-level grouped column header (<th colspan="N">)
th.num, td.num      — right-aligned numeric cells
td.mono             — monospace text for rule strings and codes
td.dim              — dimmed text for secondary metadata
```

## Accessibility Rules

- Use `<thead>` with two rows: group headers (`colspan`) in row 1, metric headers in row 2.
- Use `scope="col"` on all `<th>` elements.
- Use `scope="row"` on the entity column.
- Group headers use `colspan` — do not create empty cells to span columns.
- Footnotes appear after the table in a `<p>` with small text styling.

## Common Mistakes

- Mixing too many metrics per column group — limit to 3–4 metrics per approach column; move details to appendix.
- Highlighting multiple approaches equally — only one should be the primary.
- Omitting the raw baseline as a reference column — if the goal is to show lift, include what the lift is relative to.
- Using different metric definitions across column groups without a footnote.
- Putting the comparison table in the appendix when it is the primary evidence for the recommendation.

## Copy-Paste CSS

```css
/* ── Comparison table ──────────────────────────────────────────────── */
.compare-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 13px;
}

.compare-table thead th {
  background: var(--surface-alt);
  padding: 8px 10px;
  font-size: 11px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.04em;
  color: var(--text-secondary);
  border-bottom: 1px solid var(--border);
  text-align: left;
  white-space: nowrap;
}

.compare-table thead th.num { text-align: right; }

/* Highlighted approach column group */
.compare-table .compare-highlight {
  background: #f0f5ff; /* accent-light tint */
}

.compare-table thead th.compare-highlight {
  background: #e8edfc;
  color: var(--accent);
  border-bottom-color: var(--accent);
}

.compare-table tbody tr { border-bottom: 1px solid var(--border); }
.compare-table tbody tr:last-child { border-bottom: none; }
.compare-table tbody tr:hover { background: var(--surface-alt); }

.compare-table tbody td {
  padding: 8px 10px;
  color: var(--text);
  vertical-align: middle;
}

.compare-table tbody td.num {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

.compare-table tbody td.mono {
  font-family: var(--font-mono);
  font-size: 11px;
  color: var(--text-secondary);
  max-width: 200px;
  word-break: break-word;
}

.compare-table tbody td.dim {
  color: var(--text-muted);
  font-size: 12px;
}

.compare-footnote {
  font-size: 11px;
  color: var(--text-muted);
  margin-top: 10px;
  line-height: 1.6;
}
```

## Copy-Paste HTML

Three-approach comparison: primary approach highlighted, two benchmarks.

```html
<div class="tbl-wrap" style="overflow-x:auto;">
  <table class="compare-table">
    <thead>
      <!-- Row 1: grouped approach labels -->
      <tr>
        <th rowspan="2" style="min-width:120px;">Group</th>
        <th rowspan="2" class="num">Raw WR</th>
        <!-- Primary approach — highlighted -->
        <th colspan="3"
            class="compare-highlight"
            style="text-align:center; border-bottom:2px solid var(--accent);">
          Primary Approach
        </th>
        <!-- Benchmark A -->
        <th colspan="3"
            style="text-align:center;">
          Benchmark A
        </th>
        <!-- Benchmark B -->
        <th colspan="2"
            style="text-align:center;">
          Benchmark B
        </th>
      </tr>
      <!-- Row 2: per-approach metric headers -->
      <tr>
        <!-- Primary approach metrics -->
        <th class="num compare-highlight">Rows</th>
        <th class="num compare-highlight">WR</th>
        <th class="compare-highlight">Rule</th>
        <!-- Benchmark A metrics -->
        <th class="num">Rows</th>
        <th class="num">WR</th>
        <th>Rule</th>
        <!-- Benchmark B metrics -->
        <th class="num">Rows</th>
        <th class="num">WR</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="font-weight:700;">Group A</td>
        <td class="num">
          <span class="metric-cell metric-weak">48.6%</span>
        </td>
        <!-- Primary approach -->
        <td class="num compare-highlight">1,258</td>
        <td class="num compare-highlight">
          <span class="metric-cell metric-ok">51.7%</span>
        </td>
        <td class="mono compare-highlight">model_score top 10%</td>
        <!-- Benchmark A -->
        <td class="num">2,044</td>
        <td class="num"><span class="metric-cell metric-ok">52.2%</span></td>
        <td class="mono dim">line ≤ 13.5 and price ≤ −120</td>
        <!-- Benchmark B -->
        <td class="num">297</td>
        <td class="num"><span class="metric-cell metric-strong">55.2%</span></td>
      </tr>
      <tr>
        <td style="font-weight:700;">Group B</td>
        <td class="num"><span class="metric-cell metric-ok">51.4%</span></td>
        <td class="num compare-highlight">10,057</td>
        <td class="num compare-highlight">
          <span class="metric-cell metric-ok">52.0%</span>
        </td>
        <td class="mono compare-highlight">model_score top 80%</td>
        <td class="num">8,110</td>
        <td class="num"><span class="metric-cell metric-ok">52.6%</span></td>
        <td class="mono dim">price ≤ −110</td>
        <td class="num">8,110</td>
        <td class="num"><span class="metric-cell metric-ok">52.6%</span></td>
      </tr>
    </tbody>
  </table>
</div>

<p class="compare-footnote">
  Primary approach uses no odds filter in selection — basketball features only.
  Benchmark A uses line and price thresholds as the selector.
  Benchmark B uses price as the sole selector. Raw WR uses the full unfiltered pool.
</p>
```

## Related Parent Files

- `components/metric-color-cell.md` — for cell-level metric coloring
- `components/status-chips.md` — for entity-level status classification in rows
- `../../workflow/design-preflight.md` — Step 7 (driver section uses comparison tables)
