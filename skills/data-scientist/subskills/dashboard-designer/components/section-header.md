# Section Header

## Purpose

A two-line block that opens every major dashboard section. The title states the finding. The meta line provides scope, caveat, or population context. This pattern forces every section to carry a purpose — viewers can scan section titles to read the dashboard's story without opening every panel.

## When to Use

Use a section header on every section card that contains a finding or conclusion. Do not use section headers on the verdict band, KPI strip, or collapsible appendix summaries — those have their own patterns.

## Structure

```
[eyebrow label — optional]
[Section title — the finding, stated as a declarative sentence]
[Section meta — population, date range, caveat, or metric scope]
```

| Element | Role | Example |
|---|---|---|
| Eyebrow | Optional category label in small caps above the title | "Stability Analysis" |
| Title | The finding — a declarative sentence answering "what does this show?" | "April weakness is concentrated in two segments" |
| Meta | Context: who, what period, what denominator, any caveat | "NBA-first selected pools · Oct 2025 – May 2026 · partial months excluded" |

## The Finding Test

Before writing a section title, ask: "If someone reads only this title, do they learn something?" 

- **Passes:** "UNDER families are stronger broad baselines — they clear 52% at high volume with fewer filters"
- **Fails:** "Monthly stability table"
- **Passes:** "Price concentration is a diagnostic risk in Points families — 62–66% of volume at one price bucket"  
- **Fails:** "Concentration analysis"
- **Passes:** "Rebounds OVER needs sample depth — the prior_game_count gate explains the retention drop to 23%"
- **Fails:** "Rebounds OVER details"

A title that could apply to any dashboard in the same domain has failed the test.

## Visual Rules

- Title: 13–15px, weight 700, `var(--text)`, line-height 1.35.
- Meta: 12px, `var(--text-muted)`, margin-top 3px.
- Eyebrow (if used): 10–11px, uppercase, letter-spaced, `var(--text-muted)`.
- Bottom margin between the header block and the content below: 12–16px.

## Accessibility Rules

- Use actual heading elements (`<h2>`, `<h3>`) for the title — not styled `<div>` elements.
- Maintain heading hierarchy within the page: the page `<h1>` → section `<h2>` → sub-section `<h3>`.
- The meta line uses `<p>` or a `<div>` — not another heading.

## Common Mistakes

- Writing the chart type as the title: "Win Rate by Month" → "Month instability is highest in April and May".
- Writing the metric name as the title: "Retention" → "Renewal cohorts are recovering but 3 regions remain below baseline".
- Omitting the meta line — without scope and population, the finding cannot be evaluated.
- Using more than two lines for the meta — keep it to one line with `·` separators; details go in section footnotes.
- Writing a title as a question: "Is performance improving?" — use declarative form: "Performance is improving in 4 of 6 segments but below target in 2".

## Copy-Paste CSS

```css
/* ── Section header ────────────────────────────────────────────────── */
.section-header {
  margin-bottom: 14px;
}

.section-eyebrow {
  font-size: 10px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.07em;
  color: var(--text-muted);
  margin-bottom: 4px;
}

.section-title {
  font-size: 14px;
  font-weight: 700;
  color: var(--text);
  line-height: 1.35;
  margin: 0;
}

.section-meta {
  font-size: 12px;
  color: var(--text-muted);
  margin-top: 3px;
  line-height: 1.4;
}
```

## Copy-Paste HTML

### With eyebrow

```html
<header class="section-header">
  <div class="section-eyebrow">Stability Analysis</div>
  <h2 class="section-title">April weakness is concentrated in two segments — all other months clear 52%</h2>
  <p class="section-meta">NBA-first selected pools · Oct 2025 – May 2026 · partial months (Oct, May) excluded from stability assessment</p>
</header>
```

### Without eyebrow (most common)

```html
<header class="section-header">
  <h2 class="section-title">UNDER families are stronger broad baselines — they clear 52% at high volume with fewer filters</h2>
  <p class="section-meta">All 6 NBA-first families · full season Oct 2025 – Apr 2026 · retention % relative to raw pool</p>
</header>
```

### Inside a section card

```html
<section class="section-card">
  <header class="section-header">
    <h2 class="section-title">Points OVER has 62% price concentration — the NBA score may be recreating a market filter</h2>
    <p class="section-meta">Stability and concentration diagnostics · nba_model_score top 10% pool · 1,258 rows</p>
  </header>
  <!-- chart, table, or heatmap content below -->
</section>
```

### Section card base CSS

```css
.section-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 20px 20px 18px;
  box-shadow: var(--shadow);
  margin-bottom: 16px;
}
```

## Related Parent Files

- `../../references/visual-storytelling-guide.md` — headline writing and decision-first sequencing
- `../../workflow/design-preflight.md` — Step 7 (chart sequence: context → status → driver → uncertainty → action)
- `../../references/design-craft-guide.md` — AI fingerprint anti-patterns
