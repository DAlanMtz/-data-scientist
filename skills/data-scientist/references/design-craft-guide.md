# Design Craft Guide

Use this guide to produce visual reports, dashboards, and data artifacts that look like they came from a skilled human — not from a tool running on defaults. The gap between AI-generated output and professionally crafted output is almost entirely made of small, repeatable decisions about type, space, color, and language.

The goal is not decoration. The goal is signal clarity: the reader should find the finding, trust the evidence, understand the uncertainty, and know what to do next — without wading through visual noise or template scaffolding.

---

## Why AI-Generated Reports Look Generic

AI-generated reports have a consistent fingerprint. Recognizing it is the first step to defeating it.

### Structure fingerprints

- Every section has a heading, every heading uses the same weight, every section looks equally important.
- Bullet points for everything. Nested bullets to show hierarchy. Three levels of nesting in a single finding.
- "Introduction," "Analysis," "Findings," "Conclusion" sections that mirror each other instead of following the decision logic.
- Each section ends with a mini-summary that repeats what was just said.
- The recommendation is the last thing on the page, after everything else.

### Language fingerprints

- Chart titles describe the chart type: "Revenue by Month," "Feature Importance Plot," "Confusion Matrix."
- Captions repeat the axis labels: "This chart shows revenue increasing from January to December."
- Opening phrases: "It is important to note that…", "The data shows…", "Based on the analysis above…"
- Hedging without content: "This may suggest…", "Further analysis could reveal…", "Results should be interpreted with caution."
- Numbered or bulleted recommendations that are never tied to a specific owner, threshold, or date.

### Visual fingerprints

- Default matplotlib figure size (6.4 × 4.8 or 10 × 6 inches).
- Default matplotlib color cycle: the recognizable blue `#1f77b4` followed by orange, green, red, purple.
- DejaVu Sans font in all chart text.
- Full box frame around every chart (all four spines).
- Solid gray grid lines at full opacity.
- Legend always present, even when there are two categories.
- Every chart the same size regardless of information density.
- KPI cards with `font-weight: 700` values but no baseline or target.

### Layout fingerprints

- Everything the same margin. Everything the same card size. No variation in visual weight.
- No breathing room between sections: findings blur together.
- Dashboard that is a uniform grid of equally-sized cards.
- Report that looks like a BI tool screenshot, not a document.

---

## The Three Craft Fundamentals

Fixing AI-generated output requires three things, applied consistently:

### 1. One dominant element per view

Every page, section, and chart should have one thing that is more visually prominent than everything else. If everything is equally weighted, nothing is findable.

- Report page: one dominant visual per section. Supporting charts are smaller, less saturated, or below the fold.
- Dashboard: the KPI strip leads, one trend chart dominates the center, secondary panels are smaller.
- Chart: one line, one bar, or one region is the point of attention. Everything else is context.

### 2. Space as structure

White space is not empty. It groups, separates, and signals hierarchy. A report with consistent, generous spacing looks intentional. A report with tight or inconsistent spacing looks assembled.

- Same spacing between related elements, more spacing between unrelated elements.
- Section headings get more breathing room above than below.
- Chart containers have enough internal padding that the chart doesn't touch the edges.
- The page margin is wider than the gap between columns.

### 3. Restraint in color and text weight

Every additional color or bold element dilutes the ones that were already there. Reserve emphasis for what the viewer actually needs to find.

- One accent color per report. Use it for the most important bar, the reference line, the status chip.
- Bold text only for the number in a KPI card, a key term in a caption, or a severity label.
- No more than three colors in a single chart unless the data structure requires it.
- Use gray and muted tones as the default. Color is the exception, not the rule.

---

## Typography Craft

### Font choice

Use the system UI font stack. It renders beautifully on every platform without loading a web font, and it looks different from both the matplotlib DejaVu Sans and the generic Arial fallback.

```css
font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI",
             "Helvetica Neue", Arial, sans-serif;
```

For monospaced content (data tables, metric values, code):
```css
font-family: "SFMono-Regular", "Cascadia Mono", Menlo, Consolas,
             "Liberation Mono", monospace;
```

For charts in Python, specify fonts explicitly to avoid DejaVu Sans:
```python
"font.sans-serif": ["Helvetica Neue", "Helvetica", "Arial", "DejaVu Sans"]
```

### Type scale

Use a consistent scale. These sizes pair well:

| Use | Size | Weight | Line height |
|---|---|---|---|
| Report title (h1) | 34–36px | 700 | 1.15 |
| Section heading (h2) | 22px | 700 | 1.3 |
| Subsection (h3) | 17px | 600 | 1.4 |
| Body text | 15px | 400 | 1.65 |
| Label / metric name | 13px | 500 | 1.4 |
| Caption / footnote | 12–13px | 400 | 1.5 |
| KPI value | 28–32px | 700 | 1.1 |

