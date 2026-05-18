# Dashboard Output Formats

Use this reference when Step 10 of `workflow/design-preflight.md` asks you to select an output format and apply format-specific constraints. It explains how to adapt the same dashboard or report concept across 8 formats.

A design system choice (from `design-systems/`) is format-agnostic — the same DESIGN.md applies across all formats below. Each format has different constraints on how those tokens are expressed.

---

## Format 1: Markdown Dashboard Spec

**When to use:** Planning artifact, stakeholder alignment, handoff to a developer, or a documentation-grade description of a dashboard that will be built in a BI tool.

**Element map:**

| Dashboard element | Markdown equivalent |
|---|---|
| KPI card | Bold metric name + value in a pipe table or definition list |
| Filter | Noted in a "Filters" section with default values |
| Chart | Described by question, chart type, and data source |
| Section / page | `##` heading |
| Metric definition | Inline footnote or a separate "Metric Glossary" section |
| Freshness indicator | Noted in the header section |

**How to apply design system tokens:** No CSS. Communicate visual intent in prose: "Primary chart uses the clean-saas-analytics categorical palette, first color for the primary series."

**Key constraints:**
- No interactive elements — describe intended behavior.
- Specify default filter values explicitly.
- Include the full Metric/Data Contract block (from `templates/dashboard-discovery-brief-template.md`).
- This is a specification, not a deliverable — label it as such.

**Common mistakes:**
- Treating the markdown spec as the final artifact — it is a planning document.
- Omitting metric definitions in the glossary section.
- Forgetting to specify filter defaults.

---

## Format 2: HTML Dashboard

**When to use:** Self-contained prototype, static stakeholder deliverable, or a dependency-free dashboard that runs in a browser without a backend.

**Element map:**

| Dashboard element | HTML equivalent |
|---|---|
| KPI card | `<article class="card kpi-card">` |
| Filter | `<select>` or `<input>` in a filter strip `<div class="filters">` |
| Chart | `<figure class="chart-container">` with embedded SVG, image, or JS chart |
| Section | `<section>` with `<h2>` heading |
| Status chip | `<span class="chip chip-positive">` etc. |
| Freshness indicator | `<div class="freshness-bar">` in the header |

**How to apply design system tokens:** Apply `:root` CSS custom properties from the selected `DESIGN.md`'s HTML Report or HTML Dashboard section. Swap the token block at the top of `<style>` to change visual direction.

**Key constraints:**
- No external dependencies unless the user chooses a charting library.
- Test in a browser and export to PDF with "print backgrounds" enabled.
- Print media query required for PDF output.
- Use `templates/dashboards/html-dashboard-starter-template.md` as the base.

**Common mistakes:**
- Using hardcoded hex values in components instead of CSS variables — prevents theme swapping.
- No print media query — charts and shadows break in PDF export.
- Relying on a JavaScript framework for a prototype deliverable.

---

## Format 3: PDF-Ready Visual Report

**When to use:** Polished executive report, printed deliverable, attachment to an email or slide deck, or a document that must be archived.

**Element map:**

| Report element | PDF equivalent |
|---|---|
| KPI | Large numeric display in a white section block |
| Chart | Static exported image at 300 DPI |
| Table | Formatted table with caption above |
| Section | Page-level section with clear heading |
| Footnotes | Below-table or end-of-document text |
| Metric definition | Footnote or appendix glossary |

**How to apply design system tokens:** Use the HTML Report format with print media query active. Override CSS for print: remove box shadows, set `background: white` on cards, embed chart images rather than using interactive JS.

**Key constraints:**
- Charts must be static (PNG or SVG at 300 DPI for print).
- Page breaks must not split a chart and its caption.
- All fonts must be web-safe or embedded (system-ui is safe).
- For `executive-editorial`: apply the warm cream background (`#fafaf8`) on screen; revert to white for print.

**Common mistakes:**
- Exporting charts at screen resolution (72 DPI) — they become blurry in print.
- Page breaks splitting a chart from its caption.
- Using dark-mode design systems for print — dark backgrounds in print are expensive and unreadable.
- Forgetting to test the PDF by actually printing or exporting.

---

## Format 4: Slide / Deck Layout

**When to use:** Live presentation to an audience, stakeholder readout, or a document that will be screen-shared.

