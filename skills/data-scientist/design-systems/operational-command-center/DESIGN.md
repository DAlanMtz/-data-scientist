# Operational Command Center — Design System

> **Base relationship:** This system departs significantly from the base (`references/chart-style-system.md`) — it is a dark-mode, high-density system for monitoring and alerting contexts. Nearly all surface, text, and color tokens differ from the base.
> Tokens marked ★ intentionally differ from the base. Unmarked tokens follow the base system unless the surrounding guidance further constrains their use.

---

## Purpose

A dark-mode, high-density design system for operational dashboards: infrastructure monitoring, incident triage, alerting queues, and NOC/SRE workspaces. Designed for extended screen time in controlled lighting and fast information scanning.

---

## Best Use Cases

- Infrastructure and application monitoring dashboards
- Incident and alert triage consoles
- Network Operations Center (NOC) and SRE dashboards
- Live operational status boards
- Anomaly detection and exception monitoring queues

---

## Avoid When

- The audience is executives, board members, or non-technical stakeholders — use `executive-editorial`.
- The output is a report rather than a live dashboard.
- The context is academic or research — use `research-paper`.
- Users are not accustomed to dark terminal interfaces — the dense layout penalizes first-time readers.
- The dashboard is exploratory or used infrequently — dark high-density is fatiguing without training.

---

## Visual Personality

Dark, compact, and functional. Near-black backgrounds reduce eye strain in controlled environments. Electric blue primary accent creates clear focal points. Alert green is reserved strictly for favorable metric status. High information density — no wasted space.

---

## Token Summary

| Token | Value | Override |
|---|---|---|
| `background` | `#0d1117` | ★ |
| `surface` | `#161b22` | ★ |
| `surface_alt` | `#1c2128` | ★ |
| `text_primary` | `#e6edf3` | ★ |
| `text_secondary` | `#8b949e` | ★ |
| `border` | `#30363d` | ★ |
| `chart_grid` | `#21262d` | ★ |
| `muted_fill` | `#21262d` | ★ |
| `accent_primary` | `#388bfd` | ★ |
| `accent_secondary` | `#3fb950` | ★ |
| `positive` | `#3fb950` | ★ |
| `warning` | `#d29922` | ★ |
| `negative` | `#f85149` | ★ |
| `categorical_palette` | `#388bfd, #3fb950, #f78166, #d2a8ff, #ffa657, #79c0ff, #a5d6ff, #8b949e` | ★ |
| `sequential_palette` | `#0d1117 → #1e3a5a → #1d4e89 → #2970c4 → #388bfd` | ★ |
| `diverging_palette` | `#f85149 → #5a2020 → #21262d → #1a4228 → #3fb950` | ★ |
| `font_stack` | `system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", "Helvetica Neue", Arial, sans-serif` | |
| `type_scale` | `10px / 12px / 14px / 16px / 20px / 28px` | ★ |
| `spacing_scale` | `4 / 6 / 8 / 12 / 16 / 20 / 28 / 36 px` | ★ |
| `radius` | `4px` | ★ |
| `shadow` | `0 2px 8px rgba(0,0,0,0.4)` | ★ |

---

## Typography

- **Font:** system-ui stack. Do not use monospace for general labels — reserve monospace for metric values and IDs.
- **Heading contrast:** Size-led. H1: 20px/600, H2: 16px/600, H3: 14px/500. Dashboard titles are compact.
- **Status labels:** 10px/500, uppercase, letter-spacing 0.06em. Use for category badges and status chips.
- **Metric values in charts:** 12px. Tick labels: 10–11px, `text_secondary`.
- **Monospace values:** `"SFMono-Regular", "Cascadia Mono", Menlo, Consolas, monospace` for IDs, hashes, numeric metric cards.

---

## Spacing and Density

- **Grid:** 4px sub-grid. Spacing uses 4px increments.
- **Card padding:** 8–12px.
- **KPI card height:** 60–80px.
- **Gap between cards:** 8px.
- **Section gap:** 16–20px.
- **Density:** High. Every pixel has purpose. No decorative white space.

---

## Card / Panel Style

- Dark surface (`#161b22`) on near-black background (`#0d1117`).
- 1px `border` (`#30363d`).
- `radius: 4px`.
- `shadow: 0 2px 8px rgba(0,0,0,0.4)`.
- Alert/active card: 2px left border in `accent_primary` (`#388bfd`) or `negative` (`#f85149`) depending on severity.
- Section headers: 10px/500 uppercase, `text_secondary`, letter-spacing 0.08em.
- Status badge chips: inline, 10px/500, uppercase. Colors: `positive`, `warning`, `negative`, or `accent_primary`. Always include text label.

