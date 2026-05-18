# Warm Narrative — Design System

> **Base relationship:** This system adapts the base (`references/chart-style-system.md`) for explanatory, reader-friendly reports. The palette shifts to warm terracotta and sage; spacing is very generous; the tone is conversational rather than clinical.
> Tokens marked ★ intentionally differ from the base. Unmarked tokens follow the base system unless the surrounding guidance further constrains their use.

---

## Purpose

A warm, approachable design system for narrative reports aimed at non-technical audiences: customer-facing summaries, newsletter-style analyses, explanatory writeups, and team updates where reading experience matters more than data density.

---

## Best Use Cases

- Customer-facing data summaries and insights reports
- Non-technical stakeholder newsletters and team updates
- Explanatory analysis with heavy narrative context
- Public-facing data journalism or research summaries
- Onboarding reports where audience is unfamiliar with the data

---

## Avoid When

- The dashboard monitors live data — use `operational-command-center`.
- The audience is finance or technical and expects density — use `financial-terminal` or `clean-saas-analytics`.
- The report is a dense data grid or comparison table — this system's generous spacing is inappropriate for tabular-heavy output.
- The deliverable is a board or executive readout — use `executive-editorial`.
- Real-time or high-refresh contexts — layout is not optimized for live updates.

---

## Visual Personality

Warm, editorial, and explanation-forward. Terracotta as the primary accent creates energy without corporate coldness. Sage green anchors positive metrics with a natural, calm feel. Generous spacing and reading-focused typography lower the cognitive bar for non-expert audiences.

---

## Token Summary

| Token | Value | Override |
|---|---|---|
| `background` | `#fdf8f3` | ★ |
| `surface` | `#ffffff` | |
| `surface_alt` | `#f7f1ea` | ★ |
| `text_primary` | `#2d2016` | ★ |
| `text_secondary` | `#5c4a38` | ★ |
| `border` | `#e8ddd0` | ★ |
| `chart_grid` | `#e8ddd0` | ★ |
| `muted_fill` | `#ede4d8` | ★ |
| `accent_primary` | `#c25c2e` | ★ |
| `accent_secondary` | `#5c8a5c` | ★ |
| `positive` | `#3d7a3d` | ★ |
| `warning` | `#b07010` | ★ |
| `negative` | `#a83428` | ★ |
| `categorical_palette` | `#c25c2e, #5c8a5c, #7c5c9a, #2e7a8a, #b8860b, #8a4a2e, #4a7a5a, #9ba5b2` | ★ |
| `sequential_palette` | `#fdf8f3 → #f0d8be → #e0b080 → #c87840 → #c25c2e` | ★ |
| `diverging_palette` | `#a83428 → #e8b0a8 → #f5f0e8 → #a8c8a8 → #5c8a5c` | ★ |
| `font_stack` | `system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", "Helvetica Neue", Arial, sans-serif` | |
| `type_scale` | `11px / 14px / 16px / 20px / 26px / 36px` | ★ |
| `spacing_scale` | `4 / 8 / 16 / 24 / 32 / 40 / 56 / 72 px` | ★ |
| `radius` | `8px` | ★ |
| `shadow` | `0 2px 8px rgba(194,92,46,0.08)` | ★ |

---

## Typography

- **Font:** system-ui stack.
- **Heading style:** Warm and readable. H1: 36px/700, H2: 26px/600, H3: 20px/600. Not sterile or corporate.
- **Body:** 16px/400, line-height 1.7. Comfortable for reading extended prose.
- **Lead paragraph:** First paragraph of a section at 18px/400. Creates an easy entry point.
- **Callout text:** 18px/400, `accent_primary`, left border in `accent_primary` at 3px. For key findings or pull quotes.
- **Caption text:** 13px/400 italic, `text_secondary`.
- **Chart text:** 13px for axis labels and legends. `text_secondary`.

---

## Spacing and Density

- **Grid:** 8px baseline with generous multiples.
- **Section gap:** 56–72px between major sections.
- **Card padding:** 24–32px.
- **Content width:** 760–860px. Readable column width for prose.
- **Density:** Low. White space is not waste — it aids reading comprehension.
- **Between paragraphs:** 16–20px.

---

## Card / Panel Style

- White surface on warm cream background (`#fdf8f3`).
- 1px `border` (`#e8ddd0`) — warm, understated.
- `radius: 8px` — more rounded, approachable.
- `shadow: 0 2px 8px rgba(194,92,46,0.08)` — warm-tinted shadow.
- Callout/highlight block: `surface_alt` (`#f7f1ea`) background, 3px left border in `accent_primary` (`#c25c2e`).
- "Did you know" / insight block: `surface_alt` fill, 8px radius, `text_secondary` label above.
- No heavy card borders — warmth comes from background color contrast, not border weight.

