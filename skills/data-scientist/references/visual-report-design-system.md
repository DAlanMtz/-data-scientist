# Visual Report Design System

Use this default design system for professional analytics reports, dashboards, and exported visual deliverables when the user has not supplied a brand system. Users can override fonts, colors, spacing, or examples with their own brand standards.

The design principle is decision-first: the layout should make the supported decision, strongest evidence, and recommended action easier to find than everything else.

For the craft layer — what makes output look AI-generated vs. professionally crafted — see `references/design-craft-guide.md`. For ready-to-paste Python and R chart style code, see `references/chart-style-system.md`.

The base token system defined here is the default for all dashboards and reports. For stronger visual direction, optional design system presets are available in `design-systems/`. Each preset is a complete, standalone token override — apply one in full or use this base system. If no design system is specified, this base system applies.

---

## Design Token Reference

These values define the default system. Apply them to HTML/CSS reports, notebooks, BI tools, and chart configurations. Override any token with the user's brand system.

### Typography

```
Font stack (HTML/CSS):
  system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", "Helvetica Neue", Arial, sans-serif

Font stack (monospace / data tables):
  "SFMono-Regular", "Cascadia Mono", Menlo, Consolas, "Liberation Mono", monospace

Charts (Python rcParams):
  font.sans-serif: ["Helvetica Neue", "Helvetica", "Arial", "DejaVu Sans"]
```

### Type scale

| Role | Size | Weight | Line height |
|---|---|---|---|
| Report title (h1) | 34px | 700 | 1.15 |
| Section heading (h2) | 22px | 700 | 1.3 |
| Subsection (h3) | 17px | 600 | 1.4 |
| Body text | 15px | 400 | 1.65 |
| Label / metric name | 13px | 500 | 1.4 |
| Caption / footnote | 12–13px | 400 | 1.5 |
| KPI value (large) | 30px | 700 | 1.1 |
| Chart axis label | 10–11px | 400 | — |
| Chart title | 13px | 700 | — |

### Spacing scale (8px grid)

| Token | Value | Use |
|---|---|---|
| sp-1 | 4px | Icon-text gap, micro spacing |
| sp-2 | 8px | Inside compact components |
| sp-3 | 12px | Card inner padding (compact) |
| sp-4 | 16px | Standard inner padding |
| sp-6 | 24px | Between related components |
| sp-8 | 32px | Between sections in a column |
| sp-10 | 40px | Section break (above h2) |
| sp-12 | 48px | Page horizontal margin |
| sp-16 | 64px | Between major report sections |

### Color tokens

```
─── Surface ────────────────────────────────────────────────────
--bg:             #f7f8f9   warm off-white page background
--surface:        #ffffff   card / section background
--border:         #e3e5e8   card edges, table borders, grid lines
--border-strong:  #c8cbd0   dividers between major sections

─── Text ───────────────────────────────────────────────────────
--text:           #11141a   primary text (near-black, slightly warm)
--text-secondary: #4a5060   secondary text, axis titles
--text-muted:     #848c9a   labels, captions, footnotes, tick text

─── Accent ─────────────────────────────────────────────────────
--accent:         #2952c4   primary highlight, links, selected state
--accent-light:   #e8edfc   accent tint for backgrounds

─── Semantic status ────────────────────────────────────────────
--positive:       #1d7d4c   favorable (forest green)
--positive-bg:    #e8f7ee
--warning:        #a05c0a   needs review (amber-brown)
--warning-bg:     #fef3e2
--negative:       #b72b2b   risk / alert (deep red)
--negative-bg:    #fdeaea

─── Reference ──────────────────────────────────────────────────
--reference:      #9ba5b2   baselines, averages, historical context
```

### Chart categorical sequence

Apply in order. Use the same color for the same category across all charts in the report.

