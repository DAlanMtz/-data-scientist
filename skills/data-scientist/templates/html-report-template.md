# HTML Report Template

Use an HTML report when the deliverable needs polished layout, browser review, print/PDF export, shareable static output, or richer styling than markdown. Keep it dependency-free unless the user explicitly wants charting libraries, embedded assets, or interactivity.

Use markdown instead when the report is primarily a draft, notebook companion, or lightweight technical note.

## How To Use

1. Replace bracketed placeholders.
2. Insert chart images, SVGs, tables, or embedded static output into the chart containers.
3. Keep the executive summary short.
4. Use chart titles as takeaways.
5. Open in a browser and export to PDF with print backgrounds enabled.

## Copy-Paste HTML Skeleton

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>[Report Title]</title>
  <style>
    :root {
      --font-sans: Arial, Helvetica, sans-serif;
      --color-text: #1f2933;
      --color-muted: #64748b;
      --color-border: #d9e2ec;
      --color-surface: #ffffff;
      --color-background: #f6f8fb;
      --color-primary: #1f6feb;
      --color-positive: #16833a;
      --color-warning: #b7791f;
      --color-negative: #c62828;
      --space-xs: 4px;
      --space-sm: 8px;
      --space-md: 16px;
      --space-lg: 24px;
      --space-xl: 36px;
      --radius: 8px;
      --max-width: 1120px;
    }

    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: var(--font-sans);
      color: var(--color-text);
      background: var(--color-background);
      line-height: 1.5;
    }

    .page {
      max-width: var(--max-width);
      margin: 0 auto;
      padding: var(--space-xl) var(--space-lg);
    }

    header {
      margin-bottom: var(--space-xl);
    }

    .eyebrow {
      color: var(--color-muted);
      font-size: 13px;
      text-transform: uppercase;
      letter-spacing: .04em;
      margin-bottom: var(--space-sm);
    }

    h1 {
      font-size: 34px;
      line-height: 1.15;
      margin: 0 0 var(--space-md);
    }

    h2 {
      font-size: 22px;
      margin: var(--space-xl) 0 var(--space-md);
    }

    h3 {
      font-size: 17px;
      margin: 0 0 var(--space-sm);
    }

    p {
      margin: 0 0 var(--space-md);
    }

    .meta {
      color: var(--color-muted);
      font-size: 14px;
    }

    .summary {
      background: var(--color-surface);
      border: 1px solid var(--color-border);
      border-radius: var(--radius);
      padding: var(--space-lg);
      margin-bottom: var(--space-lg);
    }

    .kpi-grid {
      display: grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: var(--space-md);
      margin-bottom: var(--space-lg);
    }

    .kpi {
      background: var(--color-surface);
      border: 1px solid var(--color-border);
      border-radius: var(--radius);
      padding: var(--space-md);
    }

    .kpi-label {
      color: var(--color-muted);
      font-size: 13px;
      margin-bottom: var(--space-xs);
    }

    .kpi-value {
      font-size: 28px;
      font-weight: 700;
      margin-bottom: var(--space-xs);
    }

    .kpi-note {
      color: var(--color-muted);
      font-size: 13px;
    }

    .section {
      background: var(--color-surface);
      border: 1px solid var(--color-border);
      border-radius: var(--radius);
      padding: var(--space-lg);
      margin-bottom: var(--space-lg);
    }

    .chart-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: var(--space-lg);
    }

    .chart {
      border: 1px solid var(--color-border);
      border-radius: var(--radius);
      padding: var(--space-md);
      background: #fff;
    }

    .chart-title {
      font-weight: 700;
      margin-bottom: var(--space-xs);
    }

    .chart-subtitle,
    .caption {
      color: var(--color-muted);
      font-size: 13px;
    }

    .chart-placeholder {
      min-height: 260px;
      border: 1px dashed var(--color-border);
      border-radius: var(--radius);
      display: flex;
      align-items: center;
      justify-content: center;
      color: var(--color-muted);
      margin: var(--space-md) 0;
      text-align: center;
      padding: var(--space-md);
    }

    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 14px;
    }

    th,
    td {
      border-bottom: 1px solid var(--color-border);
      padding: 10px 8px;
      text-align: left;
      vertical-align: top;
    }

    th {
      color: var(--color-muted);
      font-weight: 700;
      background: #f8fafc;
    }

    .status-positive { color: var(--color-positive); font-weight: 700; }
    .status-warning { color: var(--color-warning); font-weight: 700; }
    .status-negative { color: var(--color-negative); font-weight: 700; }

    @media (max-width: 820px) {
      .kpi-grid,
      .chart-grid {
        grid-template-columns: 1fr;
      }

      .page {
        padding: var(--space-lg) var(--space-md);
      }
    }

    @media print {
      body {
        background: #fff;
      }

      .page {
        max-width: none;
        padding: 0;
      }

      .section,
      .summary,
      .kpi,
      .chart {
        break-inside: avoid;
        border-color: #cbd5e1;
      }

      a {
        color: inherit;
        text-decoration: none;
      }
    }
  </style>
