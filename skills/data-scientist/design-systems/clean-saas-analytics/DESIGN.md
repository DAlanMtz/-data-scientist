# Clean SaaS Analytics — Design System

> **Base relationship:** This system is the closest expression of the base visual system in `references/chart-style-system.md` and `references/visual-report-design-system.md`. All tokens match the base system.
> Tokens marked ★ intentionally differ from the base. Unmarked tokens follow the base system unless the surrounding guidance further constrains their use.

---

## Purpose

The default design system for analytics dashboards. Clean, functional, and legible across devices. Optimized for recurring internal dashboards, product metrics, and operational analysis where users return daily and need fast orientation rather than aesthetic impact.

---

## Best Use Cases

- General analytics and product metrics dashboards
- Recurring internal reporting (weekly/monthly business reviews)
- Multi-metric exploration dashboards
- Self-serve analytics tools and BI workspaces
- Notebook dashboards shared internally
- Any context where no other design system is explicitly required

---

## Avoid When

- The deliverable is a polished executive or board readout — use `executive-editorial` instead.
- The audience is non-technical and narrative context is essential — use `warm-narrative`.
- The dashboard monitors live infrastructure or incidents — use `operational-command-center`.
- The output is a printed or PDF-exported document — use `executive-editorial`.

---

## Visual Personality

Clean, functional, and neutral. The deep blue accent creates a professional anchor without competing with chart data. No decorative elements. Emphasis through hierarchy and white space, not color drama.

---

## Token Summary

| Token | Value | Override |
|---|---|---|
| `background` | `#f7f8f9` | |
| `surface` | `#ffffff` | |
| `surface_alt` | `#f0f2f5` | |
| `text_primary` | `#11141a` | |
| `text_secondary` | `#4a5060` | |
| `border` | `#e3e5e8` | |
| `chart_grid` | `#e3e5e8` | |
| `muted_fill` | `#d0d4da` | |
| `accent_primary` | `#2952c4` | |
| `accent_secondary` | `#e8edfc` | |
| `positive` | `#1d7d4c` | |
| `warning` | `#a05c0a` | |
| `negative` | `#b72b2b` | |
| `categorical_palette` | `#2952c4, #d4531c, #2a7f62, #7c3aac, #b5282f, #1a8fa8, #c07d2e, #9ba5b2` | |
| `sequential_palette` | `#e8edfc → #bed0f7 → #8aaee8 → #5082d0 → #2952c4` | |
| `diverging_palette` | `#b72b2b → #e8a0a0 → #f5f6f7 → #9ab8e8 → #2952c4` | |
| `font_stack` | `system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", "Helvetica Neue", Arial, sans-serif` | |
| `type_scale` | `11px / 13px / 15px / 18px / 24px / 32px` | |
| `spacing_scale` | `4 / 8 / 12 / 16 / 24 / 32 / 40 / 48 px` | |
| `radius` | `6px` | |
| `shadow` | `0 1px 3px rgba(0,0,0,0.08)` | |

---

## Typography

- **Font:** system-ui stack — renders as the OS native sans-serif (San Francisco on macOS/iOS, Segoe UI on Windows, Roboto on Android).
- **Heading contrast:** Size-led hierarchy. H1: 24px/700, H2: 18px/600, H3: 15px/600, body: 15px/400.
- **Label style:** Metric labels in 11–12px/500, uppercase, letter-spacing 0.04em. Use for KPI card labels and axis titles.
- **Chart text:** 12px for tick labels, 13px for axis titles and legends.

---

## Spacing and Density

- **Grid:** 8px baseline. All spacing values are multiples of 4px.
- **Card padding:** 16–24px.
- **KPI card height:** 80–100px.
- **Gap between cards:** 16px.
- **Section gap:** 32px.
- **Density:** Medium. Comfortable for daily use without feeling sparse.

---

## Card / Panel Style

- White surface on warm off-white background.
- 1px `border` (`#e3e5e8`) around cards.
- `radius: 6px`.
- `shadow: 0 1px 3px rgba(0,0,0,0.08)` for slight elevation.
- No decorative headers or gradient fills.
- Section headers: 11px/500 uppercase, `text_secondary`, letter-spacing 0.06em.

---

## Chart Style

- Apply `HOUSE_RCPARAMS` from `references/chart-style-system.md` — removes top/right spines, uses `chart_grid` (`#e3e5e8`) at 0.5px, system font.
- First series color: `accent_primary` (`#2952c4`).
- Multi-series: use `categorical_palette` in order.
- Inactive / zero-value fills: `muted_fill` (`#d0d4da`).
- No filled area under line charts unless showing a confidence interval.
- Annotations and reference lines: `text_secondary` with dashed stroke.
- Chart background: `surface` (`#ffffff`) or transparent on `background`.

---

## Table Style

- Header row: `surface_alt` (`#f0f2f5`), 13px/600.
- Alternating rows: white / `surface_alt`.
- Border: 1px `border` on header bottom; 1px `border` between rows.
- Right-align numeric columns; left-align text.
- Monospace font (`SFMono-Regular`, Menlo, Consolas) for numbers in dense tables.
- Positive delta: `positive` (`#1d7d4c`). Negative delta: `negative` (`#b72b2b`).

---

## KPI Style