| # | Hex | Name | When to use |
|---|---|---|---|
| 1 | `#2952c4` | Deep blue | Primary series, most important category |
| 2 | `#d4531c` | Burnt orange | Second series, contrast to blue |
| 3 | `#2a7f62` | Forest green | Third series |
| 4 | `#7c3aac` | Deep purple | Fourth series |
| 5 | `#b5282f` | Brick red | Fifth series |
| 6 | `#1a8fa8` | Teal | Sixth series |
| 7 | `#c07d2e` | Amber | Seventh series |
| 8 | `#9ba5b2` | Slate gray | Reference, baseline, historical context |

Never use the default matplotlib tab10, seaborn, or BI tool default palettes in stakeholder-facing output.

### Sequential palettes

For density, intensity, or single-metric heatmaps (light to dark):

- Blue: `#e8edfc → #adbdf0 → #7290e1 → #2952c4 → #1a347a`
- Gray: `#f4f5f6 → #d1d5db → #9ca3af → #6b7280 → #374151`
- Green: `#e3f7ed → #9ad9bb → #4db584 → #1d7d4c → #104d2f`

### Diverging palette

For two-sided data (above/below target, positive/negative change):

`#d4531c → #f2bfa6 → #f5f0ee → #b3c7ee → #2952c4`

---

## Design Priorities

- Put the decision and answer before supporting detail.
- Use hierarchy so the most important information is visually easiest to scan.
- Keep views simple: avoid decorative complexity, excess colors, and chart dumps.
- Group related metrics and repeat layout patterns consistently.
- Use captions as takeaways, not generic labels.
- Make uncertainty, filters, freshness, and limitations visible when they affect interpretation.

## Typography Hierarchy

Use a clear hierarchy even if the output is markdown, HTML, notebook, BI dashboard, slide deck, or spreadsheet. Apply the type scale from the Design Token Reference above.

- Report title: short, decision-relevant, largest text on the page. Use --text (near-black) at h1 size.
- Section heading: names the business question or decision area. Visually distinct from title; does not compete.
- Chart title: states the insight or question answered. Bold, 13px in charts.
- Chart subtitle: defines population, time window, metric, denominator, and filters. --text-muted.
- Caption/takeaway: explains why the viewer should care and what action may change. 12–13px, --text-muted.
- Footnote: method, caveat, source, or definition detail. 12px, --text-muted, below the main content.

Avoid using chart titles like "Revenue by Month" when a takeaway is available. Prefer "Revenue recovered after March outage but remains below Q4 baseline."

Use uppercase letter-spacing for eyebrow labels and small category labels (`text-transform: uppercase; letter-spacing: 0.06em`). Do not uppercase body text, headings, or captions.

## Spacing And Layout

- Use a predictable grid: one-column for narrative reports, two-column for comparison sections, dashboard grid for recurring monitoring.
- Keep related items close together: KPI card + trend + definition belong near each other.
- Leave enough whitespace around sections so findings do not visually blur together.
- Align chart edges, labels, and tables.
- Avoid nesting cards inside cards. Use section bands, headings, or dividers instead.
- Put filters, date ranges, and refresh status in a consistent location.

## Page Sections

Recommended report sequence:

1. Title, audience, decision supported, date, data freshness.
2. Executive visual summary: 1-3 visuals or KPI cards that answer the main question.
3. Key findings: ranked by decision importance.
4. Evidence sections: charts with captions and supporting tables.
5. Limitations and uncertainty.
6. Recommendation and next action.
7. Appendix: method, definitions, diagnostics, detailed tables.

Recommended dashboard sequence:

1. Header: dashboard purpose, refresh status, filters.
2. KPI strip: primary metrics, target/baseline, change over time.
3. Decision view: trend, segment, ranking, or funnel that drives action.
4. Diagnostic view: data quality, drilldowns, exceptions, model or metric health.
5. Detail table: exportable rows only when users need follow-up action.

## KPI Cards

A KPI card is useful only when the viewer needs a fast status read.

Include:

- Metric name in business language.
- Current value with unit.
- Comparison point: prior period, target, baseline, forecast, or threshold.
- Direction and magnitude of change.
- Freshness/date range.
- Small trend or status indicator when useful.

