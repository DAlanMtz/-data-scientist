# Research Paper — Design System

> **Base relationship:** This system adapts the base (`references/chart-style-system.md`) for academic and citation-heavy long-form reports. Surface tokens shift to pure white for a printed-document feel; spacing is very generous; heading hierarchy is reduced. Font is system-ui by default; Georgia or a serif stack is an optional adaptation for PDF-only long-form output.
> Tokens marked ★ intentionally differ from the base. Unmarked tokens follow the base system unless the surrounding guidance further constrains their use.

---

## Purpose

A minimal, legible design system for academic reports, methodology writeups, long-form analysis, and citation-heavy deliverables. Optimized for reading focus, printability, and scholarly credibility. Deprioritizes visual drama in favor of clear argumentation.

---

## Best Use Cases

- Academic or technical reports with citations and methodology sections
- Long-form analysis writeups (10+ pages)
- Methodology documentation for model audits or validation reports
- Research summaries shared with technical reviewers
- PDF-exported analytical documents

---

## Avoid When

- The deliverable is a dashboard — this system has no dashboard optimization.
- The audience is executive and needs a short, impactful summary — use `executive-editorial`.
- The context is operational monitoring — use `operational-command-center`.
- The report is an internal quick-turn deliverable — layout overhead exceeds value.
- Multiple charts need to be compared side by side interactively.

---

## Visual Personality

Near-monochrome and legible. Pure white background maximizes contrast and print quality. Dark slate accent is authoritative without the brand weight of navy or blue. Generous line height and spacing support reading focus. No decorative elements — every visual element must carry information.

---

## Token Summary

| Token | Value | Override |
|---|---|---|
| `background` | `#ffffff` | ★ |
| `surface` | `#ffffff` | ★ |
| `surface_alt` | `#f8f9fa` | ★ |
| `text_primary` | `#212529` | ★ |
| `text_secondary` | `#495057` | ★ |
| `border` | `#dee2e6` | ★ |
| `chart_grid` | `#e9ecef` | ★ |
| `muted_fill` | `#e9ecef` | ★ |
| `accent_primary` | `#2c3e50` | ★ |
| `accent_secondary` | `#7f8c8d` | ★ |
| `positive` | `#27ae60` | ★ |
| `warning` | `#f39c12` | ★ |
| `negative` | `#c0392b` | ★ |
| `categorical_palette` | `#2c3e50, #7f8c8d, #2980b9, #8e44ad, #c0392b, #16a085, #d35400, #bdc3c7` | ★ |
| `sequential_palette` | `#ecf0f1 → #bdc3c7 → #95a5a6 → #566573 → #2c3e50` | ★ |
| `diverging_palette` | `#c0392b → #e8a090 → #f5f5f5 → #a0b8d0 → #2c3e50` | ★ |
| `font_stack` | `system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", "Helvetica Neue", Arial, sans-serif` | |
| `type_scale` | `11px / 13px / 16px / 20px / 26px / 34px` | ★ |
| `spacing_scale` | `4 / 8 / 16 / 24 / 32 / 48 / 64 / 80 px` | ★ |
| `radius` | `2px` | ★ |
| `shadow` | `none` | ★ |

---

## Typography

- **Default font:** system-ui stack. Renders as San Francisco, Segoe UI, or Roboto depending on OS.
- **Optional serif (PDF long-form only):** Georgia, "Times New Roman", serif — use only for PDF output where a scholarly register is explicitly needed. Do not use for web dashboards or screen reports.
- **Heading contrast:** Size-led, restrained. H1: 26–34px/600, H2: 20px/600, H3: 16px/600. No bold contrast drama — headings are navigational, not theatrical.
- **Body:** 16px/400, line-height 1.75. Generous leading is the primary reading comfort mechanism.
- **Abstract / summary block:** 15px/400 italic, `text_secondary`, indented 24px.
- **Citation text:** 12px/400, `text_secondary`. Monospace for DOIs and URLs.
- **Chart text:** 13px for tick labels and axis titles. `text_secondary`.

---

## Spacing and Density

- **Grid:** 8px baseline with generous multiples.
- **Section gap:** 64–80px between major sections.
- **Paragraph spacing:** 16px after each paragraph.
- **Card/figure padding:** 24–32px.
- **Content width:** 680–760px (narrower than a standard report for reading focus).
- **Density:** Very low. Longer content spans more vertical space — that is intentional.