</head>
<body>
  <main class="page">
    <header>
      <div class="eyebrow">[Audience] • [Report date]</div>
      <h1>[Takeaway-Oriented Report Title]</h1>
      <p class="meta">Decision supported: [Decision] • Data freshness: [Latest data timestamp]</p>
    </header>

    <section class="summary" aria-labelledby="executive-summary">
      <h2 id="executive-summary">Executive Summary</h2>
      <p><strong>Recommendation:</strong> [Recommended action and expected impact.]</p>
      <p><strong>Evidence:</strong> [One to three evidence points.]</p>
      <p><strong>Caveat:</strong> [Most decision-relevant limitation or uncertainty.]</p>
    </section>

    <section aria-labelledby="key-metrics">
      <h2 id="key-metrics">Key Metrics</h2>
      <div class="kpi-grid">
        <article class="kpi">
          <div class="kpi-label">[Metric name]</div>
          <div class="kpi-value">[Value]</div>
          <div class="kpi-note">[Change vs target/baseline]</div>
        </article>
        <article class="kpi">
          <div class="kpi-label">[Metric name]</div>
          <div class="kpi-value">[Value]</div>
          <div class="kpi-note">[Change vs target/baseline]</div>
        </article>
        <article class="kpi">
          <div class="kpi-label">[Metric name]</div>
          <div class="kpi-value">[Value]</div>
          <div class="kpi-note">[Change vs target/baseline]</div>
        </article>
        <article class="kpi">
          <div class="kpi-label">[Metric name]</div>
          <div class="kpi-value">[Value]</div>
          <div class="kpi-note">[Change vs target/baseline]</div>
        </article>
      </div>
    </section>

    <section class="section" aria-labelledby="visual-story">
      <h2 id="visual-story">Visual Story</h2>
      <div class="chart-grid">
        <article class="chart">
          <div class="chart-title">[Insight title, not chart type]</div>
          <div class="chart-subtitle">[Metric, population, time window, filters]</div>
          <div class="chart-placeholder">Insert chart image, SVG, table, or embedded static visual here.</div>
          <p class="caption">[Caption as takeaway: implication, caveat, next action.]</p>
        </article>
        <article class="chart">
          <div class="chart-title">[Insight title, not chart type]</div>
          <div class="chart-subtitle">[Metric, population, time window, filters]</div>
          <div class="chart-placeholder">Insert chart image, SVG, table, or embedded static visual here.</div>
          <p class="caption">[Caption as takeaway: implication, caveat, next action.]</p>
        </article>
      </div>
    </section>

    <section class="section" aria-labelledby="findings">
      <h2 id="findings">Findings</h2>
      <table>
        <thead>
          <tr>
            <th>Finding</th>
            <th>Evidence</th>
            <th>Implication</th>
            <th>Confidence / caveat</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>[Finding]</td>
            <td>[Metric/chart/table]</td>
            <td>[Decision implication]</td>
            <td>[Uncertainty or limitation]</td>
          </tr>
        </tbody>
      </table>
    </section>

    <section class="section" aria-labelledby="limitations">
      <h2 id="limitations">Limitations</h2>
      <ul>
        <li>[Data coverage limitation]</li>
        <li>[Metric or method limitation]</li>
        <li>[Uncertainty or sample-size limitation]</li>
      </ul>
    </section>

    <section class="section" aria-labelledby="recommendations">
      <h2 id="recommendations">Recommendations</h2>
      <p><strong>Next action:</strong> [Specific owner, action, and timing.]</p>
      <p><strong>Measurement plan:</strong> [How impact will be checked.]</p>
    </section>
  </main>
</body>
</html>
```

## Exporting To PDF

- Open the HTML file in a browser.
- Use Print / Save as PDF.
- Enable background graphics if the browser disables them.
- Check page breaks, chart readability, and table overflow.
- Include data freshness and source notes in the exported file.

## Quality Checks

- [ ] The report title states the key takeaway or decision.
- [ ] KPI cards include comparison points.
- [ ] Every chart container has a takeaway caption.
- [ ] Limitations appear before the final recommendation when they affect action.
- [ ] Print/PDF output is readable.
- [ ] No external dependency is required unless intentionally added.

## Related References And Checklists

- `references/visual-report-design-system.md`
- `references/visual-storytelling-guide.md`
- `templates/visual-report-template.md`
- `checklists/visual-report-checklist.md`