### Hierarchy enforcement

- The report title should be noticeably larger than everything else. If h1 and h2 feel the same size, the title is too small or the section heading is too large.
- Section headings should be visually distinct but not compete with the title.
- Labels, captions, and footnotes should feel quieter than body text — reduce their color or size, not just their weight.

### Letter spacing

Use positive letter spacing for uppercase labels and negative letter spacing (or none) for large headings:

```css
.eyebrow { text-transform: uppercase; letter-spacing: 0.06em; font-size: 12px; }
h1 { letter-spacing: -0.01em; }
```

---

## Space and Proportion

### The 8px baseline grid

All spacing should be multiples of 8px (or 4px for fine adjustments). This creates visual regularity even if the viewer can't name it.

```
4px  — micro: between inline elements (icon + text)
8px  — small: inside compact components
12px — inner: card padding at compact size
16px — base: standard internal padding
24px — medium: between components in a group
32px — large: between sections in a column
40px — section gap: between major report sections
48px — page margin: horizontal edge spacing
64px — page section gap: space above major h2 headings
```

### Report vs dashboard proportions

A report should feel like a document: narrow content column, generous margins, clear vertical rhythm. Use 860–900px max content width, not 1200px.

A dashboard should use the full screen: start with a top bar, then a KPI strip, then the main grid. Sidebars are narrow (220–260px), mains are wide.

### Breathing room rules

- Heading gets more space above it than below it (pre-heading margin ≥ 2× post-heading margin).
- KPI value + label + comparison are tightly grouped; next KPI card has a gap.
- Chart title + subtitle belong to the chart, not the section. They should be inside the card, not above it.
- Appendix content uses smaller spacing and smaller type than the main report body.

---

## Color Discipline

### Single accent rule

A report or dashboard should use one accent color for highlights, primary actions, and the most important data element. Every other element defaults to grays and neutrals.

Wrong: five different colored bars for five categories, all fully saturated.
Right: all bars in neutral gray except the one being discussed, which uses the accent color.

### When categories require multiple colors

Use the design token chart sequence defined in `references/chart-style-system.md`. Never use the default matplotlib tab10 or seaborn default palettes in stakeholder-facing output.

Rules for multiple-color charts:
- Cap at 6 categories before grouping into "Other."
- Start with the most important category in the strongest color (accent).
- Put baselines, averages, and reference lines in gray.
- Use the same color for the same category across all charts in the report.

### Semantic color discipline

Status colors (green = good, red = bad, amber = warning) should be used for status only. Do not use green bars just to make a chart look "positive" or red just to make something look concerning.

Use muted, desaturated versions of status colors. Bright `#00ff00` or `#ff0000` reads as "default" or "alarming." Prefer:
- Positive: `#1d7d4c` (forest green)
- Warning: `#a05c0a` (amber-brown)
- Negative: `#b72b2b` (deep red)

### The gray-first principle

Build the chart in gray first. Add color only to the element the viewer needs to find. If the chart still communicates clearly without color, it will work in grayscale, on projectors, and for colorblind viewers.

---

## Chart Polish

These are the specific settings that separate professional charts from defaults.

### Remove the box frame

Professional charts have no top or right spines. The bottom and left axes (or no axes) are enough.

```python
# matplotlib
ax.spines["top"].set_visible(False)
ax.spines["right"].set_visible(False)
# Or use the house rcParams — see chart-style-system.md
```

```r
# ggplot2
theme(panel.border = element_blank())
```

### Thin, light grid lines

Grid lines should be light gray, not default dark gray. They provide measurement reference without visual weight.

```css
grid: #e3e5e8, linewidth 0.4–0.6, axes.axisbelow: True
```

### Direct labels over legends

Legends require the viewer to match color to category by scanning back and forth. Direct labels place the category name next to its line or bar.

Use legends only when direct labels would overlap. When a chart has two lines, label them at the right end. When a chart has three or more bars, use a legend only if bars are grouped.

### Titles as takeaways

Every chart in a stakeholder-facing report should have a title that states the finding, not the chart type.

| Generic (AI default) | Editorial (craft) |
|---|---|
| Revenue by Month | Revenue recovered after March outage but remains below Q4 |
| Feature Importance | Usage frequency is the strongest churn predictor |
| Confusion Matrix at Threshold 0.4 | High recall at 0.4 threshold generates 2× more alerts than capacity supports |

### Subtitles carry the metadata

