# Executive Editorial — Design System

> **Base relationship:** This system extends the base visual system (`references/chart-style-system.md`) for high-stakes stakeholder reports. The color palette shifts to deep navy and warm gold; spacing becomes more generous for a print-editorial feel.
> Tokens marked ★ intentionally differ from the base. Unmarked tokens follow the base system unless the surrounding guidance further constrains their use.

---

## Purpose

A polished, restrained design system for executive deliverables: board readouts, C-suite reports, investor summaries, and PDF/print exports. Communicates authority and editorial quality. Prioritizes legibility and decision-clarity over density.

---

## Best Use Cases

- C-suite and board-level reports
- Investor or partner stakeholder presentations
- PDF/print-exported visual reports
- Quarterly business review summaries
- Any deliverable where design quality signals credibility

---

## Avoid When

- The output is an operational or monitoring dashboard — use `operational-command-center`.
- Users need to interact with filters or explore data — this is a static-report system.
- The audience is technical and cares about density — use `clean-saas-analytics`.
- The report is a quick internal note or draft — this system adds overhead for ephemeral work.
- Real-time or high-refresh dashboards — layout is not optimized for live data.

---

## Visual Personality

Restrained and authoritative. Deep navy creates a high-contrast, professional tone. Warm gold accents add editorial distinction without decorative excess. Generous white space and strong heading hierarchy signal careful curation. Headings achieve contrast through size and weight, not color.

---

## Token Summary

| Token | Value | Override |
|---|---|---|
| `background` | `#fafaf8` | ★ |
| `surface` | `#ffffff` | |
| `surface_alt` | `#f5f4f0` | ★ |
| `text_primary` | `#11141a` | |
| `text_secondary` | `#4a5060` | |
| `border` | `#d8d4cc` | ★ |
| `chart_grid` | `#e8e5de` | ★ |
| `muted_fill` | `#e2dfd8` | ★ |
| `accent_primary` | `#1a2942` | ★ |
| `accent_secondary` | `#c8a96b` | ★ |
| `positive` | `#1d7d4c` | |
| `warning` | `#a05c0a` | |
| `negative` | `#b72b2b` | |
| `categorical_palette` | `#1a2942, #c8a96b, #2a7f62, #7c3aac, #b5282f, #1a8fa8, #c07d2e, #9ba5b2` | ★ |
| `sequential_palette` | `#ece9e0 → #c8b898 → #a08a60 → #6a5a38 → #1a2942` | ★ |
| `diverging_palette` | `#b72b2b → #e8a0a0 → #f5f3ee → #9aaecc → #1a2942` | ★ |
| `font_stack` | `system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", "Helvetica Neue", Arial, sans-serif` | |
| `type_scale` | `11px / 13px / 15px / 18px / 26px / 36px` | ★ |
| `spacing_scale` | `4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 px` | ★ |
| `radius` | `4px` | ★ |
| `shadow` | `0 1px 2px rgba(0,0,0,0.06)` | ★ |

---

## Typography

- **Font:** system-ui stack. No custom webfonts needed.
- **Heading contrast:** Achieved through size and weight — not color. H1: 36px/700, H2: 26px/700, H3: 18px/600. Strong size contrast between heading levels creates hierarchy without drama.
- **Subheading eyebrow:** Small caps or uppercase 11px/500, `text_secondary`, letter-spacing 0.08em — use for section category labels above headings.
- **Body:** 15px/400, `text_primary`, line-height 1.65.
- **Pull quotes / callouts:** 18px/400 italic, `text_secondary`, left border in `accent_secondary` (`#c8a96b`).
- **Chart text:** 12px for tick labels, 13px for axis/legend. `text_secondary` color.

---

## Spacing and Density

- **Grid:** 8px baseline. Spacing is more generous than base.
- **Section gap:** 48–64px between major sections.
- **Card padding:** 24–32px.
- **Content width:** 860px max (editorial page feel, not full-width dashboard).
- **Density:** Low. White space is intentional — it communicates curation.
- **Print margins:** 40px top/bottom, 48px left/right on A4/letter.

