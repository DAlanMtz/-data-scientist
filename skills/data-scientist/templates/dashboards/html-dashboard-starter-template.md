# HTML Dashboard Starter Template

Use this when the user asks for a self-contained dashboard prototype or static dashboard deliverable. The starter is dependency-free HTML/CSS. Add Plotly, Vega-Lite, Chart.js, static exported images, or generated SVGs only when the user chooses that implementation path.

## Copy-Paste Starter

The CSS below uses the canonical design tokens from `references/visual-report-design-system.md`. The dark sidebar uses `#16181d` (near-black, not pure black) and the main area uses the warm off-white page background. Replace with the user's brand colors when available.

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>[Dashboard Name]</title>
  <style>
    /* ── Design tokens ────────────────────────────────────────── */
    /* CSS tokens below follow the clean-saas-analytics design system (default).
       To change visual direction, replace token values with those from
       design-systems/<name>/DESIGN.md — see design-systems/README.md for the chooser. */
    :root {
      --font: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI",
              "Helvetica Neue", Arial, sans-serif;

      /* Surface */
      --bg:            #f7f8f9;
      --surface:       #ffffff;
      --border:        #e3e5e8;
      --border-strong: #c8cbd0;

      /* Text */
      --text:          #11141a;
      --text-secondary:#4a5060;
      --text-muted:    #848c9a;

      /* Accent */
      --accent:        #2952c4;
      --accent-light:  #e8edfc;

      /* Semantic */
      --positive:      #1d7d4c;
      --positive-bg:   #e8f7ee;
      --warning:       #a05c0a;
      --warning-bg:    #fef3e2;
      --negative:      #b72b2b;
      --negative-bg:   #fdeaea;

      /* Sidebar */
      --nav-bg:        #16181d;
      --nav-text:      #e8eaf0;
      --nav-muted:     #7a8090;
      --nav-active:    #2952c4;
      --nav-active-bg: rgba(41, 82, 196, 0.14);

      /* Layout */
      --radius:        6px;
      --shadow-sm:     0 1px 2px rgba(17, 20, 26, 0.07);
      --shadow:        0 2px 6px rgba(17, 20, 26, 0.09);
      --gap:           16px;
      --nav-width:     240px;
    }

    /* ── Reset ────────────────────────────────────────────────── */
    *, *::before, *::after { box-sizing: border-box; }
    img, svg { display: block; max-width: 100%; }

    /* ── Base ─────────────────────────────────────────────────── */
    body {
      margin: 0;
      font-family: var(--font);
      font-size: 14px;
      line-height: 1.5;
      color: var(--text);
      background: var(--bg);
      -webkit-font-smoothing: antialiased;
    }

    /* ── App shell ────────────────────────────────────────────── */
    .shell {
      display: grid;
      grid-template-columns: var(--nav-width) minmax(0, 1fr);
      min-height: 100vh;
    }

    /* ── Sidebar / nav ────────────────────────────────────────── */
    .nav {
      background: var(--nav-bg);
      padding: 0;
      display: flex;
      flex-direction: column;
      position: sticky;
      top: 0;
      height: 100vh;
      overflow-y: auto;
    }

    .nav-header {
      padding: 22px 18px 16px;
      border-bottom: 1px solid rgba(255,255,255,0.07);
    }

    .nav-header h1 {
      font-size: 15px;
      font-weight: 700;
      color: var(--nav-text);
      margin: 0 0 4px;
      letter-spacing: -0.01em;
    }

    .nav-header p {
      font-size: 12px;
      color: var(--nav-muted);
      margin: 0;
      line-height: 1.4;
    }

    .nav-section {
      padding: 16px 10px 8px;
    }

    .nav-label {
      font-size: 11px;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.07em;
      color: var(--nav-muted);
      padding: 0 8px;
      margin-bottom: 4px;
    }

    .nav-item {
      display: block;
      padding: 7px 8px;
      border-radius: var(--radius);
      color: var(--nav-text);
      font-size: 13px;
      text-decoration: none;
      margin-bottom: 1px;
      opacity: 0.8;
    }

    .nav-item.active {
      background: var(--nav-active-bg);
      color: #7ea8ff;
      opacity: 1;
      font-weight: 600;
    }

    .nav-footer {
      margin-top: auto;
      padding: 12px 18px 20px;
      font-size: 12px;
      color: var(--nav-muted);
      border-top: 1px solid rgba(255,255,255,0.07);
    }

    /* ── Main content ─────────────────────────────────────────── */
    main {
      padding: 24px 28px;
      max-width: 1440px;
      width: 100%;
      overflow-x: hidden;
    }

    /* ── Top bar ──────────────────────────────────────────────── */
    .topbar {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      gap: var(--gap);
      margin-bottom: 20px;
    }

    .topbar-title h2 {
      font-size: 22px;
      font-weight: 700;
      letter-spacing: -0.01em;
      margin: 0 0 4px;
      color: var(--text);
    }

    .topbar-meta {
      font-size: 13px;
      color: var(--text-muted);
    }

    .freshness-badge {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 8px 14px;
      box-shadow: var(--shadow-sm);
      white-space: nowrap;
      font-size: 13px;
    }

    .freshness-badge strong { color: var(--text); }

    /* ── Filters ──────────────────────────────────────────────── */
    .filters {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
      margin-bottom: 20px;
    }

    .filter-pill {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 20px;
      padding: 5px 14px;
      font-size: 13px;
      color: var(--text-secondary);
      cursor: pointer;
      white-space: nowrap;
    }

    .filter-pill.active {
      background: var(--accent-light);
      border-color: var(--accent);
      color: var(--accent);
      font-weight: 600;
    }

    /* ── KPI strip ────────────────────────────────────────────── */
    .kpis {
      display: grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: var(--gap);
      margin-bottom: 20px;
    }

    .card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      box-shadow: var(--shadow-sm);
      padding: 16px;
    }

    .kpi-label {
      font-size: 11px;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.06em;
      color: var(--text-muted);
      margin-bottom: 6px;
    }

    .kpi-value {
      font-size: 28px;
      font-weight: 700;
      line-height: 1.1;
      color: var(--text);
      margin-bottom: 6px;
    }

    .kpi-delta {
      font-size: 12px;
      color: var(--text-muted);
      display: flex;
      align-items: center;
      gap: 4px;
    }

    .kpi-delta.up   { color: var(--positive); }
    .kpi-delta.down { color: var(--negative); }
    .kpi-delta.warn { color: var(--warning); }

    /* ── Status chips ─────────────────────────────────────────── */
    .chip {
      display: inline-block;
      border-radius: 4px;
      padding: 2px 8px;
      font-size: 12px;
      font-weight: 600;
    }

    .chip-positive { background: var(--positive-bg); color: var(--positive); }
    .chip-warning  { background: var(--warning-bg);  color: var(--warning); }
    .chip-negative { background: var(--negative-bg); color: var(--negative); }
    .chip-neutral  { background: var(--bg); color: var(--text-secondary); border: 1px solid var(--border); }
    .chip-accent   { background: var(--accent-light); color: var(--accent); }

    /* ── Content grids ────────────────────────────────────────── */
    .grid-2-1 {
      display: grid;
      grid-template-columns: 2fr 1fr;
      gap: var(--gap);
      margin-bottom: var(--gap);
    }

    .grid-2 {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: var(--gap);
      margin-bottom: var(--gap);
    }

    .grid-3 {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: var(--gap);
      margin-bottom: var(--gap);
    }

    /* ── Chart cards ──────────────────────────────────────────── */
    .chart-title {
      font-size: 13px;
      font-weight: 700;
      color: var(--text);
      margin-bottom: 2px;
    }

    .chart-subtitle {
      font-size: 12px;
      color: var(--text-muted);
      margin-bottom: 12px;
      line-height: 1.4;
    }

    .chart-placeholder {
      min-height: 240px;
      border: 1px dashed var(--border);
      border-radius: var(--radius);
      background: #fafbfc;
      display: flex;
      align-items: center;
      justify-content: center;
      color: var(--text-muted);
      font-size: 13px;
      text-align: center;
      padding: 16px;
    }

    .caption {
      font-size: 12px;
      color: var(--text-muted);
      margin-top: 8px;
      line-height: 1.5;
    }

    /* ── Insight / narrative cards ────────────────────────────── */
    .insight-stack {
      display: grid;
      gap: var(--gap);
    }

    .insight-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-left: 3px solid var(--accent);
      border-radius: 0 var(--radius) var(--radius) 0;
      padding: 14px 16px;
      box-shadow: var(--shadow-sm);
    }

    .insight-card h3 {
      font-size: 13px;
      font-weight: 700;
      margin: 0 0 6px;
    }

    .insight-card p {
      font-size: 13px;
      color: var(--text-secondary);
      margin: 0;
      line-height: 1.5;
    }

    /* ── Tables ───────────────────────────────────────────────── */
    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 13px;
    }

    th, td {
      padding: 9px 10px;
      border-bottom: 1px solid var(--border);
      text-align: left;
      vertical-align: top;
    }

    th {
      font-size: 11px;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.04em;
      color: var(--text-muted);
      background: var(--bg);
    }

    tr:last-child td { border-bottom: none; }
    tr:hover td { background: #fafbfc; }

    /* ── Footer ───────────────────────────────────────────────── */
    .dash-footer {
      font-size: 12px;
      color: var(--text-muted);
      margin-top: 24px;
      padding-top: 16px;
      border-top: 1px solid var(--border);
    }

    /* ── Responsive ───────────────────────────────────────────── */
    @media (max-width: 1024px) {
      .kpis { grid-template-columns: repeat(2, 1fr); }
      .grid-2-1, .grid-3 { grid-template-columns: 1fr; }
    }

    @media (max-width: 800px) {
      .shell { grid-template-columns: 1fr; }
      .nav { display: none; }
      .kpis, .grid-2 { grid-template-columns: 1fr; }
      main { padding: 16px; }
      .topbar { flex-direction: column; }
    }

    /* ── Print ────────────────────────────────────────────────── */
    @media print {
      body { background: #fff; font-size: 12px; }
      .nav, .filters { display: none; }
      .shell { display: block; }
      main { padding: 0; max-width: none; }
      .card { break-inside: avoid; box-shadow: none; }
      .chip { border: 1px solid currentColor; }
    }
  </style>
</head>
<body>
  <div class="shell">

    <!-- ── Sidebar ─────────────────────────────────────────────── -->
    <nav class="nav" aria-label="Dashboard navigation">
      <div class="nav-header">
        <h1>[Dashboard Name]</h1>
        <p>[Decision supported and audience]</p>
      </div>

      <div class="nav-section">
        <div class="nav-label">Views</div>
        <a class="nav-item active" href="#">Overview</a>
        <a class="nav-item" href="#">Segments</a>
        <a class="nav-item" href="#">Diagnostics</a>
        <a class="nav-item" href="#">Detail</a>
      </div>

      <div class="nav-footer">
        Refresh: [cadence]<br>
        Owner: [name]
      </div>
    </nav>

    <!-- ── Main ───────────────────────────────────────────────── -->
    <main>

      <!-- Top bar -->
      <section class="topbar">
        <div class="topbar-title">
          <h2>[Takeaway-Oriented Dashboard Title]</h2>
          <div class="topbar-meta">Decision: [decision] · Range: [date range]</div>
        </div>
        <div class="freshness-badge">
          <strong>Updated:</strong> [timestamp]<br>
          <span style="color: var(--text-muted)">Source: [source]</span>
        </div>
      </section>

      <!-- Filters -->
      <section class="filters" aria-label="Active filters">
        <div class="filter-pill active">Last 30 days</div>
        <div class="filter-pill">All segments</div>
        <div class="filter-pill">All statuses</div>
        <div class="filter-pill">Current version</div>
      </section>

      <!-- KPI strip -->
      <section class="kpis" aria-label="Key performance indicators">
        <article class="card">
          <div class="kpi-label">[Primary KPI]</div>
          <div class="kpi-value">[Value]</div>
          <div class="kpi-delta up">↑ [Change] vs [target / prior period]</div>
        </article>
        <article class="card">
          <div class="kpi-label">[Secondary KPI]</div>
          <div class="kpi-value">[Value]</div>
          <div class="kpi-delta down">↓ [Change] vs [target / prior period]</div>
        </article>
        <article class="card">
          <div class="kpi-label">[Volume]</div>
          <div class="kpi-value">[Value]</div>
          <div class="kpi-delta">[Comparison]</div>
        </article>
        <article class="card">
          <div class="kpi-label">[Quality / risk metric]</div>
          <div class="kpi-value">[Value]</div>
          <div class="kpi-delta warn">⚠ [Threshold note]</div>
        </article>
      </section>

      <!-- Main trend + insight sidebar -->
      <section class="grid-2-1">
        <article class="card">
          <div class="chart-title">[Finding, not chart type — e.g., "Renewal rate improving but below target"]</div>
          <div class="chart-subtitle">[Metric · Population · Denominator · Date range]</div>
          <div class="chart-placeholder">Replace with static chart, SVG, Plotly/Vega-Lite mount, or BI embed.</div>
        </article>
        <div class="insight-stack">
          <article class="insight-card">
            <h3>Key Finding</h3>
            <p>[Takeaway: what changed, for whom, why it matters, caveat.]</p>
          </article>
          <article class="insight-card">
            <h3>Recommended Action</h3>
            <p>[Owner · Action · Timing · How impact will be measured.]</p>
          </article>
        </div>
      </section>

      <!-- Segment and status panels -->
      <section class="grid-2">
        <article class="card">
          <div class="chart-title">[Segment breakdown finding]</div>
          <div class="chart-subtitle">[Segment · Metric · Denominator]</div>
          <div class="chart-placeholder">Breakdown chart placeholder.</div>
          <p class="caption">[Caption: where the pattern is concentrated and what it means.]</p>
        </article>
        <article class="card">
          <div class="chart-title">[Exception / status summary finding]</div>
          <div class="chart-subtitle">[Scope, threshold, and status rules]</div>
          <div class="chart-placeholder">Status chart placeholder.</div>
          <p class="caption">[Caption: severity, distribution of alerts, recommended triage order.]</p>
        </article>
      </section>

      <!-- Detail table -->
      <section class="card">
        <div class="chart-title">Ranked Detail</div>
        <div class="chart-subtitle">Rows reconcile to summary KPIs under active filters. Sort by priority.</div>
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
              <td><span class="chip chip-warning">[Status]</span></td>
              <td>[Owner]</td>
              <td>[Action]</td>
            </tr>
          </tbody>
        </table>
      </section>

      <!-- Footer -->
      <footer class="dash-footer">
        Data freshness: [timestamp] · Definitions: [metric glossary] · Caveats: [known limitations]
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