---

## Card / Panel Style

- White surface on white background — no elevation or shadow.
- Thin `border` (`#dee2e6`) as a divider, not a card surround.
- `radius: 2px` — minimal rounding.
- `shadow: none` — flat, print-consistent.
- Figure containers: caption below figure, 12px/400, `text_secondary`. No box around the figure.
- Callout/note blocks: `surface_alt` fill, 2px left border in `accent_secondary` (`#7f8c8d`).
- Definition or equation blocks: `surface_alt` fill, monospace font, 14px.

---

## Chart Style

- Override `HOUSE_RCPARAMS` for this system:
  ```python
  paper_overrides = {
      "axes.facecolor": "#ffffff",
      "figure.facecolor": "#ffffff",
      "grid.color": "#e9ecef",
      "grid.linewidth": 0.4,
      "axes.prop_cycle": plt.cycler("color", ["#2c3e50", "#7f8c8d", "#2980b9", "#8e44ad", "#c0392b", "#16a085", "#d35400", "#bdc3c7"]),
  }
  mpl.rcParams.update({**HOUSE_RCPARAMS, **paper_overrides})
  ```
- First series: `#2c3e50` (dark slate). Second: `#2980b9` (medium blue). Avoid using gray (`#7f8c8d`) as a primary data series — reserve it for reference lines and annotations.
- Figure captions: below each chart, italicized, metric + method + caveat. "Figure 3. Monthly churn rate by cohort (n=1,240). Rates below 10 observations are suppressed."
- No filled area charts unless showing prediction intervals.
- Grid lines: subtle at 0.4 linewidth. Can be removed entirely for minimal single-series charts.

---

## Table Style

- Header row: `surface_alt` (`#f8f9fa`), 14px/600.
- Alternating rows: white / `surface_alt`.
- Border: 1px `border` (`#dee2e6`) on all sides. Academic tables often use lines above and below header only — either style is acceptable.
- Right-align numeric columns; left-align text.
- Footnotes below the table: 11px/400, `text_secondary`, prefixed with superscript letters.
- Table caption above the table: "Table 2. Summary statistics for [variable], [population], [period]."

---

## KPI Style

This system is not optimized for KPI cards. If a summary metric is needed:
- Value: 26px/600, `text_primary`.
- Label: 13px/400, `text_secondary`.
- No colored background. No chip badges.
- Place in a simple two-column summary block at the top of a section.

---

## Semantic Color Rules

- `positive` (`#27ae60`) encodes a favorable metric state — not general emphasis or chart fill.
- `warning` (`#f39c12`) encodes approaching a threshold — not annotation.
- `negative` (`#c0392b`) encodes unfavorable state or a statistically significant adverse finding.
- `accent_secondary` (`#7f8c8d`, gray) is for reference lines, annotations, and secondary labels — not status.
- In this near-monochrome system: be especially deliberate with color. Every use of green or red implies a value judgment. Use sparingly and always with a text label.
- Do not color chart series with `positive`/`negative` unless the series represents a directional metric.

---

## Dashboard Layout Rules

This system is report-primary. If used for a dashboard:
- Limit to one chart per screen section.
- No sidebar. Top navigation or in-page section links.
- Treat each "card" as a research figure — caption required.
- Do not use chip badges or status indicators — describe findings in text.

---

## Report Layout Rules

- Standard academic structure: Abstract → Introduction → Data and Methods → Results → Discussion → Limitations → Conclusion → References → Appendix.
- Each section starts on a new page (or with 80px top spacing in web output).
- In-text citations: parenthetical format. Reference list in a separate appendix.
- Figures and tables: numbered sequentially across the document. Captions identify content, method, and caveat.
- Methodology section: describe data grain, source, exclusion rules, and any proxy variables used.

---

## Caption / Title Tone

- Chart titles: descriptive-first. "Distribution of residuals for the holdout validation set (n=2,400)" — not a finding headline.
- Captions: complete and self-contained. A reader should understand the figure from the caption alone without reading surrounding text.
- Section titles: neutral and descriptive. "Results," "Model Validation," "Sensitivity Analysis."
- Avoid marketing or persuasion language. Hedges are appropriate: "suggests," "is consistent with," "does not rule out."
- Causal language: use only when the study design supports causal inference (randomized experiment, instrumental variable, difference-in-differences). Otherwise use correlational language.

