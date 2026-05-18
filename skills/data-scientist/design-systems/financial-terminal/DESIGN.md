# Financial Terminal — Design System

> **Base relationship:** This system departs significantly from the base (`references/chart-style-system.md`). It is a dark-mode, monospace-first, maximum-density system for finance, risk, and trading contexts. Nearly all tokens differ from the base; font is monospace-first rather than system-ui.
> Tokens marked ★ intentionally differ from the base. Unmarked tokens follow the base system unless the surrounding guidance further constrains their use.

---

## Purpose

A high-density, dark-mode design system modeled on financial terminal interfaces — Bloomberg, trading platforms, risk dashboards. Optimized for users who scan large amounts of numerical data quickly and expect compact, monospace-forward presentation.

---

## Best Use Cases

- Finance and P&L dashboards
- Risk management and exposure monitoring dashboards
- Trading desks and market data platforms
- Quantitative analysis workspaces
- Backtesting and model performance dashboards for finance teams

---

## Avoid When

- The audience is non-specialist — this system assumes familiarity with terminal-style interfaces. Compact monospace spacing is unintuitive for first-time readers.
- The output is a report for executives or board members — use `executive-editorial`.
- The dashboard will be used in bright ambient light or on non-calibrated screens.
- The content is narrative or explanatory — use `warm-narrative`.
- The dashboard is exploratory or used infrequently — dense layouts penalize occasional users.
- Do not use for general analytics dashboards. The visual weight signals specialized finance context that may confuse general audiences.

---

## Visual Personality

Terminal black with precision-first aesthetics. Monospace type for all numeric values creates the data-density and alignment that finance users expect. Terminal blue and terminal green are status colors, not decorative elements. Maximum information density per screen unit.

---

## Token Summary

| Token | Value | Override |
|---|---|---|
| `background` | `#0a0c10` | ★ |
| `surface` | `#111418` | ★ |
| `surface_alt` | `#161a20` | ★ |
| `text_primary` | `#e2e8f0` | ★ |
| `text_secondary` | `#94a3b8` | ★ |
| `border` | `#1e2530` | ★ |
| `chart_grid` | `#1a2030` | ★ |
| `muted_fill` | `#1a2030` | ★ |
| `accent_primary` | `#58a6ff` | ★ |
| `accent_secondary` | `#3fb950` | ★ |
| `positive` | `#3fb950` | ★ |
| `warning` | `#ffa657` | ★ |
| `negative` | `#f85149` | ★ |
| `categorical_palette` | `#58a6ff, #ffa657, #d2a8ff, #ff7b72, #79c0ff, #a5d6ff, #3fb950, #8b949e` | ★ |
| `sequential_palette` | `#0a0c10 → #0e2040 → #1a3a6a → #2a5a9a → #58a6ff` | ★ |
| `diverging_palette` | `#f85149 → #3d1510 → #111418 → #0f2d1a → #3fb950` | ★ |
| `font_stack` | `"SFMono-Regular", "Cascadia Mono", Menlo, Consolas, "Liberation Mono", monospace` | ★ |
| `type_scale` | `10px / 11px / 13px / 15px / 18px / 24px` | ★ |
| `spacing_scale` | `4 / 6 / 8 / 12 / 16 / 20 / 28 / 36 px` | ★ |
| `radius` | `2px` | ★ |
| `shadow` | `0 2px 8px rgba(0,0,0,0.6)` | ★ |

---

## Typography

- **Font:** Monospace-first. `"SFMono-Regular", "Cascadia Mono", Menlo, Consolas, "Liberation Mono", monospace` for all numeric values, metric labels, tickers, IDs, and data cells.
- **General UI text (section headers, nav labels):** System-ui can be used for non-numeric labels to reduce visual monotony — `system-ui, sans-serif`.
- **Size:** Very compact. Base text: 13px. Tick labels: 10–11px. Status chips: 10px.
- **Weight:** Use 600/700 only for the primary metric value in a KPI card. All other weights: 400–500.
- **Letter spacing:** None for monospace — it has intrinsic spacing. For uppercase status labels: 0.06em.

---

## Spacing and Density

- **Grid:** 4px sub-grid. All values in 2–4px increments.
- **Card padding:** 8–10px.
- **KPI card height:** 50–70px.
- **Gap between cards:** 6px.
- **Section gap:** 12–16px.
- **Density:** Maximum. Tables are the primary visualization medium — charts are secondary.

---

## Card / Panel Style

- Terminal black surface (`#111418`) on near-black background (`#0a0c10`).
- 1px `border` (`#1e2530`) — very subtle, nearly invisible.
- `radius: 2px` — minimal. Square-cornered feel is appropriate.
- `shadow: 0 2px 8px rgba(0,0,0,0.6)`.
- Accent border variant: 1px left border in `accent_primary` (`#58a6ff`) for selected/active panels.
- Section headers: 10px/500 monospace, `text_secondary`, uppercase, letter-spacing 0.08em.
- Status indicators: inline badge with color + text. Never color alone.