---

## Card / Panel Style

- White surface on warm cream background (`#fafaf8`).
- 1px `border` (`#d8d4cc`) — slightly warmer than base.
- `radius: 4px` — more restrained than base.
- Executive summary block: `surface_alt` background, 3px left border in `accent_primary` (`#1a2942`).
- Finding callout blocks: same left-border treatment with `accent_secondary` (`#c8a96b`).
- No card shadows in print exports — remove `box-shadow` in print media query.

---

## Chart Style

- Override `HOUSE_RCPARAMS` chart grid color: use `#e8e5de` instead of `#e3e5e8`.
- First series color: `#1a2942` (deep navy). Second: `#c8a96b` (gold). Remaining: `categorical_palette` in order.
- Chart background: `#ffffff`. Figure background: `#fafaf8` for screen; `#ffffff` for print.
- No grid lines on minimal charts — remove `axes.grid = True` for single-series bar charts.
- Subtle grid at 0.3–0.4 linewidth for multi-series charts.
- Annotations: `#1a2942` for key labels, `text_secondary` for supporting notes.

---

## Table Style

- Header row: `surface_alt` (`#f5f4f0`), 13px/600.
- Alternating rows: white / `surface_alt`.
- Border: 1px `border` (`#d8d4cc`) — warm tone matches background.
- Right-align numeric columns. Use tabular-numerals or monospace for numbers.
- Positive delta: `#1d7d4c`. Negative delta: `#b72b2b`. Include text alongside color.
- Key rows (summary, total): `accent_primary` (`#1a2942`) text, bold.

---

## KPI Style

- Value: 36px/700, `text_primary`. Generous size communicates importance.
- Label: 11px/500, uppercase, `text_secondary`, letter-spacing 0.08em.
- Delta: 13px/500. Numeric change with direction arrow. Color: `positive` or `negative`.
- Secondary context (vs. target, vs. prior period): 13px/400, `text_secondary`.
- KPI cards have no background fill or border — they sit directly on `background` or `surface`.

---

## Semantic Color Rules

- `positive` (`#1d7d4c`) encodes a favorable metric state only — not general emphasis or chart fills.
- `warning` (`#a05c0a`) encodes approaching a threshold — not decorative annotation.
- `negative` (`#b72b2b`) encodes an unfavorable metric state — not general contrast or emphasis.
- `accent_secondary` (`#c8a96b`, gold) is for editorial callouts, pull-quote borders, and section accents — never for positive/negative status. Gold does not mean "good."
- All status information must include a text label alongside color — never color alone.
- Do not use `categorical_palette` colors for positive/negative states.

---

## Dashboard Layout Rules

This system is report-primary. If used for a dashboard:
- Limit to one decision per page. No busy multi-metric strips.
- KPI section: 2–3 metrics maximum, displayed prominently with generous white space.
- Primary chart: one clear focal visual per view, with a written takeaway title.
- Avoid sidebar navigation — use page/section navigation in print or tabs in web.

---

## Report Layout Rules

- Page structure: Cover / Executive Summary → Main Findings (1–3) → Supporting Evidence → Limitations → Recommendation → Appendix.
- Executive summary: first content block, max 150 words, key finding + recommended action.
- Each finding: takeaway headline → chart/table → 1–2 sentences of interpretation.
- Appendix: data tables, methodology notes, sensitivity analysis — clearly separated.
- Print: ensure page breaks fall between sections. No chart/caption splits across pages.

---

## Caption / Title Tone

- Chart titles: finding-first. "Operating margin compressed 3pp year-over-year" not "Operating Margin."
- Captions: precise. Metric + population + time window + implication. Use parenthetical caveats for small samples.
- Section labels: authoritative but restrained. No exclamation marks. No marketing language.
- Executive summary sentences: short and declarative. Each sentence should be standalone and quotable.

---

## Accessibility Rules

- Minimum contrast ratio: 4.5:1 for body text, 3:1 for large headings.
- Status information must include a text label alongside color.
- Print/PDF: ensure charts are interpretable in grayscale (test by printing without color).
- Font size minimum: 11px for any label in the final exported document.
- Do not rely on color alone to distinguish chart series in print output — use pattern fills or direct labels.

