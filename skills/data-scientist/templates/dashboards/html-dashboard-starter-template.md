# HTML Dashboard Starter Template

Use this when the user asks for a self-contained dashboard prototype or static dashboard deliverable. The starter is dependency-free HTML/CSS. Add Plotly, Vega-Lite, Chart.js, static exported images, or generated SVGs only when the user chooses that implementation path.

## Copy-Paste Starter

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>[Dashboard Name]</title>
  <style>
    :root {
      --bg: #f6f8fb;
      --surface: #ffffff;
      --text: #1f2933;
      --muted: #64748b;
      --border: #d9e2ec;
      --primary: #1f6feb;
      --positive: #16833a;
      --warning: #b7791f;
      --negative: #c62828;
      --radius: 8px;
      --gap: 16px;
      --shadow: 0 1px 2px rgba(15, 23, 42, 0.08);
      --font: Arial, Helvetica, sans-serif;
    }

    * { box-sizing: border-box; }

    body {
      margin: 0;
      font-family: var(--font);
      color: var(--text);
      background: var(--bg);
      line-height: 1.45;
    }

    .shell {
      display: grid;
      grid-template-columns: 240px minmax(0, 1fr);
      min-height: 100vh;
    }

    aside {
      background: #111827;
      color: #f8fafc;
      padding: 24px 18px;
    }

    aside h1 {
      font-size: 18px;
      margin: 0 0 8px;
    }

    aside p,
    aside li {
      color: #cbd5e1;
      font-size: 13px;
    }

    main {
      padding: 24px;
      max-width: 1440px;
      width: 100%;
    }

    .topbar {
      display: flex;
      justify-content: space-between;
      gap: var(--gap);
      align-items: flex-start;
      margin-bottom: 18px;
    }

    .title h2 {
      font-size: 26px;
      margin: 0 0 4px;
    }

    .muted {
      color: var(--muted);
      font-size: 13px;
    }

    .freshness {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 10px 12px;
      box-shadow: var(--shadow);
      white-space: nowrap;
    }

    .filters {
      display: grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: var(--gap);
      margin-bottom: 18px;
    }

    .filter {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 10px 12px;
      box-shadow: var(--shadow);
    }

    .filter label {
      display: block;
      color: var(--muted);
      font-size: 12px;
      margin-bottom: 4px;
    }

    .kpis {
      display: grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: var(--gap);
      margin-bottom: 18px;
    }

    .card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      padding: 16px;
    }

    .kpi-label {
      color: var(--muted);
      font-size: 13px;
      margin-bottom: 6px;
    }

    .kpi-value {
      font-size: 28px;
      font-weight: 700;
      margin-bottom: 4px;
    }

    .badge {
      display: inline-block;
      border-radius: 999px;
      padding: 3px 8px;
      font-size: 12px;
      font-weight: 700;
      background: #eef2ff;
      color: var(--primary);
    }

    .positive { color: var(--positive); }
    .warning { color: var(--warning); }
    .negative { color: var(--negative); }

    .grid {
      display: grid;
      grid-template-columns: 2fr 1fr;
      gap: var(--gap);
      margin-bottom: 18px;
    }

    .chart-title {
      font-weight: 700;
      margin-bottom: 4px;
    }

    .chart-subtitle {
      color: var(--muted);
      font-size: 13px;
      margin-bottom: 12px;
    }

    .chart-placeholder {
      min-height: 260px;
      border: 1px dashed var(--border);
      border-radius: var(--radius);
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      color: var(--muted);
      padding: 16px;
      background: #fbfdff;
    }

    .insights {
      display: grid;
      gap: var(--gap);
    }

    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 14px;
    }

    th, td {
      padding: 10px 8px;
      border-bottom: 1px solid var(--border);
      text-align: left;
    }

    th {
      color: var(--muted);
      background: #f8fafc;
      font-weight: 700;
    }

    footer {
      color: var(--muted);
      font-size: 12px;
      margin-top: 24px;
    }

    @media (max-width: 980px) {
      .shell { grid-template-columns: 1fr; }
      aside { display: none; }
      .filters, .kpis, .grid { grid-template-columns: 1fr; }
      .topbar { flex-direction: column; }
      main { padding: 16px; }
    }

    @media print {
      body { background: #fff; }
      aside, .filters { display: none; }
      .shell { display: block; }
      main { padding: 0; max-width: none; }
      .card { break-inside: avoid; box-shadow: none; }
    }
  </style>
</head>
<body>
  <div class="shell">
    <aside>
      <h1>[Dashboard Name]</h1>
      <p>[Purpose and decision supported.]</p>
      <ul>
        <li>[Primary decision]</li>
        <li>[Audience]</li>
        <li>[Refresh cadence]</li>
      </ul>
    </aside>

    <main>
      <section class="topbar">
        <div class="title">
          <h2>[Takeaway-Oriented Dashboard Title]</h2>
          <div class="muted">Decision supported: [decision] • Date range: [range]</div>
        </div>
        <div class="freshness">
          <strong>Freshness:</strong> [Last updated timestamp]<br>
          <span class="muted">Source: [source]</span>
        </div>
      </section>

      <section class="filters" aria-label="Dashboard filters">
        <div class="filter"><label>Date range</label>[Last 30 days]</div>
        <div class="filter"><label>Segment</label>[All segments]</div>
        <div class="filter"><label>Status</label>[All statuses]</div>
        <div class="filter"><label>Version</label>[Current]</div>
      </section>

      <section class="kpis" aria-label="Key performance indicators">
        <article class="card">
          <div class="kpi-label">[Primary KPI]</div>
          <div class="kpi-value">[Value]</div>
          <span class="badge positive">[Delta vs target]</span>
        </article>
        <article class="card">
          <div class="kpi-label">[Secondary KPI]</div>
          <div class="kpi-value">[Value]</div>
          <span class="badge warning">[Status]</span>
        </article>
        <article class="card">
          <div class="kpi-label">[Volume]</div>
          <div class="kpi-value">[Value]</div>
          <span class="badge">[Comparison]</span>
        </article>
        <article class="card">
          <div class="kpi-label">[Quality metric]</div>
          <div class="kpi-value">[Value]</div>
          <span class="badge negative">[Risk]</span>
        </article>
      </section>

      <section class="grid">
        <article class="card">
          <div class="chart-title">[Insight title for main trend]</div>
          <div class="chart-subtitle">[Metric, population, denominator, date range]</div>
          <div class="chart-placeholder">Replace with static chart image, SVG, Plotly/Vega-Lite/Chart.js mount point, or BI embed.</div>
        </article>
        <aside class="insights">
          <article class="card">
            <div class="chart-title">Key Insight</div>
            <p>[Takeaway, caveat, and next action.]</p>
          </article>
          <article class="card">
            <div class="chart-title">Recommendation</div>
            <p>[Action, owner, timing, and measurement plan.]</p>
          </article>
        </aside>
      </section>

      <section class="grid">
        <article class="card">
          <div class="chart-title">[Segment breakdown takeaway]</div>
          <div class="chart-subtitle">[Segment, metric, denominator]</div>
          <div class="chart-placeholder">Breakdown chart placeholder.</div>
        </article>
        <article class="card">
          <div class="chart-title">[Status / exception summary]</div>
          <div class="chart-subtitle">[Scope and status rules]</div>
          <div class="chart-placeholder">Status chart placeholder.</div>
        </article>
      </section>

      <section class="card">
        <div class="chart-title">Ranked Detail Table</div>
        <div class="chart-subtitle">Rows should reconcile to dashboard totals under active filters.</div>
        <table>
          <thead>
            <tr>
              <th>Entity</th>
              <th>Segment</th>
              <th>Metric</th>
              <th>Status</th>
              <th>Owner</th>
              <th>Next action</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>[Entity]</td>
              <td>[Segment]</td>
              <td>[Value]</td>
              <td><span class="badge warning">[Status]</span></td>
              <td>[Owner]</td>
              <td>[Action]</td>
            </tr>
          </tbody>
        </table>
      </section>

      <footer>
        Data freshness: [timestamp] • Definitions: [metric glossary location] • Caveats: [known limitations]
      </footer>
    </main>
  </div>
</body>
</html>
```

## Replacement Notes

- Static reports: replace placeholders with exported PNG/SVG charts.
- HTML prototypes: mount generated SVGs or simple inline tables.
- Plotly, Vega-Lite, Chart.js: add script tags only when the user wants interactive charts.
- BI tools: translate sections into pages, cards, visuals, filters, and tooltips.
- Streamlit/Shiny: map KPI cards to metrics/value boxes, chart cards to plot outputs, detail table to dataframe/DT.

## QA Checks

- [ ] The first screen answers the dashboard decision.
- [ ] KPI cards include target/baseline and date range.
- [ ] Filter defaults are visible.
- [ ] Chart titles state takeaways.
- [ ] Detail rows reconcile to summary metrics.
- [ ] Print view is readable.