---

## Chart Style

- Override `HOUSE_RCPARAMS` for terminal dark:
  ```python
  terminal_overrides = {
      "axes.facecolor": "#111418",
      "figure.facecolor": "#0a0c10",
      "axes.edgecolor": "#1e2530",
      "axes.labelcolor": "#94a3b8",
      "xtick.color": "#94a3b8",
      "ytick.color": "#94a3b8",
      "text.color": "#e2e8f0",
      "grid.color": "#1a2030",
      "grid.linewidth": 0.3,
      "font.family": "monospace",
      "font.monospace": ["SFMono-Regular", "Cascadia Mono", "Menlo", "Consolas", "DejaVu Sans Mono"],
      "axes.prop_cycle": plt.cycler("color", ["#58a6ff", "#ffa657", "#d2a8ff", "#ff7b72", "#79c0ff", "#a5d6ff", "#3fb950", "#8b949e"]),
  }
  mpl.rcParams.update({**HOUSE_RCPARAMS, **terminal_overrides})
  ```
- Line charts preferred over bar charts for time-series data.
- Candlestick / OHLC charts: use matplotlib-finance or custom rendering. Up bars: `positive` (`#3fb950`). Down bars: `negative` (`#f85149`).
- Reference lines (zero, benchmark): `border` (`#1e2530`) at 1px.
- Annotations: `text_secondary` (`#94a3b8`), monospace, 10px.

---

## Table Style

- Tables are the primary visualization medium — optimize for density and scannability.
- Header row: `surface_alt` (`#161a20`), 11px/600 monospace, `text_primary`.
- Row height: 24–28px (compact).
- Alternating rows: `surface` / `surface_alt`.
- Border: 1px `border` between rows. No thick outer borders.
- All numeric columns: right-aligned, monospace. Ticker/ID columns: left-aligned, monospace.
- Positive values: `positive` (`#3fb950`). Negative values: `negative` (`#f85149`). Include sign (+ / –).
- P&L cells with absolute values: also encode magnitude with subtle background tint (10% opacity of `positive`/`negative`).

---

## KPI Style

- Value: 18–24px/600, monospace, `text_primary`.
- Label: 10px/500, uppercase, monospace, `text_secondary`, letter-spacing 0.06em.
- Change indicator: 11px/500 monospace. `+2.4%` in `positive` or `-1.8%` in `negative`. Always include the sign character.
- Absolute change alongside percentage: `+$1.2M (+2.4%)`.
- Status chip: 10px badge. Color + text abbreviation: "POS", "NEG", "WARN", "FLAT".

---

## Semantic Color Rules

- **`positive` (`#3fb950`) = favorable metric direction** — green means the metric is moving in the desired direction (profit up, risk down, etc.).
- **`negative` (`#f85149`) = unfavorable metric direction** — red means the metric is moving against the desired direction.
- **`warning` (`#ffa657`) = threshold proximity** — approaching a risk limit or performance floor.
- **`accent_primary` (`#58a6ff`, terminal blue) = selected state, highlights, focus** — not a status color.
- **`accent_secondary` (`#3fb950`) = same value as `positive`** — green in this system always means favorable metric status. Do not use it for neutral highlighting, chart fills, or decorative emphasis.
- In categorical charts: `#3fb950` appears as the seventh palette slot. If a categorical series uses this slot alongside status indicators, substitute `#a5d6ff` to avoid ambiguity.
- All status colors must be paired with a text label or numeric value — never color alone.
- **Never use `positive`/`negative` for categorical groupings** — use `categorical_palette` starting from `#58a6ff`.

---

## Dashboard Layout Rules

- Maximum density layout. Tables dominate — charts are supplementary or for trend context only.
- Row 1: P&L summary strip or top-level KPI bar (6–10 compact cards).
- Row 2: Primary data table (full width or 60%) + key trend chart (40%).
- Row 3+: Breakdown tables, risk matrix, position detail, decomposition.
- Sidebar: compact dark nav, icon + ticker or label.
- Filters: inline above the primary table — date range, instrument, portfolio, region.
- No empty states or explanatory text — assume user expertise.

---

## Report Layout Rules

This system is dashboard-primary. If used for a report:
- Background remains dark — do not switch to light mode for reports.
- Tables are the narrative — embed charts only for trend or distribution context.
- Section dividers: 1px `border` (`#1e2530`).
- Print: this system does not render well in print. Export to Excel/CSV for print-friendly output. Prefer `executive-editorial` or `research-paper` for print deliverables.

---

## Caption / Title Tone

- No elaborate titles. Tickers, periods, and metric names suffice: "AAPL — Rolling 30d Vol (Annualized)".
- Annotations: date + event label. "Mar 10: Fed announcement."
- Captions: factual and compact. "P&L by desk, USD M, MTD." No narrative prose.
- Status: abbreviated, consistent. "↑ 3.2%" or "↓ 1.8%". Always include direction symbol.