**Element map:**

| Dashboard element | Slide equivalent |
|---|---|
| KPI | Large number in the center or upper-left of the slide |
| Chart | One chart per slide, full-bleed or centered |
| Section | Divider slide with section title only |
| Finding | Slide headline — the most important sentence |
| Detail | Speaker notes, not on the slide |
| Table | Summary table, max 5 columns and 6 rows |

**How to apply design system tokens:** Set the slide theme background color, accent, and font to match the selected design system. In PowerPoint/Keynote: use the slide master. In Google Slides: set theme colors and fonts.

**Key constraints:**
- Maximum 3 visuals per slide.
- Slide headline = caption = the finding. "Revenue declined 8% in Q3, driven by Europe."
- No more than 6 words in a slide headline. Findings belong in the headline, not bullet points.
- Detail and caveats belong in speaker notes.
- One font size for body text — do not vary within a slide.

**Common mistakes:**
- Bullet-pointed analysis that should be a chart.
- Chart title repeating the slide headline — redundant.
- Dark-mode design systems in slide decks viewed on projectors — projectors wash out dark backgrounds.
- Missing the finding in the headline (using the label "Q3 Revenue" instead of the insight).

---

## Format 5: Notebook Visual Section

**When to use:** Embedded visual section within an analysis notebook (Jupyter, R Markdown, Quarto, Observable). The dashboard/report is part of a larger analysis document.

**Element map:**

| Dashboard element | Notebook equivalent |
|---|---|
| KPI | A `print()` or display block before the first chart |
| Chart | Code cell + output |
| Caption / takeaway | Markdown cell immediately below the chart cell |
| Section | Markdown `##` heading cell |
| Metric definition | Markdown cell before the chart section |
| Freshness | A comment or display at the top of the section |

**How to apply design system tokens:** Apply `HOUSE_RCPARAMS` (from `references/chart-style-system.md`) with the selected design system's chart overrides at the top of the notebook or section. Use `mpl.rcParams.update(...)` in Python or `theme_house()` in R.

**Key constraints:**
- Every chart cell must be followed by a markdown takeaway cell.
- Do not reuse the chart title as the takeaway — the takeaway should extend or interpret it.
- Apply `rcParams` at the notebook level, not per-chart.
- Separate exploratory cells from communication cells — exploratory charts do not need full craft treatment.

**Common mistakes:**
- No markdown takeaway after the chart.
- `rcParams` applied in the wrong cell (after chart creation instead of before).
- Exploratory diagnostic charts mixed into the stakeholder-facing narrative section without labels.

---

## Format 6: Streamlit / Shiny App

**When to use:** Interactive analytics application with filters, dynamic charts, and user controls. Appropriate when the audience needs real-time or near-real-time exploration.

**Element map:**

| Dashboard element | App equivalent |
|---|---|
| KPI card | `st.metric()` (Streamlit) or `valueBox()` (Shiny) |
| Filter | `st.selectbox()` / `st.slider()` (Streamlit) or `selectInput()` (Shiny) |
| Chart | `st.plotly_chart()` / `st.pyplot()` or `renderPlot()` |
| Section | `st.header()` / `st.subheader()` or `tags$h2()` |
| Status | `st.success()` / `st.warning()` / `st.error()` (Streamlit) or custom HTML |
| Freshness | `st.caption()` or sidebar footer |

**How to apply design system tokens:** Map DESIGN.md tokens to the app's theme configuration. In Streamlit: set `primaryColor`, `backgroundColor`, `secondaryBackgroundColor`, `textColor` in `.streamlit/config.toml`. In Shiny: use `bslib::bs_theme()` to set `bg`, `fg`, `primary`, `secondary`. Do not hardcode hex values in app component calls — use the config system.

**Key constraints:**
- Map tokens to the theme config, not to individual component calls.
- Test the app with filters applied — ensure no blank chart states occur without informative messages.
- Performance: apply `@st.cache_data` or `reactive()` caching for heavy queries.
- Dark-mode tokens (operational-command-center, financial-terminal) require full dark theme config.

**Common mistakes:**
- Hardcoding hex colors in `st.metric()` or chart calls instead of using the theme.
- No caching on data-heavy operations.
- No empty-state messages on filtered charts.
- Interactive features that do not apply to the actual decision use case.