---

## Chart Style

- Override `HOUSE_RCPARAMS` for warm background:
  ```python
  warm_overrides = {
      "axes.facecolor": "#ffffff",
      "figure.facecolor": "#fdf8f3",
      "grid.color": "#e8ddd0",
      "grid.linewidth": 0.5,
      "axes.prop_cycle": plt.cycler("color", ["#c25c2e", "#5c8a5c", "#7c5c9a", "#2e7a8a", "#b8860b", "#8a4a2e", "#4a7a5a", "#9ba5b2"]),
  }
  mpl.rcParams.update({**HOUSE_RCPARAMS, **warm_overrides})
  ```
- First series: `#c25c2e` (terracotta). Second: `#5c8a5c` (sage).
- Bar charts: single warm terracotta fill by default. Multi-series: `categorical_palette` in order.
- Inactive / background series: `muted_fill` (`#ede4d8`).
- Annotations: `text_secondary` with conversational label text ("This is where we changed pricing").

---

## Table Style

- Header row: `surface_alt` (`#f7f1ea`), 14px/600.
- Alternating rows: white / `surface_alt`.
- Border: 1px `border` (`#e8ddd0`).
- Right-align numeric columns; left-align text.
- `radius: 4px` on table container.
- Positive delta: `positive` (`#3d7a3d`). Negative delta: `negative` (`#a83428`). Include text.
- Keep tables short (max 10 rows visible). Offer "See full table" for longer data.

---

## KPI Style

- Value: 36px/700, `accent_primary` or `text_primary`. Large and readable.
- Label: 13px/400, `text_secondary`. Conversational phrasing: "customers this month" not "MTD_CUST_COUNT".
- Delta: 14px/500. "Up 12% from last month" — written-out, not abbreviated.
- Context sentence below value: "That's 340 more than our target." `text_secondary`, 14px/400.
- No colored background fills on KPI cards — warmth comes from background and typography.

---

## Semantic Color Rules

- `positive` (`#3d7a3d`, warm forest green) encodes a favorable metric state — not general decoration or chart fills.
- `warning` (`#b07010`, warm amber) encodes approaching a threshold — not annotation or callout styling.
- `negative` (`#a83428`, warm brick red) encodes an unfavorable metric state — not emphasis.
- `accent_primary` (`#c25c2e`, terracotta) is the visual voice of this system — use for chart series, callout borders, and heading accents. It is NOT a semantic color. Terracotta does not mean positive or negative.
- `accent_secondary` (`#5c8a5c`, sage) is a complementary visual color — use for secondary chart series and decorative text accents. Sage is NOT inherently positive. Use `positive` for metric direction, sage for visual complement.
- All status colors must be paired with text — never color alone.

---

## Dashboard Layout Rules

This system is report-primary. If used for a dashboard:
- Limit to one finding per "section" or scroll view.
- KPI cards: 2–3 max, large values, conversational labels.
- Primary chart: full width, with a written lead-in sentence above and takeaway caption below.
- Avoid sidebar navigation — use top tabs or section navigation.
- No dense filter strips — use simple dropdowns in a clean top bar.

---

## Report Layout Rules

- Structure: Introduction / Context → Key Finding → What It Means → Supporting Evidence → What's Next.
- Opening paragraph: set the scene for a non-technical reader. What decision does this illuminate?
- Each section: lead with the finding, then support it with the chart/table, then explain implications.
- Avoid jargon. Define any technical term on first use.
- Closing: clear next step, owner, and follow-up action.
- Length: err on the side of shorter. A 4-page warm narrative report is more effective than an 8-page dense one.

---

## Caption / Title Tone

- Chart titles: conversational and finding-forward. "More customers are returning for a second purchase" not "Second Purchase Rate, Monthly."
- Captions: human and specific. "Of the 2,400 customers who joined in January, about 1 in 3 made a second purchase within 90 days."
- Avoid jargon in captions: write "number of users" not "n=2,400 monthly actives."
- Use first or second person sparingly but naturally: "Here's how this played out across regions."
- Caveats: include, but in plain language. "Note: the small number of customers in Region 4 means this result is less certain."

---

## Accessibility Rules