---

## Accessibility Rules

- Minimum contrast: 4.5:1. `#e2e8f0` on `#111418` = approx 9:1 — passes.
- Status information must include text label alongside color. Do not rely on green/red alone.
- Color-blind consideration: `#58a6ff` (blue) and `#3fb950` (green) — distinguishable under protanopia/deuteranopia, but always supplement with `+`/`–` sign and text label.
- Font size minimum: 10px for status chips; 11px for table values.
- Consider high-density fatigue for users without terminal interface training — provide tooltips or expandable detail rows.

---

## Format-Specific Guidance

### Markdown Report

- Use monospace code blocks (` ``` `) for P&L tables and numerical output.
- ASCII table formatting: acceptable and preferred for numeric grids in markdown contexts.
- Status: use `+` / `–` signs and parenthetical values. Bold for primary metric.
- Keep narrative minimal — numbers carry the report.

### HTML Report

- Override `:root` tokens for terminal dark:
  ```css
  --bg: #0a0c10;
  --surface: #111418;
  --surface-alt: #161a20;
  --border: #1e2530;
  --text: #e2e8f0;
  --text-secondary: #94a3b8;
  --accent: #58a6ff;
  --accent-light: #0e2040;
  --positive: #3fb950; --positive-bg: #0f2d1a;
  --warning: #ffa657; --warning-bg: #2d1e00;
  --negative: #f85149; --negative-bg: #2d0f0f;
  --font: "SFMono-Regular", "Cascadia Mono", Menlo, Consolas, monospace;
  --radius: 2px;
  ```
- Override body font to monospace. Table cells: 12–13px monospace, compact padding.

### HTML Dashboard

- Dark body: `background: #0a0c10; color: #e2e8f0; font-family: monospace`.
- Table-heavy layout: `<table>` elements with full-width data grids.
- Status spans: `<span class="pos">+3.2%</span>` with CSS `.pos { color: #3fb950; }`.
- Sidebar: `#0a0c10`, compact 40px width when collapsed.

### Python / Matplotlib Charts

- Apply `terminal_overrides` (see Chart Style section) on top of `HOUSE_RCPARAMS`.
- Line charts: `linewidth=1.2`. No markers unless indicating key events.
- Area bands (confidence intervals, ranges): `alpha=0.15` with the series color.
- Candlestick: use `mplfinance` library. Style: `type='candle', style='nightclouds'` (adapt for token colors).
- Export: `plt.savefig(..., facecolor='#0a0c10', bbox_inches='tight')`.

### R / ggplot2 Charts

```r
theme_terminal <- theme_house() + theme(
  plot.background = element_rect(fill = "#0a0c10", colour = NA),
  panel.background = element_rect(fill = "#111418", colour = NA),
  panel.grid.major = element_line(colour = "#1a2030", linewidth = 0.3),
  axis.text = element_text(colour = "#94a3b8", size = 9, family = "mono"),
  axis.title = element_text(colour = "#94a3b8", size = 10),
  text = element_text(colour = "#e2e8f0", family = "mono"),
)
scale_colour_terminal <- scale_colour_manual(
  values = c("#58a6ff", "#ffa657", "#d2a8ff", "#ff7b72", "#79c0ff", "#a5d6ff", "#3fb950", "#8b949e")
)
```

### Excel / Sheets Dashboard

- Dark mode is impractical in standard Excel. Light-mode adaptation: use `#f0f2f5` background, `#1a2942` accent.
- If dark Excel: fill cells manually with `#111418`. This requires manual maintenance — document the color codes in a named style sheet.
- Monospace: set cell font to Consolas or Courier New for numeric columns.
- P&L conditional formatting: green fill `#c6efce` for positive, red fill `#ffc7ce` for negative — with sign prefix in cell value.
- Named styles: `Terminal_Value`, `Terminal_Positive`, `Terminal_Negative`, `Terminal_Header`.

### BI Dashboard

- Canvas background: `#0a0c10`. Card background: `#111418`. Card border: `#1e2530`.
- Font color: `#e2e8f0`. Use monospace font if supported by the BI tool.
- Accent: `#58a6ff`. Positive: `#3fb950`. Warning: `#ffa657`. Negative: `#f85149`.
- Most BI tools have limited dark-mode support — use the tool's dark theme as a starting point and override with these tokens where possible.
- Tooltip: `#161a20` background, monospace font, compact.

---

## Common Mistakes

- Using `positive` (terminal green) for chart fill or categorical series — it means favorable metric direction only.
- Applying this system to general analytics dashboards — the monospace density signals specialized finance context and confuses non-specialist users.
- Sharing dark terminal dashboards as print documents — always export to a light-mode format for print.
- Omitting the sign (+ / –) from numeric deltas — terminal users expect explicit direction characters.
- Using proportional (non-monospace) fonts for numeric columns — column misalignment is a usability failure in dense data tables.
- Building this system for occasional users — dense monospace layouts require trained familiarity.
