# Visual Report Checklist

Use this checklist before sharing a stakeholder visual report, executive readout, notebook narrative, PDF, web report, or slide-style analysis summary.

## Audience And Decision

- [ ] Audience is named.
- [ ] Decision supported is explicit.
- [ ] Recommended action is clear.
- [ ] Report scope, time window, and population are stated.
- [ ] Technical detail matches the audience.

**Minimum acceptable standard:** A reader can tell what decision the report supports within the first page or first screen.

## Question-To-Chart Mapping

- [ ] Every chart answers a specific question.
- [ ] No chart is included only because it was created during analysis.
- [ ] Chart inventory includes metric, denominator, population, and decision use.
- [ ] Exploratory, diagnostic, and final communication visuals are not mixed without labels.

**Red flag:** More charts than findings, with no clear main message.

## Visual Hierarchy

- [ ] Main finding appears first.
- [ ] KPI cards or executive visuals are limited to the most important metrics.
- [ ] Supporting detail follows the decision sequence.
- [ ] Appendix detail is separated from main narrative.
- [ ] Layout makes the reading path obvious.

## Chart Correctness

- [ ] Chart type matches the question.
- [ ] Denominators are correct.
- [ ] Aggregations match the intended grain.
- [ ] Missing values are handled and disclosed where relevant.
- [ ] Recent incomplete periods are excluded or clearly labeled.
- [ ] Sample sizes are shown for small groups.

## Axis And Scale Checks

- [ ] Axes are labeled with units.
- [ ] Scale choices do not exaggerate differences.
- [ ] Log scales are disclosed.
- [ ] Dual axes are avoided unless absolutely necessary and clearly explained.
- [ ] Time intervals are evenly represented or gaps are visible.

## Color Usage

- [ ] Colors are consistent across charts.
- [ ] Semantic colors have stable meanings.
- [ ] Color is not the only way status is encoded.
- [ ] Palette is simple and not decorative.
- [ ] Highlight color is reserved for the point of attention.

## Caption Quality

- [ ] Chart titles or captions state the insight.
- [ ] Captions include time window, population, and caveat where relevant.
- [ ] Captions explain the decision implication.
- [ ] Causal language is avoided unless causal design supports it.

**Strong practice:** Every major visual can be understood from title, subtitle, and caption without reading surrounding paragraphs.

## Uncertainty And Limitations

- [ ] Key uncertainty is visible.
- [ ] Forecasts include intervals when appropriate.
- [ ] Small-sample findings are labeled as exploratory.
- [ ] Data quality limitations are documented.
- [ ] Limitations are not hidden after the recommendation if they affect the decision.

## Accessibility

- [ ] Text is readable at the delivery size.
- [ ] Color contrast is sufficient.
- [ ] Labels and legends are clear.
- [ ] Visuals are understandable in grayscale when exported.
- [ ] Alt text or written takeaways are provided when needed.

## Export And Readability

- [ ] PDF, HTML, slide, notebook, or spreadsheet output has been reviewed in final form.
- [ ] Charts do not become blurry or unreadable after export.
- [ ] Tables fit the target medium.
- [ ] Source, freshness, and definitions are available.
- [ ] Page breaks do not split key chart-caption pairs.

## Recommendation Clarity

- [ ] Recommendation follows from the evidence shown.
- [ ] Owner, timing, and next action are named.
- [ ] Expected impact or tradeoff is stated.
- [ ] Measurement plan or follow-up check is included.

## Related Files

- `references/design-craft-guide.md` — craft principles and AI anti-pattern reference; use before finalizing any stakeholder-facing visual
- `references/chart-style-system.md` — matplotlib/ggplot2/Plotly house style; apply to all Python and R charts
- `references/visual-report-design-system.md` — design token reference (hex values, type scale, spacing, palette)
- `references/visual-storytelling-guide.md` — narrative structure, caption writing, decision-first sequencing
- `templates/visual-report-template.md` — markdown report structure template
- `templates/html-report-template.md` — polished HTML report with design tokens applied