---

## Chart Style

- Override `HOUSE_RCPARAMS` for dark mode:
  ```python
  dark_overrides = {
      "axes.facecolor": "#161b22",
      "figure.facecolor": "#0d1117",
      "axes.edgecolor": "#30363d",
      "axes.labelcolor": "#8b949e",
      "xtick.color": "#8b949e",
      "ytick.color": "#8b949e",
      "text.color": "#e6edf3",
      "grid.color": "#21262d",
      "grid.linewidth": 0.4,
      "axes.prop_cycle": plt.cycler("color", ["#388bfd", "#3fb950", "#f78166", "#d2a8ff", "#ffa657", "#79c0ff", "#a5d6ff", "#8b949e"]),
  }
  ```
- Single-metric charts: use `accent_primary` (`#388bfd`) as the series color.
- Threshold/alert lines: `negative` (`#f85149`), dashed, labeled.
- Zero/baseline lines: `border` (`#30363d`).
- Chart backgrounds: match `surface` (`#161b22`).

---

## Table Style

- Header row: `surface_alt` (`#1c2128`), 12px/600, `text_primary`.
- Alternating rows: `surface` / `surface_alt`.
- Border: 1px `border` between rows. No heavy outer border.
- Right-align numeric columns; use monospace for IDs and hash values.
- Positive delta: `positive` (`#3fb950`). Negative delta: `negative` (`#f85149`). Warning: `warning` (`#d29922`). All with text label.
- Alert rows: `negative` left border at 2px or `negative` background tint at 10% opacity.

---

## KPI Style

- Value: 20–24px/700, `text_primary`. Monospace font for numbers.
- Label: 10px/500, uppercase, `text_secondary`, letter-spacing 0.06em.
- Status chip: inline 10px badge alongside value. Always text + color.
- Delta: 12px/500, `positive` or `negative`. Arrow + numeric.
- Sparkline: 1px line in `accent_primary`. No fill. Tight padding.
- Threshold marker on sparkline: `negative` dot at threshold breach.

---

## Semantic Color Rules

- **`positive` (`#3fb950`) is strictly for favorable metric status** — not for data presence, chart fills, or decorative elements. Alert green = "metric is healthy."
- **`negative` (`#f85149`) is for unfavorable metric state or active alert** — not general emphasis.
- **`warning` (`#d29922`) is for a metric approaching a threshold** — not informational annotation.
- **`accent_secondary` (`#3fb950`) = `positive`** in this system. They share the same value intentionally. Do not use green for categorical series or non-status contexts.
- Categorical series must use `categorical_palette` (`#388bfd, #3fb950, ...`) — but `#3fb950` in a categorical context should not appear alongside status chips to avoid confusion. If conflict exists, substitute `#79c0ff` (fifth color) for the categorical green slot.
- All status colors must be paired with a text label or icon — never color alone.

---

## Dashboard Layout Rules

- Row 1: Status bar — system-level health indicators, alert count, and time of last refresh.
- Row 2: Primary alert/exception queue or KPI strip (4–8 compact cards with status chips).
- Row 3: Primary time-series trend with threshold lines and event annotations.
- Row 4+: Segment breakdowns, alert detail tables, log/event feeds.
- Layout: high density, 3–4 column grid. Cards can be as narrow as 200px.
- Sidebar: dark left navigation (`#0d1117`), compact icon + label.
- Filters: inline filter strip below status bar, compact pill style.

---

## Report Layout Rules

This system is dashboard-primary. If used for a report:
- Background remains dark — do not switch to light for "reports."
- Section headers: 16px/600, `text_primary`. Section dividers: 1px `border`.
- Callout blocks: `surface` background, `accent_primary` left border.
- Print: this system does not print well in dark mode. Export charts with white backgrounds if print is required. Prefer `executive-editorial` for print deliverables.

---

## Caption / Title Tone

- Titles: operational and factual. "API error rate exceeded threshold at 03:42 UTC" not "Error Rate."
- Captions: concise, metric + time + status. "P95 latency: 840ms (threshold: 500ms) — 3 instances affected."
- Status language: "degraded," "nominal," "critical," "recovering" — consistent terminology across the dashboard.
- Avoid hedging language in status labels.

---

## Accessibility Rules