The subtitle is where the metric definition, population, time window, denominator, and filter go. This frees the title to carry the finding.

```
Title: Renewal risk is concentrated in small accounts
Subtitle: Accounts due for renewal in 90 days; usage change vs prior 30 days; n=1,240
Caption: Accounts with usage down >25% show 3× higher churn rate. Excludes accounts with incomplete telemetry (n=89).
```

### Figure sizes by context

| Context | Width × Height | Use |
|---|---|---|
| Full-width standalone | 10 × 5 in | Main finding, trend, dashboard primary |
| Half-width panel | 6 × 4 in | Segment breakdown, comparison, secondary |
| Small supporting | 5 × 3 in | Diagnostic, appendix, sparkline reference |
| KPI sparkline | 3 × 1.5 in | Inline trend context |
| Print/PDF column | 7 × 3.5 in | Document report |

Export at 200+ dpi (savefig.dpi ≥ 200). Never include rasterized charts at screen resolution in printed reports.

### Axis formatting

- Use readable number formats: `1.2M` not `1200000`, `42%` not `0.4183`.
- Remove redundant zero padding on axes.
- Do not start every chart at zero. Use a reference line or annotation when the baseline matters.
- Rotate x-axis labels only when necessary. Prefer horizontal labels or abbreviated labels.
- Axis titles should be lowercase, concise, and include units.

---

## Editorial Quality

What separates a McKinsey deck, an FT visualization, or an Economist chart from a BI tool export is editorial judgment — every element has been reviewed and either earned its place or been cut.

### The editorial review questions

Before finalizing any visual deliverable, ask:

1. What is the one thing a reader must leave this chart knowing?
2. Does the title state that thing?
3. Is there anything in this chart that doesn't support that thing?
4. Is there anything missing that would make a careful reader doubt the finding?
5. Can a reader with no context understand this chart from title + subtitle + caption alone?

### What editorial quality looks like

- **Annotation over legend.** Key events, thresholds, and reference points are annotated directly on the chart, not explained in surrounding text.
- **Data reduction.** Fewer categories, tighter time windows, aggregated where appropriate. Not every row of data needs to be visible.
- **Consistent visual language.** Same font, same color palette, same grid style, same caption structure across every visual in the report.
- **Asymmetric layout.** The most important visual gets more space. Supporting visuals are smaller. The appendix is visually quiet.
- **Purposeful emphasis.** One thing per chart is highlighted. Not two. Not zero.

### The three-second test

A professional chart should communicate its point within three seconds to someone who has never seen it. If the takeaway requires sustained reading, the chart needs a better title, a stronger visual hierarchy, or a different chart type.

---

## Common AI-Generation Anti-Patterns

### In reports

| Anti-pattern | Fix |
|---|---|
| "It is important to note that…" | Delete. State the caveat directly. |
| Recommendation at the end | Move it to the executive summary or page 1. |
| Every section the same visual weight | Use larger type for main finding sections; quieter for supporting and appendix. |
| Nested bullets 3 levels deep | Flatten to one level. Use prose for nuance. |
| Summary at the end that restates findings | Delete. Readers stop before the end anyway. |
| Metric tables without units or denominators | Always include unit and denominator in column headers. |

### In charts

| Anti-pattern | Fix |
|---|---|
| Default `#1f77b4` blue everywhere | Use the design token palette. |
| DejaVu Sans chart font | Set font.sans-serif to Helvetica/Arial. |
| Top and right spines visible | Remove them. |
| Dense gray grid lines | Use `#e3e5e8` at 0.4–0.6 linewidth. |
| Legend when two categories | Direct label. |
| Title says "Sales by Month" | Title says "Sales recovered in Q3 after H1 decline." |
| Same figure size for every chart | Match size to information density. |

### In dashboards

| Anti-pattern | Fix |
|---|---|
| Uniform grid of identically-sized cards | Vary card sizes by information importance. |
| KPI card with no baseline or target | Every KPI must have a comparison point. |
| Filter bar changes metric definitions silently | Lock definitions; filter only population. |
| Refreshed daily but no freshness indicator | Show "Last updated" in the header. |
| Background color is default BI tool gray | Use warm off-white (`#f7f8f9`) for the page; white for cards. |

---

## Related Files

- `references/visual-report-design-system.md` — design tokens, color palette, type scale, spacing scale
- `references/chart-style-system.md` — Python and R house style code, color constants, export settings
- `references/visual-storytelling-guide.md` — narrative structure, caption writing, decision-first sequencing
- `templates/html-report-template.md` — editorial HTML report with design tokens applied
- `templates/dashboards/html-dashboard-starter-template.md` — dashboard HTML with design tokens applied
