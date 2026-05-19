# Dashboard Template Library

Reusable HTML/CSS dashboard templates for the `dashboard-designer` sub-skill. Each template is a standalone, dependency-free reference layout using tokenized CSS. Use these as starting points — adapt copy, metrics, and sections to the user's actual data and context.

---

## Template Families

| Template | Variant | When to use |
|---|---|---|
| `analytical-research-dashboard-full.html` | Full | Research evaluation, benchmark comparison, method comparison, segment evidence, readiness assessment, caveats, and recommendations — complete diagnostic view |
| `analytical-research-dashboard-compact.html` | Compact | First-screen analytical summary, evaluation overview, or triage of research findings |
| `executive-kpi-dashboard-full.html` | Full | Executive KPI review, target tracking, business question dashboard, top drivers, risk/opportunity callouts, and recommended actions — full narrative |
| `executive-kpi-dashboard-compact.html` | Compact | One-screen leadership summary, status at a glance, priority action |
| `model-monitoring-dashboard-full.html` | Full | Deployed or scheduled model health — alerts, performance trend, data quality, drift/feature health, calibration/threshold status, retraining/rollback notes |
| `model-monitoring-dashboard-compact.html` | Compact | Operational model status summary, key health signals, alert triage |
| `experiment-ab-test-dashboard-full.html` | Full | A/B tests and holdouts — treatment/control comparison, sample balance, guardrails, statistical readiness, segment effect stability, and rollout/continue/stop decision |
| `experiment-ab-test-dashboard-compact.html` | Compact | Experiment status summary, primary metric result, guardrail check, decision |
| `data-quality-audit-dashboard-full.html` | Full | Dataset and source readiness — validation checks, completeness, validity, duplicates, freshness, referential integrity, field-level issues, blocking remediation, and audit actions |
| `data-quality-audit-dashboard-compact.html` | Compact | Source readiness summary, critical failures, remediation priority |
| `forecast-planning-dashboard-full.html` | Full | Forecasts and scenario planning — uncertainty ranges, forecast windows, baseline comparisons, drivers, segment planning watchlists, forecast accuracy/backtest summaries, caveats, and planning actions |
| `forecast-planning-dashboard-compact.html` | Compact | Forecast status, primary scenario, key assumptions, planning action |

---

## Full vs Compact

| | Full | Compact |
|---|---|---|
| **Use when** | Complete review, deep evidence, diagnostics, appendix, production reference | Overview, one-screen summary, executive/triage view, constrained space |
| **Sections** | All sections including diagnostics, evidence tables, field-level detail, appendix | Header + KPIs + status + key finding + recommended action |
| **Audience** | Analyst, reviewer, technical stakeholder requiring full context | Executive, triage reviewer, status consumer |
| **Token economy** | Full — all components present | Constrained — fewer sections, shorter tables |

---

## Archetype Selection Guide

| User request signals | Template family |
|---|---|
| Research evaluation, analytical investigation, benchmark, method comparison, segment evidence, readiness | `analytical-research` |
| Executive KPI, leadership summary, target tracking, business question, drivers, risk/opportunity | `executive-kpi` |
| Deployed model health, model alerts, performance trend, data quality, drift, calibration, retraining | `model-monitoring` |
| A/B test, holdout, treatment/control, experiment, guardrails, rollout decision | `experiment-ab-test` |
| Data quality, source readiness, validation checks, completeness, freshness, remediation | `data-quality-audit` |
| Forecast, scenario planning, uncertainty, planning window, assumptions, backtest accuracy | `forecast-planning` |

---

## Shared Standards

All templates in this library follow these standards:

- **Domain-neutral placeholders** — no real product names, real metrics, or real claims
- **Visible denominators** — rates, percentages, lift, accuracy, drift, validity, completeness, confidence intervals, and forecast ranges always show sample size or denominator
- **Caveats and freshness visible** — limitations and data freshness always appear in context
- **Recommended action visible** — every template surfaces a clear action or decision
- **Tokenized CSS** — all visual properties use CSS custom properties (`--bg`, `--accent`, `--positive`, etc.); swap the `:root` block to change the design system
- **No external dependencies** — no CDN links, no external scripts, no web fonts loaded from external sources
- **Static HTML/CSS only** — no JavaScript; interactive elements use native `<details>/<summary>`
- **No real claims** — all copy is placeholder; do not commit templates with real data

---

## Cleanup Rule

Templates in this directory must not contain OpenDesign export artifacts. Before committing any new or updated template, verify:

```bash
grep -l "data-od-sandbox-shim\|data-od-snapshot-bridge\|data-od-srcdoc-transport-activation\|data-od-id" *.html
```

If any matches are found, re-run the cleanup script before committing.
