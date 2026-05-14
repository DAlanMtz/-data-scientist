# Anomaly Monitoring Dashboard Template

Use this for anomaly, exception, incident, fraud-signal, data-quality, or operational alert dashboards.

## Anomaly Definition

- Metric or event monitored:
- Expected behavior or baseline:
- Anomaly score/rule:
- Severity rules:
- Entity grain:
- Review cadence:

## Alert Volume

- Total alerts:
- Alerts by severity:
- New vs open vs resolved:
- Alert rate:
- False-positive rate where available:

Recommended visuals: KPI cards, stacked trend, status chips.

## Severity Levels

| Severity | Definition | Response time | Owner |
| --- | --- | --- | --- |
| Critical | `[definition]` | `[SLA]` | `[owner]` |
| High | `[definition]` | `[SLA]` | `[owner]` |
| Medium | `[definition]` | `[SLA]` | `[owner]` |
| Low | `[definition]` | `[SLA]` | `[owner]` |

## Time Trend

- Alerts over time:
- Alert rate normalized by volume:
- Recurring incidents:
- Recent spikes:

## Top Affected Segments / Entities

- Segment/entity:
- Alert count:
- Severity:
- Business impact:
- Owner:

Recommended visuals: ranked bars, heatmap, ranked detail table.

## Investigation Queue

| Entity | Timestamp | Severity | Metric | Expected | Observed | Reason | Status | Owner | Action |
| --- | --- | --- | --- | ---: | ---: | --- | --- | --- | --- |
| `[entity]` | `[time]` | `[severity]` | `[metric]` | `[expected]` | `[observed]` | `[reason]` | `[status]` | `[owner]` | `[action]` |

## False-Positive Review

- Disposition categories:
- False-positive rate by rule/model:
- Rules to adjust:
- Suppression logic:
- Feedback captured for retraining/tuning:

## Status Workflow

Recommended statuses:

- New
- In review
- Escalated
- Resolved
- Dismissed false positive
- Suppressed

## Escalation Rules

- Critical:
- Repeated anomaly:
- Sensitive entity:
- Data quality uncertainty:
- No owner assigned:

## Monitoring Notes

- Label/outcome delay:
- Expected alert volume:
- Known noisy periods:
- Upstream data dependencies:
- Review cadence:

## QA Checks

- [ ] Anomaly definition is explicit.
- [ ] Severity thresholds have owners/actions.
- [ ] Queue includes status and owner.
- [ ] False-positive review is captured.
- [ ] Alert volume is normalized when base volume changes.
- [ ] Escalation path is documented.