---

## Accessibility Rules

- Minimum contrast: 4.5:1. `#212529` on `#ffffff` = approx 16:1 — well above minimum.
- Print: test all charts in grayscale. Use pattern fills or direct labels to distinguish series without color.
- Font size minimum: 11px for figure captions, 12px for table footnotes.
- Tables: use `<th scope="col">` in HTML for screen readers.
- No information conveyed by color alone in charts — use markers, line styles, or direct labels as supplements.

---

## Format-Specific Guidance

### Markdown Report

- Use numbered headings for navigational clarity in long documents: `## 2. Data and Methods`.
- Abstract/summary: unindented blockquote or italic paragraph at document top.
- Citations: `[Author, Year]` inline; full reference list at bottom under `## References`.
- Tables: left-align text columns, right-align numeric. Include unit in column header.
- Figure placeholders: `_Figure N: [caption text]_` below the image or code block.

### HTML Report

- Override `:root` tokens:
  ```css
  --bg: #ffffff;
  --surface: #ffffff;
  --surface-alt: #f8f9fa;
  --border: #dee2e6;
  --text: #212529;
  --text-secondary: #495057;
  --accent: #2c3e50;
  --accent-light: #ecf0f1;
  --radius: 2px;
  ```
- Content width: 720px. Line height: 1.75 for body text.
- Section dividers: 1px `#dee2e6` horizontal rule, 64px top margin.
- No box shadows. No decorative backgrounds.
- Print: no changes needed — this system is already print-optimized.

### HTML Dashboard

- Not recommended. If required: use a minimal single-column layout.
- Background: `#ffffff`. Borders only — no card shadows.
- Charts: figures with captions, not interactive KPI cards.

### Python / Matplotlib Charts

- Apply `paper_overrides` (see Chart Style section) on top of `HOUSE_RCPARAMS`.
- Figure captions: add as `plt.figtext(0.5, -0.04, "Figure N. Caption text.", ha='center', fontsize=11, color='#495057')`.
- Export: `plt.savefig(..., dpi=300, bbox_inches='tight', facecolor='white')` for print quality.
- For grayscale print: `plt.set_cmap('Greys')` for sequential; use distinct markers (`'o', 's', '^', 'D'`) for multi-series.

### R / ggplot2 Charts

```r
theme_paper <- theme_house() + theme(
  plot.background = element_rect(fill = "#ffffff", colour = NA),
  panel.grid.major = element_line(colour = "#e9ecef", linewidth = 0.4),
  panel.grid.minor = element_blank(),
  plot.caption = element_text(size = 10, colour = "#495057", face = "italic"),
)
scale_colour_paper <- scale_colour_manual(
  values = c("#2c3e50", "#7f8c8d", "#2980b9", "#8e44ad", "#c0392b", "#16a085", "#d35400", "#bdc3c7")
)
```

### Excel / Sheets Dashboard

- Worksheet style: white background, thin `#dee2e6` borders, no cell shadows.
- Header row: `#f8f9fa` fill, bold text.
- Accent highlight: `#2c3e50` text bold on `#f8f9fa`. Avoid colored fills for emphasis — use bold.
- Conditional formatting: green (`#d5f5e3`) for positive, red (`#fdecea`) for negative — with text labels in adjacent cells.
- Footnotes: row below the table, italic, `#495057`.

### BI Dashboard

- Canvas background: `#ffffff`. Card background: `#ffffff`. Card border: `#dee2e6`, no shadow.
- Font: system sans-serif, 16px body, 20–26px heading.
- Accent: `#2c3e50`. No colored sidebar.
- Tooltip: light background (`#f8f9fa`), `#212529` text.
- Caption block below each visual: 11px italic text description.

---

## Common Mistakes

- Using bold red/green colors for chart series — in this near-monochrome system, saturated colors draw disproportionate attention.
- Short-form captions ("Figure 3: Revenue") — captions must be self-contained descriptions.
- Using this system for dashboards — it provides no interaction affordances.
- Switching to serif fonts for web/screen reports — reserve serif for PDF-only contexts.
- Reducing line height or spacing for length — this system's legibility depends on generous whitespace.
- Omitting uncertainty or confidence intervals from findings sections.