- Value: 28–32px/700, `text_primary`.
- Label: 11px/500, uppercase, `text_secondary`, letter-spacing 0.06em.
- Delta/trend indicator: 13px/500. Arrow + numeric change. Color: `positive` or `negative`. Always include a text label alongside color.
- Sparkline (optional): thin 1px line in `accent_primary`, no fill.
- Target comparison: small secondary number in `text_secondary` below value.

---

## Semantic Color Rules

- `positive` (`#1d7d4c`) encodes a favorable metric state only — not general data presence or chart fills.
- `warning` (`#a05c0a`) encodes a metric approaching a threshold — not general annotation.
- `negative` (`#b72b2b`) encodes an unfavorable metric state or alert — not general emphasis.
- `accent_secondary` (`#e8edfc`) is for selected state, hover backgrounds, and filter chips — not status encoding.
- Never use `positive` / `negative` for categorical series. Use `categorical_palette` for multi-series data.
- All semantic colors must be paired with a text label or icon — never color alone for status.

---

## Dashboard Layout Rules

- Row 1: KPI strip (3–5 cards max). Include freshness indicator and active filter summary.
- Row 2: Primary decision visual — the chart that answers the main question.
- Row 3: Supporting trend or segment comparison.
- Row 4+: Diagnostic detail, drilldown tables, data quality indicators.
- Sidebar (if used): filter controls, navigation. Dark sidebar (`#16181d`) or light sidebar (`background`).
- Do not place more than 6 visuals on a single dashboard view without a secondary page or tab.

---

## Report Layout Rules

- This system is dashboard-primary. For reports, prefer `executive-editorial`.
- If used for a report: max content width 1040px. Section headers bold with bottom border in `border`.
- Executive summary block at top with `surface_alt` background and left `accent_primary` border.

---

## Caption / Title Tone

- Chart titles: takeaway-first. "Revenue declined 8% in Q3" not "Q3 Revenue."
- Captions: metric + time window + implication + caveat.
- Business language, not technical jargon.
- No exclamation marks. No hedging qualifiers in titles.

---

## Accessibility Rules

- Minimum contrast ratio: 4.5:1 for body text, 3:1 for large text and UI components.
- Status information must include a text label alongside color.
- Chart labels must be readable at 100% zoom without magnification.
- Grayscale-safe: all series distinguishable by shape/pattern in addition to color.
- Font size minimum: 11px for any visible label.

---

## Format-Specific Guidance

### Markdown Report

- Use `##` headings for sections, `###` for subsections.
- Bold metric values on first mention: `**8.3%**`.
- Use pipe tables for KPI summaries. Align numeric columns to the right using `---:`.
- Separate findings, observations, and recommendations into labeled sections.
- Captions: italicize caption text below a code block or image placeholder.

### HTML Report

- Apply `:root` tokens as CSS custom properties (see `templates/html-report-template.md`).
- No token overrides needed — the base template already uses this system.
- Content width: 860px. Add padding `0 24px` on smaller viewports.
- Print media query: chart backgrounds white, border reduced to 1px solid `#d0d4da`.

### HTML Dashboard

- Apply `:root` tokens (see `templates/dashboards/html-dashboard-starter-template.md`).
- No token overrides needed — the starter template already uses this system.
- Dashboard layout: CSS Grid or Flexbox. KPI strip: 3–5 equal-width cards. Charts: full-width or 50/50 grid.
- Sidebar: `#16181d` background, `#ffffff` text, `accent_primary` active state.

### Python / Matplotlib Charts

- Use `HOUSE_RCPARAMS` from `references/chart-style-system.md` without modification.
- First color: `#2952c4`. Multi-series: `CHART_COLORS` list in order.
- Figure background: `#ffffff` (surface). Axes background: `#ffffff`.
- Save with `savefig.dpi=220`, `bbox_inches='tight'`.

### R / ggplot2 Charts

- Use `theme_house()` from `references/chart-style-system.md` without modification.
- First color: `#2952c4`. Multi-series: `CHART_COLORS` vector in order.
- Background: `#ffffff`. Grid: `#e3e5e8` at 0.5pt.

### Excel / Sheets Dashboard

- Header fill: `#f0f2f5` (surface_alt). Header font: bold, `#11141a`.
- Accent/highlight cells: `#e8edfc` background, `#2952c4` bold text.
- Positive delta: `#1d7d4c` text. Negative delta: `#b72b2b` text.
- Borders: `#e3e5e8` thin lines between data rows. No heavy outer box borders.
- Named styles: `KPI_Value`, `KPI_Label`, `Row_Positive`, `Row_Negative`.

### BI Dashboard

- Canvas background: `#f7f8f9`. Card background: `#ffffff`. Card border: `#e3e5e8`.
- Title font: system sans-serif, 18px/600. Body: 14px/400.
- Accent: `#2952c4`. Tooltip background: `#11141a`, text: `#ffffff`.
- Legend position: top or right. Consistent spacing 16px between cards.

---

## Common Mistakes

- Using `accent_secondary` (`#e8edfc`) for positive status — it is a tint, not a semantic color.
- Adding decorative color fills to chart areas that convey no data meaning.
- Mixing this system's blue palette with arbitrary brand colors in the same deliverable.
- Using KPI cards for more than 5 metrics on the top row — creates visual noise.
- Omitting the freshness indicator from the dashboard header.
- Leaving chart titles as label-style ("Revenue by Month") instead of takeaway-style ("Revenue plateaued in Q3").