---

## Format 7: Excel / Sheets Dashboard

**When to use:** Business stakeholders who prefer spreadsheet tools, dashboards that need to be distributed without a browser, or output that will be printed from a spreadsheet.

**Element map:**

| Dashboard element | Excel/Sheets equivalent |
|---|---|
| KPI card | Merged cell range with large value + label below |
| Chart | Embedded chart object from the data range |
| Filter / slicer | Excel Slicer or Sheets filter view |
| Section | Distinct worksheet tab or colored section header row |
| Status | Conditional formatting rule |
| Metric definition | Cell comment, footnote row, or a "Definitions" tab |
| Freshness | A cell in the header area: "Last updated: [formula]" |

**How to apply design system tokens:** Create a named styles sheet (or Excel cell styles) for:
- `KPI_Value`: large font, bold, design system text_primary color
- `KPI_Label`: small font, uppercase, text_secondary
- `Row_Positive`: green text (`positive` token value)
- `Row_Negative`: red text (`negative` token value)
- `Section_Header`: surface_alt fill, bold, border bottom

**Key constraints:**
- Protect raw data sheets — dashboards should read from data, not contain data.
- Conditional formatting: tie to named styles, not ad-hoc formats.
- Slicers: set default values to match the most common workflow.
- Formulas: no volatile functions (`NOW()`, `RAND()`) in dashboard cells that recalculate on every keystroke.

**Common mistakes:**
- Mixing raw data and dashboard views in the same sheet.
- Conditional formatting applied with hardcoded colors instead of named styles.
- No "Last updated" cell — users cannot tell if the data is current.
- Charts with default Excel color schemes — replace with design system palette manually.

---

## Format 8: BI Tool Specification

**When to use:** The dashboard will be built in Power BI, Tableau, Looker, Metabase, Superset, or another BI tool. The spec is a handoff document or a direct implementation guide.

**Element map:**

| Dashboard element | BI tool equivalent |
|---|---|
| KPI card | KPI tile / metric card / scorecard visual |
| Chart | Visualization / chart pane |
| Filter | Filter pane / parameter / quick filter |
| Section / page | Report page / dashboard tab |
| Status | Conditional formatting / alert rule |
| Metric definition | Field description / calculated field comment |
| Freshness | Data source last-refresh timestamp tile |

**How to apply design system tokens:** Map DESIGN.md tokens to the tool's theme system:
- **Power BI**: Custom theme JSON (`theme.json`). Set `background`, `foreground`, `tableAccent`, and `dataColors` from DESIGN.md tokens.
- **Tableau**: Workbook formatting and color palette XML. Set background, text, and grid colors.
- **Looker**: LookML `color_palette` parameter in the manifest; Explore/Dashboard tile backgrounds.
- **Metabase / Superset**: Dashboard-level color settings; chart color arrays.

Translate DESIGN.md tokens to tool-specific fields. Document the mapping so the theme can be reproduced.

**Key constraints:**
- Document metric definitions as field descriptions in the tool — not just in the discovery brief.
- Row-level security: test that security rules apply before certifying the dashboard.
- Freshness: connect the dashboard's refresh indicator to the tool's data source metadata.
- Export: verify that PDF/image exports render correctly before publishing.

**Common mistakes:**
- Building the dashboard before documenting metric definitions in the tool.
- Row-level security untested before publish.
- Default BI tool color schemes — always override with design system palette.
- No freshness tile — users cannot tell if the data is stale.
- Publishing without testing the PDF export.

---

## Format Selection Summary

| Format | Interactive | Print-ready | Needs backend | Best for |
|---|---|---|---|---|
| Markdown spec | No | No | No | Planning, handoff |
| HTML dashboard | Filter-only | With print CSS | No | Prototypes, static deliverables |
| PDF visual report | No | Yes | No | Executive print |
| Slide deck | No | Yes | No | Live presentations |
| Notebook section | Code-only | With export | No | Analysis notebooks |
| Streamlit / Shiny | Yes | No | Yes | Interactive apps |
| Excel / Sheets | Filter/slicer | Yes | No | Spreadsheet-first audiences |
| BI tool | Yes | With export | Yes | Recurring operational dashboards |