- Minimum contrast: 4.5:1 for body text on dark backgrounds. `#e6edf3` on `#161b22` = approx 10:1 — passes.
- All status information must include text label alongside color. Never color alone for alert state.
- Avoid relying on green/red alone — include status text ("OK", "ALERT", "WARN").
- Font size minimum: 10px for status chips; 12px for main metric values.
- Consider color-blind users: `#388bfd` (blue) and `#3fb950` (green) are distinguishable under deuteranopia, but always supplement with text labels.

---

## Format-Specific Guidance

### Markdown Report

- Use code blocks (` ``` `) for status output, logs, or metric snapshots.
- Status summary: bold label + value. `**API Gateway:** DEGRADED — 3 services affected`.
- Use `>` blockquotes for incident summaries or key alert text.
- Tables: full-width, minimal whitespace. Include a Status column with text values.

### HTML Report

- Override `:root` tokens for dark mode:
  ```css
  --bg: #0d1117;
  --surface: #161b22;
  --surface-alt: #1c2128;
  --border: #30363d;
  --text: #e6edf3;
  --text-secondary: #8b949e;
  --accent: #388bfd;
  --accent-light: #1c2840;
  --positive: #3fb950; --positive-bg: #0f2d1a;
  --warning: #d29922; --warning-bg: #2d1e00;
  --negative: #f85149; --negative-bg: #2d0f0f;
  --radius: 4px;
  ```
- Body background: `#0d1117`. Remove `box-shadow` and replace with `border: 1px solid #30363d`.

### HTML Dashboard

- Dark body: `body { background: #0d1117; color: #e6edf3; }`.
- Sidebar: `#0a0c10` or `#0d1117`. Active item: `accent_primary` left border or background tint.
- Status chips: inline `<span>` with background and text. Class names: `chip-ok`, `chip-warn`, `chip-alert`, `chip-degraded`.
- Filter strip: `surface_alt` background, compact height (32px).

### Python / Matplotlib Charts

- Apply dark overrides (see Chart Style section above) on top of `HOUSE_RCPARAMS`.
- Threshold lines: `plt.axhline(threshold, color='#f85149', linestyle='--', linewidth=1, label='Threshold')`.
- Export: `plt.savefig(..., facecolor='#0d1117', bbox_inches='tight')` for dark backgrounds.
- For embedded charts in light reports: set `figure.facecolor = '#ffffff'` and `axes.facecolor = '#ffffff'` and revert text colors.

### R / ggplot2 Charts

```r
theme_occ <- theme_house() + theme(
  plot.background = element_rect(fill = "#0d1117", colour = NA),
  panel.background = element_rect(fill = "#161b22", colour = NA),
  panel.grid.major = element_line(colour = "#21262d", linewidth = 0.4),
  axis.text = element_text(colour = "#8b949e"),
  axis.title = element_text(colour = "#8b949e"),
  text = element_text(colour = "#e6edf3"),
)
scale_colour_occ <- scale_colour_manual(
  values = c("#388bfd", "#3fb950", "#f78166", "#d2a8ff", "#ffa657", "#79c0ff", "#a5d6ff", "#8b949e")
)
```

### Excel / Sheets Dashboard

- Cell fills: dark system is impractical in Excel for standard use. Use a light-mode adaptation: `#0d1117` → `#f0f2f5`; `#388bfd` accent; `#3fb950` positive; `#f85149` negative.
- For dark-mode Excel: use the "Dark Gray" theme or set custom cell fills manually.
- Conditional formatting: green fill (`#d6f5e0`) for positive, red fill (`#fdeaea`) for negative, amber fill (`#fef3e2`) for warning. Include text label in adjacent cell.

### BI Dashboard

- Canvas background: `#0d1117`. Card background: `#161b22`. Card border: `#30363d`.
- Font color: `#e6edf3`. Secondary text: `#8b949e`.
- Accent: `#388bfd`. Alert indicator: `#f85149`. Warning: `#d29922`. Healthy: `#3fb950`.
- Most BI tools have a "dark mode" or custom theme option — apply tokens there.
- Tooltip background: `#1c2128`, text: `#e6edf3`.

---

## Common Mistakes

- Using `positive` (alert green) for chart fills or categorical series — it means "favorable metric status," nothing else.
- Applying this dark system to reports that will be printed or shared with non-specialist executives.
- Treating high density as "more information" — each metric must still earn its place. Density ≠ completeness.
- Forgetting to override chart backgrounds — matplotlib/ggplot default to white, which breaks the dark aesthetic.
- Using this system for a one-time analysis or exploratory notebook — overhead is not worth it.
- Omitting text labels from status chips and relying only on color.
