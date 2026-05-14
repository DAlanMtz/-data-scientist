# Visual Report Template

Use this template for stakeholder-facing visual reports, executive readouts, PDF/web reports, notebook narratives, or slide-style analysis summaries. The report should be decision-first: every chart must answer a question or change the viewer's next action.

## 1. Title And Metadata

- **Report title:** `[Decision-relevant title]`
- **Prepared for:** `[Audience / stakeholder]`
- **Prepared by:** `[Owner]`
- **Date:** `[Date]`
- **Data freshness:** `[Latest data timestamp / extract date]`
- **Status:** `[Draft / reviewed / final]`

## 2. Audience

- Primary audience:
- Secondary audience:
- Expected level of technical detail:
- Decisions this audience can make:

## 3. Decision Supported

- Primary decision:
- Decision cadence:
- Action options:
- Cost of wrong action:
- Deadline or operating window:

## 4. Business Question

State the question in plain language.

Example:

> Which segments should receive intervention next month, and what evidence supports prioritizing them?

## 5. Data Used

| Source | Grain | Date range | Refresh/freshness | Key limitations |
| --- | --- | --- | --- | --- |
| `[source]` | `[row/entity grain]` | `[range]` | `[freshness]` | `[coverage caveat]` |

Include metric definitions, denominators, filters, and exclusions that affect interpretation.

## 6. Executive Visual Summary

Use 1-3 visuals or KPI cards.

For each:

- **Visual:** `[Chart/KPI/table name]`
- **Question answered:** `[Question]`
- **Takeaway title:** `[Insight, not chart type]`
- **Decision implication:** `[What should change]`
- **Caveat:** `[Uncertainty / limitation]`

## 7. Key Metrics

| Metric | Definition | Current value | Baseline/target | Direction | Decision use |
| --- | --- | ---: | ---: | --- | --- |
| `[metric]` | `[definition]` | `[value]` | `[target]` | `[up/down/stable]` | `[how used]` |

Rules:

- Use consistent date ranges.
- Include denominators for rates.
- Avoid metrics without a decision use.

## 8. Visual Story Sequence

Use this structure unless the audience needs a different sequence.

1. **Context:** population, baseline, scope.
2. **Main finding:** the visual that answers the business question.
3. **Driver/segment:** where the pattern is strongest or weakest.
4. **Trend or stability:** whether the pattern is persistent.
5. **Tradeoff/uncertainty:** cost, risk, confidence, interval, or sensitivity.
6. **Recommendation:** action and expected impact.

## 9. Chart Inventory

| Section | Chart | Question answered | Metric/denominator | Owner | Keep/remove |
| --- | --- | --- | --- | --- | --- |
| `[section]` | `[chart]` | `[question]` | `[metric]` | `[owner]` | `[keep/remove]` |

Remove charts that do not answer a question, validate a risk, or support a decision.

## 10. Findings By Section

### Finding 1: `[Takeaway headline]`

- Evidence:
- Visual(s):
- Population and time window:
- Business implication:
- Limitation:
- Next action:

### Finding 2: `[Takeaway headline]`

- Evidence:
- Visual(s):
- Population and time window:
- Business implication:
- Limitation:
- Next action:

## 11. Captions And Takeaways

Use this pattern under every stakeholder-facing visual:

> `[Metric] is [higher/lower/changing] for [population/segment] during [period], which implies [decision-relevant action or risk]. Caveat: [limitation/uncertainty].`

Caption checklist:

- [ ] States the insight, not just the chart type.
- [ ] Includes denominator, time window, and filters when relevant.
- [ ] Avoids causal language unless supported by design.
- [ ] Explains the decision implication.

## 12. Limitations

- Data coverage:
- Missingness or quality concerns:
- Sample size or uncertainty:
- Metric definition limitations:
- Causal limitations:
- Operational constraints:

## 13. Recommendation

- Recommended action:
- Evidence:
- Expected impact:
- Risks:
- Owner:
- Timing:
- How success will be measured:

## 14. Appendix / Method Notes

Include only details needed for review:

- Data definitions.
- Query or extraction logic.
- Model or statistical method.
- Validation or sensitivity checks.
- Full tables.
- Diagnostic visuals.

## 15. Quality Checks

- [ ] Decision supported is explicit.
- [ ] Every chart maps to a question.
- [ ] Main finding appears before supporting detail.
- [ ] Captions state takeaways.
- [ ] Colors, labels, filters, and metric definitions are consistent.
- [ ] Uncertainty and limitations are visible.
- [ ] Exported report is readable on the target medium.
- [ ] Recommendation includes owner and next action.

## Related References And Checklists

- `references/visual-report-design-system.md`
- `references/visual-storytelling-guide.md`
- `references/visualization-guide.md`
- `templates/visual-analysis-workflow.md`
- `checklists/visual-report-checklist.md`
