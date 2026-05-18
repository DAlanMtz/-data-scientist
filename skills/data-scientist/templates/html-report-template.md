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

The CSS below uses the canonical design tokens from `references/visual-report-design-system.md`. The report layout is intentionally narrower than a dashboard (860px max content width) to feel like a published document rather than a BI tool.

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>[Report Title]</title>
  <style>
    /* ── Design tokens ────────────────────────────────────────── */
    /* CSS tokens below follow the executive-editorial design system (default for
       stakeholder reports). To change visual direction, replace token values with
       those from design-systems/<name>/DESIGN.md — see design-systems/README.md. */
    :root {
      /* Typography */
      --font: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI",
              "Helvetica Neue", Arial, sans-serif;
      --font-mono: "SFMono-Regular", "Cascadia Mono", Menlo, Consolas,
                   "Liberation Mono", monospace;

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

      /* Layout */
      --radius:        6px;
      --shadow-sm:     0 1px 3px rgba(17, 20, 26, 0.07);
      --content-width: 860px;   /* narrower = editorial feel */
      --page-pad:      48px;
    }

    /* ── Reset ────────────────────────────────────────────────── */
    *, *::before, *::after { box-sizing: border-box; }
    img, svg { display: block; max-width: 100%; }

    /* ── Base ─────────────────────────────────────────────────── */
    body {
      margin: 0;
      font-family: var(--font);
      font-size: 15px;
      line-height: 1.65;
      color: var(--text);
      background: var(--bg);
      -webkit-font-smoothing: antialiased;
    }

    /* ── Page shell ───────────────────────────────────────────── */
    .page {
      max-width: var(--content-width);
      margin: 0 auto;
      padding: 56px var(--page-pad) 80px;
    }

    /* ── Header ───────────────────────────────────────────────── */
    header {
      padding-bottom: 32px;
      border-bottom: 2px solid var(--text);     /* strong top anchor line */
      margin-bottom: 40px;
    }

    .eyebrow {
      font-size: 12px;
      font-weight: 500;
      text-transform: uppercase;
      letter-spacing: 0.07em;
      color: var(--text-muted);
      margin-bottom: 12px;
    }

    h1 {
      font-size: 34px;
      font-weight: 700;
      line-height: 1.15;
      letter-spacing: -0.01em;
      color: var(--text);
      margin: 0 0 16px;
    }

    .meta {
      font-size: 13px;
      color: var(--text-muted);
      line-height: 1.5;
    }

    /* ── Section headings ─────────────────────────────────────── */
    h2 {
      font-size: 22px;
      font-weight: 700;
      line-height: 1.3;
      color: var(--text);
      margin: 56px 0 16px;   /* more space above than below */
    }

    h3 {
      font-size: 17px;
      font-weight: 600;
      line-height: 1.4;
      color: var(--text);
      margin: 0 0 8px;
    }

    p { margin: 0 0 16px; }
    ul, ol { margin: 0 0 16px; padding-left: 20px; }
    li { margin-bottom: 6px; }

    /* ── Summary / callout block ──────────────────────────────── */
    .summary {
      background: var(--accent-light);
      border-left: 3px solid var(--accent);
      border-radius: 0 var(--radius) var(--radius) 0;
      padding: 20px 24px;
      margin-bottom: 40px;
    }

    .summary h2 {
      margin: 0 0 12px;
      font-size: 17px;
    }

    /* ── KPI strip ────────────────────────────────────────────── */
    .kpi-grid {
      display: grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: 16px;
      margin-bottom: 40px;
    }

    .kpi {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 16px 18px;
      box-shadow: var(--shadow-sm);
    }

    .kpi-label {
      font-size: 12px;
      font-weight: 500;
      text-transform: uppercase;
      letter-spacing: 0.05em;
      color: var(--text-muted);
      margin-bottom: 6px;
    }

    .kpi-value {
      font-size: 30px;
      font-weight: 700;
      line-height: 1.1;
      color: var(--text);
      margin-bottom: 4px;
    }

    .kpi-delta {
      font-size: 13px;
      color: var(--text-muted);
    }

    .kpi-delta.up   { color: var(--positive); }
    .kpi-delta.down { color: var(--negative); }
    .kpi-delta.warn { color: var(--warning); }

    /* ── Section card ─────────────────────────────────────────── */
    .section {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 24px;
      margin-bottom: 24px;
      box-shadow: var(--shadow-sm);
    }

    .section h2 { margin-top: 0; }

    /* ── Chart containers ─────────────────────────────────────── */
    .chart-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 20px;
    }

    .chart {
      border-top: 2px solid var(--border);   /* top accent only — editorial style */
      padding-top: 14px;
    }

    .chart-title {
      font-size: 13px;
      font-weight: 700;
      color: var(--text);
      margin-bottom: 3px;
    }

    .chart-subtitle {
      font-size: 12px;
      color: var(--text-muted);
      margin-bottom: 12px;
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
      margin-bottom: 8px;
    }

    .caption {
      font-size: 12px;
      color: var(--text-muted);
      line-height: 1.5;
      margin-top: 6px;
    }

    /* ── Tables ───────────────────────────────────────────────── */
    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 14px;
    }

    th, td {
      padding: 10px 10px;
      border-bottom: 1px solid var(--border);
      text-align: left;
      vertical-align: top;
    }

    th {
      font-size: 12px;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.04em;
      color: var(--text-muted);
      background: var(--bg);
    }

    td:not(:first-child) { color: var(--text-secondary); }
    tr:last-child td { border-bottom: none; }

    /* ── Status utilities ─────────────────────────────────────── */
    .status-positive { color: var(--positive); font-weight: 600; }
    .status-warning  { color: var(--warning);  font-weight: 600; }
    .status-negative { color: var(--negative); font-weight: 600; }

    .tag {
      display: inline-block;
      border-radius: 4px;
      padding: 2px 8px;
      font-size: 12px;
      font-weight: 600;
    }

    .tag-positive { background: var(--positive-bg); color: var(--positive); }
    .tag-warning  { background: var(--warning-bg);  color: var(--warning); }
    .tag-negative { background: var(--negative-bg); color: var(--negative); }
    .tag-neutral  { background: var(--bg);          color: var(--text-secondary); }

    /* ── Divider ──────────────────────────────────────────────── */
    hr {
      border: none;
      border-top: 1px solid var(--border);
      margin: 40px 0;
    }

    /* ── Appendix ─────────────────────────────────────────────── */
    .appendix {
      border-top: 1px solid var(--border-strong);
      margin-top: 64px;
      padding-top: 32px;
    }

    .appendix h2 {
      font-size: 17px;
      margin-top: 0;
      color: var(--text-secondary);
    }

    .appendix p, .appendix li {
      font-size: 13px;
      color: var(--text-secondary);
    }

    /* ── Responsive ───────────────────────────────────────────── */
    @media (max-width: 760px) {
      :root { --page-pad: 20px; }
      .kpi-grid, .chart-grid { grid-template-columns: 1fr; }
      h1 { font-size: 26px; }
    }

    /* ── Print / PDF ──────────────────────────────────────────── */
    @media print {
      :root { --bg: #fff; }
      body { background: #fff; font-size: 13px; }

      .page { max-width: none; padding: 0; }

      .section, .kpi, .summary { break-inside: avoid; box-shadow: none; }

      .chart-placeholder {
        background: #f9f9f9;
        border-style: solid;
        min-height: 180px;
      }

      a { color: inherit; text-decoration: none; }

      h2 { page-break-after: avoid; }
    }
  </style>
</head>
<body>
  <main class="page">

    <!-- ── Header ─────────────────────────────────────────────── -->
    <header>
      <div class="eyebrow">[Audience] · [Report date] · [Status: Draft / Final]</div>
      <h1>[Takeaway-Oriented Report Title]</h1>
      <p class="meta">
        Decision supported: [Decision] &nbsp;·&nbsp;
        Data freshness: [Latest data timestamp] &nbsp;·&nbsp;
        Owner: [Name]
      </p>
    </header>

    <!-- ── Executive summary ──────────────────────────────────── -->
    <section class="summary" aria-labelledby="exec-summary">
      <h2 id="exec-summary">Summary</h2>
      <p><strong>Recommendation:</strong> [Recommended action and expected impact.]</p>
      <p><strong>Evidence:</strong> [One to three evidence points.]</p>
      <p><strong>Caveat:</strong> [Most decision-relevant limitation or uncertainty.]</p>
    </section>

    <!-- ── KPI strip ───────────────────────────────────────────── -->
    <section aria-label="Key metrics">
      <div class="kpi-grid">
        <article class="kpi">
          <div class="kpi-label">[Metric name]</div>
          <div class="kpi-value">[Value]</div>
          <div class="kpi-delta up">↑ [Change] vs [baseline/target]</div>
        </article>
        <article class="kpi">
          <div class="kpi-label">[Metric name]</div>
          <div class="kpi-value">[Value]</div>
          <div class="kpi-delta down">↓ [Change] vs [baseline/target]</div>
        </article>
        <article class="kpi">
          <div class="kpi-label">[Metric name]</div>
          <div class="kpi-value">[Value]</div>
          <div class="kpi-delta">[Comparison]</div>
        </article>
        <article class="kpi">
          <div class="kpi-label">[Metric name]</div>
          <div class="kpi-value">[Value]</div>
          <div class="kpi-delta warn">⚠ [Risk / threshold note]</div>
        </article>
      </div>
    </section>

    <!-- ── Visual story ────────────────────────────────────────── -->
    <section class="section" aria-labelledby="visual-story">
      <h2 id="visual-story">Visual Story</h2>
      <div class="chart-grid">
        <article class="chart">
          <div class="chart-title">[Finding, not chart type]</div>
          <div class="chart-subtitle">[Metric · Population · Time window · Filters]</div>
          <div class="chart-placeholder">Insert chart image, SVG, or embedded output.</div>
          <p class="caption">[Takeaway: what changed, for whom, what it means, caveat.]</p>
        </article>
        <article class="chart">
          <div class="chart-title">[Finding, not chart type]</div>
          <div class="chart-subtitle">[Metric · Population · Time window · Filters]</div>
          <div class="chart-placeholder">Insert chart image, SVG, or embedded output.</div>
          <p class="caption">[Takeaway: what changed, for whom, what it means, caveat.]</p>
        </article>
      </div>
    </section>

    <!-- ── Findings table ──────────────────────────────────────── -->
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
            <td>[Finding headline]</td>
            <td>[Metric, chart, or table reference]</td>
            <td>[Decision implication]</td>
            <td>[Uncertainty, limitation, or sample note]</td>
          </tr>
        </tbody>
      </table>
    </section>

    <!-- ── Limitations ─────────────────────────────────────────── -->
    <section class="section" aria-labelledby="limitations">
      <h2 id="limitations">Limitations</h2>
      <ul>
        <li>[Data coverage or freshness limitation]</li>
        <li>[Metric or method limitation]</li>
        <li>[Uncertainty or sample-size limitation]</li>
      </ul>
    </section>

    <!-- ── Recommendations ─────────────────────────────────────── -->
    <section class="section" aria-labelledby="recommendations">
      <h2 id="recommendations">Recommendations</h2>
      <p><strong>Next action:</strong> [Owner · Action · Timing]</p>
      <p><strong>Expected impact:</strong> [Quantified or directional estimate]</p>
      <p><strong>Measurement plan:</strong> [How and when to evaluate impact]</p>
    </section>

    <!-- ── Appendix ────────────────────────────────────────────── -->
    <aside class="appendix" aria-labelledby="appendix">
      <h2 id="appendix">Appendix</h2>
      <p>[Data definitions, query logic, method details, sensitivity checks, full tables, and diagnostic visuals.]</p>
    </aside>

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

- `references/design-craft-guide.md` — craft principles, AI anti-patterns, typography, space, color discipline, chart polish
- `references/chart-style-system.md` — matplotlib/ggplot2 house style code and color palette constants
- `references/visual-report-design-system.md` — design token reference (hex values, type scale, spacing scale)
- `references/visual-storytelling-guide.md` — narrative structure, caption writing, decision-first sequencing
- `templates/visual-report-template.md` — markdown-first version of this report structure
- `checklists/visual-report-checklist.md` — publish-quality checks before sharing