Avoid KPI cards with unexplained percentages, no denominator, no target, or inconsistent time windows.

## Chart Title, Subtitle, And Caption Format

Use this pattern:

- **Title:** takeaway or question answered.
- **Subtitle:** metric, population, time window, filters, denominator.
- **Caption:** implication, uncertainty, limitation, or next action.

Example:

- Title: "Renewal risk is concentrated in small accounts with falling usage"
- Subtitle: "Accounts up for renewal in next 90 days; usage change vs prior 30 days"
- Caption: "Prioritize outreach to accounts with usage down more than 25%; sample excludes accounts with incomplete telemetry."

## Table Design

Use tables for lookup, audit, detailed comparison, or action queues. Do not use tables when a chart would make the pattern obvious faster.

Rules:

- Put the most important columns first.
- Use plain names and units in headers.
- Align text left and numbers right.
- Use consistent decimal places.
- Sort by decision relevance by default.
- Include row counts, totals, or denominators when they matter.
- Use conditional formatting sparingly for status, thresholds, and exceptions.
- Freeze headers or repeat headers in long/exported tables.

## Color Usage Rules

- Use the design token color system above, not BI tool defaults or matplotlib tab10.
- Use `--text`, `--text-secondary`, and `--text-muted` for all text. Do not use pure black (`#000000`).
- Use `--bg` for page backgrounds and `--surface` for card/panel backgrounds.
- Use `--border` (`#e3e5e8`) for chart grid lines, card edges, and table borders.
- Reserve `--accent` (`#2952c4`) for the most important data element per chart. One accent per chart.
- Use the categorical sequence from the Design Token Reference. Apply colors in order, consistently.
- Keep categorical palettes at 6 categories or fewer before grouping into "Other."
- Do not change category colors between charts.
- Avoid rainbow palettes, decorative gradients, and heavily saturated colors.
- Use direct labels where legends become hard to scan.

## Semantic Color Rules

Use `--positive`, `--warning`, and `--negative` for status encoding only. Do not use green or red for non-status purposes.

- Green (`--positive: #1d7d4c`): favorable status, target met, improvement.
- Red (`--negative: #b72b2b`): risk, alert, target missed, harm, decline.
- Amber (`--warning: #a05c0a`): needs review, incomplete, approaching threshold.
- Blue (`--accent: #2952c4`): primary highlight, selected state, focus.
- Gray (`--reference: #9ba5b2`): baseline, inactive, missing, historical context.

Always pair semantic color with a text label, icon, or pattern. Do not rely on color alone.

## Accessibility And Contrast

- Use sufficient contrast for text, lines, markers, and status colors.
- Avoid relying on color alone.
- Use readable font sizes for the delivery medium.
- Keep axis labels and legends legible after export.
- Add alt text or written takeaways when exporting visuals into documents.
- Avoid tiny multiples that cannot be read on the target screen or paper size.

## Responsive Vs Print/Export

For responsive dashboards:

- Prioritize the KPI strip and main decision chart on smaller screens.
- Collapse secondary diagnostics below primary views.
- Avoid dense tables on mobile unless the workflow requires them.
- Test filter panels, legends, and tooltips at expected screen sizes.

For print or PDF:

- Use fixed page sections with clear breaks.
- Repeat key filters and date ranges on every page.
- Ensure charts remain readable in grayscale.
- Include source, refresh date, and definitions in footnotes or appendix.

## Common Design Mistakes

- Chart dump with no decision, hierarchy, or action.
- Titles describe chart type instead of insight.
- Too many colors, filters, tabs, or chart types.
- KPI cards lack target, baseline, denominator, or time window.
- Inconsistent metric definitions across pages.
- Tables are too wide, unsorted, or lack units.
- Dashboard hides freshness, filters, or data quality status.
- Exported visuals are unreadable outside the original tool.
- Decorative elements compete with findings.
- Important caveats are buried after the recommendation.