- Minimum contrast: 4.5:1. `#2d2016` on `#fdf8f3` = approx 12:1 — well above minimum.
- Status information must include text label alongside color.
- Font size minimum: 13px for captions and labels.
- Warm tones are friendly but subtle — test color-coded statuses at low saturation and with color blindness simulators.
- Direct labels preferred over legends — reduces cognitive load for non-technical audiences.
- Charts: include brief written interpretation below every chart. Non-expert readers need the takeaway stated explicitly.

---

## Format-Specific Guidance

### Markdown Report

- Open each section with a bold summary sentence. "**In Q3, repeat purchase rates rose across all regions.**"
- Use conversational blockquotes (`>`) for key findings: `> About 1 in 3 new customers returned within 90 days.`
- Bullet lists: keep to 3–5 items. Long bullets are anti-pattern — write sentences.
- Tables: limited to 6–8 rows for narrative reports. Caption above the table in plain language.
- Footnotes: use sparingly and in plain language.

### HTML Report

- Override `:root` tokens:
  ```css
  --bg: #fdf8f3;
  --surface-alt: #f7f1ea;
  --border: #e8ddd0;
  --text: #2d2016;
  --text-secondary: #5c4a38;
  --accent: #c25c2e;
  --accent-light: #f7e8dd;
  --positive: #3d7a3d; --positive-bg: #e8f5e8;
  --warning: #b07010; --warning-bg: #fef3e0;
  --negative: #a83428; --negative-bg: #fdeaea;
  --radius: 8px;
  --shadow: 0 2px 8px rgba(194,92,46,0.08);
  ```
- Body font size: 16px. Line height: 1.7.
- Heading font: system-ui, sizes 36/26/20px.
- Content width: 820px. Generous top/bottom section padding (56px).

### HTML Dashboard

- Warm cream background (`#fdf8f3`). White card surfaces with warm border.
- Avoid dark sidebars — use a warm-toned top navigation bar (`#f7f1ea` fill, `text_primary` text).
- Filter area: simple, full-width top bar with `surface_alt` background.
- Cards: `8px` radius, warm shadow.

### Python / Matplotlib Charts

- Apply `warm_overrides` (see Chart Style section) on top of `HOUSE_RCPARAMS`.
- Annotations: conversational label style. `ax.annotate("Pricing change", ...)` with arrow.
- For single-series bar charts: `color='#c25c2e'`, no legend needed.
- Export: `plt.savefig(..., facecolor='#fdf8f3', bbox_inches='tight')`.

### R / ggplot2 Charts

```r
theme_warm <- theme_house() + theme(
  plot.background = element_rect(fill = "#fdf8f3", colour = NA),
  panel.grid.major = element_line(colour = "#e8ddd0", linewidth = 0.5),
  axis.text = element_text(colour = "#5c4a38"),
  axis.title = element_text(colour = "#5c4a38"),
  plot.caption = element_text(colour = "#5c4a38", face = "italic", size = 11),
)
scale_colour_warm <- scale_colour_manual(
  values = c("#c25c2e", "#5c8a5c", "#7c5c9a", "#2e7a8a", "#b8860b", "#8a4a2e", "#4a7a5a", "#9ba5b2")
)
```

### Excel / Sheets Dashboard

- Background: `#fdf8f3`. Card fill: `#ffffff`. Border: `#e8ddd0`.
- Header fill: `#f7f1ea`. Header font: bold, `#2d2016`.
- Accent highlight: `#c25c2e` text bold or `#f7e8dd` cell fill.
- Positive delta: `#3d7a3d` text. Negative delta: `#a83428` text.
- Use Calibri or Arial — match the readable, clean feel.
- Avoid harsh cell borders — use light `#e8ddd0` borders only.

### BI Dashboard

- Canvas background: `#fdf8f3`. Card background: `#ffffff`. Card border: `#e8ddd0`, `8px` radius.
- Accent color: `#c25c2e`. Positive: `#3d7a3d`. Warning: `#b07010`. Negative: `#a83428`.
- Font: system sans-serif, 16px body. Avoid monospace.
- Tooltip: warm surface (`#f7f1ea`), `#2d2016` text.
- Legend: prefer direct labels in charts over separate legend panels.

---

## Common Mistakes

- Using `accent_primary` (terracotta) for positive status — terracotta is a visual personality color, not a semantic color.
- Using `accent_secondary` (sage green) to mean "positive" — sage is decorative. Use `positive` (`#3d7a3d`) for metric status.
- Over-explaining in chart captions for technical audiences who are receiving this report — calibrate explanation depth to the actual audience.
- Reducing spacing to fit more content — density destroys the warm/readable feel. Cut content instead.
- Using technical metric names in KPI labels — rewrite for the audience.
- Omitting the opening context paragraph — non-technical readers need framing before data.