---

## Format-Specific Guidance

### Markdown Report

- Use `#` for report title only. Use `##` for main sections, `###` for subsections.
- Open each section with a bold finding sentence before the supporting text.
- Use blockquotes (`>`) for key findings or executive callout text.
- Minimize use of bullet lists — prefer short paragraphs for executive prose.
- Tables: right-align numeric columns; include unit in column header.

### HTML Report

- Override `:root` tokens in the HTML template:
  ```css
  --bg: #fafaf8;
  --surface-alt: #f5f4f0;
  --border: #d8d4cc;
  --accent: #1a2942;
  --accent-light: #c8a96b;
  --radius: 4px;
  ```
- Add print media query: `background: white; box-shadow: none; border-color: #ccc`.
- Content width: 860px. Heading sizes: H1 36px, H2 26px.
- Use the top-border-only chart container style (1px `#1a2942` top, no side borders).

### HTML Dashboard

- This system is not optimized for interactive dashboards. If used: light background only (no dark sidebar).
- Card borders: 1px `#d8d4cc`. No colored sidebar. Navigation: horizontal tabs at top.
- Filter chips: `surface_alt` background, `text_secondary` text, `border` edge.

### Python / Matplotlib Charts

- Override `HOUSE_RCPARAMS` for this system:
  ```python
  overrides = {
      "axes.facecolor": "#ffffff",
      "figure.facecolor": "#fafaf8",
      "grid.color": "#e8e5de",
      "axes.prop_cycle": plt.cycler("color", ["#1a2942", "#c8a96b", "#2a7f62", "#7c3aac", "#b5282f", "#1a8fa8", "#c07d2e", "#9ba5b2"]),
  }
  mpl.rcParams.update({**HOUSE_RCPARAMS, **overrides})
  ```
- For print/PDF: use `savefig.dpi=300`, `bbox_inches='tight'`, `facecolor='white'`.

### R / ggplot2 Charts

- Build on `theme_house()` with overrides:
  ```r
  theme_executive <- theme_house() + theme(
    plot.background = element_rect(fill = "#fafaf8", colour = NA),
    panel.grid.major = element_line(colour = "#e8e5de", linewidth = 0.4),
  )
  scale_colour_executive <- scale_colour_manual(
    values = c("#1a2942", "#c8a96b", "#2a7f62", "#7c3aac", "#b5282f", "#1a8fa8", "#c07d2e", "#9ba5b2")
  )
  ```

### Excel / Sheets Dashboard

- Background fill: `#fafaf8`. Header fill: `#f5f4f0`. Border color: `#d8d4cc`.
- Accent color (key rows, highlighted cells): `#1a2942` bold text on `#f5f4f0`.
- Gold callout: `#c8a96b` background for emphasis cells — use sparingly, max 1–2 cells per table.
- Positive delta: `#1d7d4c`. Negative delta: `#b72b2b`. Never use gold for status.
- Font: system sans-serif (Calibri, Arial). Do not use decorative fonts.

### BI Dashboard

- Canvas background: `#fafaf8`. Card background: `#ffffff`. Card border: `#d8d4cc`.
- Title font: system sans-serif, 18px/700. Heading contrast via size — not color.
- Accent: `#1a2942` for selected state, highlights, and key labels.
- Avoid dark sidebars — this system is light-mode only.
- Tooltip: `#1a2942` background, `#ffffff` text. Keep concise.

---

## Common Mistakes

- Using `accent_secondary` (gold) as a positive status indicator — gold is editorial, not semantic.
- Heavy grid lines on charts — this system uses reduced or no grid for minimal charts.
- Cramming multiple KPIs at the same visual weight — use generous size contrast between primary and secondary metrics.
- Breaking the page content width beyond 860px — it destroys the editorial feel.
- Overly bold headings at every level — contrast comes from size, not weight uniformity.
- Forgetting the print media query — box shadows and background fills break PDF export.
