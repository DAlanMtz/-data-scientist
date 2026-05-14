# Visual Report Design System

Use this default design system for professional analytics reports, dashboards, and exported visual deliverables when the user has not supplied a brand system. Users can override fonts, colors, spacing, or examples with their own brand standards.

The design principle is decision-first: the layout should make the supported decision, strongest evidence, and recommended action easier to find than everything else.

## Design Priorities

- Put the decision and answer before supporting detail.
- Use hierarchy so the most important information is visually easiest to scan.
- Keep views simple: avoid decorative complexity, excess colors, and chart dumps.
- Group related metrics and repeat layout patterns consistently.
- Use captions as takeaways, not generic labels.
- Make uncertainty, filters, freshness, and limitations visible when they affect interpretation.

## Typography Hierarchy

Use a clear hierarchy even if the output is markdown, HTML, notebook, BI dashboard, slide deck, or spreadsheet.

- Report title: short, decision-relevant, largest text on the page.
- Section heading: names the business question or decision area.
- Chart title: states the insight or question answered.
- Chart subtitle: defines population, time window, metric, denominator, and filters.
- Caption/takeaway: explains why the viewer should care and what action may change.
- Footnote: method, caveat, source, or definition detail.

Avoid using chart titles like "Revenue by Month" when a takeaway is available. Prefer "Revenue recovered after March outage but remains below Q4 baseline."

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

- Use neutral colors for most structure and text.
- Reserve strong colors for status, alerts, highlights, or selected categories.
- Keep categorical palettes small and consistent across pages.
- Do not change category colors between charts.
- Avoid rainbow palettes and decorative gradients.
- Use direct labels where legends become hard to scan.

## Semantic Color Rules

If using semantic colors, keep meanings stable:

- Green: favorable status, target met, improvement.
- Red: risk, alert, target missed, harm, decline.
- Amber/yellow: warning, needs review, incomplete.
- Blue: neutral primary highlight or selected state.
- Gray: baseline, inactive, missing, historical context.

Do not use red/green alone to convey meaning. Pair color with text, icons, labels, or patterns.

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
