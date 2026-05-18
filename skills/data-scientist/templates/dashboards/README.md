# Dashboard Template Library

Use this library when the user asks to design, generate, review, or prototype a dashboard. Start with the decision and audience, then choose the closest template. Adapt the template to the user's tool: HTML/CSS, React/Tailwind, Python Streamlit, R Shiny/flexdashboard, Excel/Sheets, Tableau, Power BI, notebook dashboards, or another BI/app platform.

## How To Choose

- Use `analytics-dashboard-template.md` for general metric exploration and analysis.
- Use `executive-kpi-dashboard-template.md` for leadership decisions and one-screen summaries.
- Use `model-performance-dashboard-template.md` for ML/model monitoring and validation dashboards.
- Use `forecasting-dashboard-template.md` for time-series actuals, forecast accuracy, and planning.
- Use `cohort-retention-dashboard-template.md` for retention, repeat behavior, lifecycle, and cohort views.
- Use `anomaly-monitoring-dashboard-template.md` for alerting, exceptions, triage, and monitoring queues.
- Use `html-dashboard-starter-template.md` when the user asks for a self-contained dashboard prototype.

## Business Need Mapping

| Business need | Dashboard template | Related references/checklists |
| --- | --- | --- |
| Explore performance by metric, segment, and trend | `analytics-dashboard-template.md` | `references/dashboard-layout-patterns.md`, `references/dashboard-component-patterns.md`, `checklists/dashboard-qa-checklist.md` |
| Give leadership a status and action summary | `executive-kpi-dashboard-template.md` | `references/visual-report-design-system.md`, `references/visual-storytelling-guide.md`, `checklists/visual-report-checklist.md` |
| Monitor model quality, drift, calibration, and errors | `model-performance-dashboard-template.md` | `references/model-monitoring-and-drift.md`, `references/dashboard-component-patterns.md`, `checklists/deployment-checklist.md` |
| Compare forecasts to actuals and manage planning exceptions | `forecasting-dashboard-template.md` | `templates/forecasting-workflow.md`, `checklists/forecasting-checklist.md` |
| Track retention, repeat usage, churn, or lifecycle behavior | `cohort-retention-dashboard-template.md` | `examples/sql/cohort-retention-analysis.md`, `references/dashboard-layout-patterns.md` |
| Triage anomalies, exceptions, incidents, or suspicious activity | `anomaly-monitoring-dashboard-template.md` | `templates/anomaly-detection-workflow.md`, `checklists/anomaly-detection-checklist.md` |
| Prototype a static dashboard without external dependencies | `html-dashboard-starter-template.md` | `references/visual-report-design-system.md`, `checklists/dashboard-qa-checklist.md` |

## Selection Rules

- If the dashboard is recurring, start with `templates/dashboard-design-brief-template.md`.
- If the dashboard is already built, start with `templates/dashboard-qa-checklist-template.md`.
- If the output is a static stakeholder deliverable rather than an operating dashboard, use `templates/visual-report-template.md` or `templates/html-report-template.md`.
- If multiple templates apply, use one primary template and borrow sections from the others. Do not overload one dashboard with every view.

## Visual Direction

Dashboard archetypes define the **structure and content** of a dashboard — what sections to include, what questions to answer, what data to surface. Design systems define the **visual personality** — typography, color, spacing, and chart style.

Choose a design system from `design-systems/README.md` after selecting the archetype. The two decisions are independent.

| Design system | Best for |
| --- | --- |
| `clean-saas-analytics` | General analytics dashboards (default) |
| `executive-editorial` | Stakeholder reports, print/PDF output |
| `operational-command-center` | Monitoring, alerting, incident dashboards (dark mode) |
| `research-paper` | Academic reports, methodology writeups |
| `financial-terminal` | Finance, risk, trading dashboards (dark mode) |
| `warm-narrative` | Explanatory reports, non-technical audiences |

Each system's `DESIGN.md` is standalone — it contains the full token summary, chart style overrides, and format-specific guidance. Apply it directly without reading any other file.

## Component Recipes

The templates in this folder define dashboard **intent**: what sections to include, what questions to answer, and what data to surface. They are tool-flexible and format-agnostic.

For copy-paste-complete **HTML/CSS component recipes** — KPI strip, status chips, metric color cells, verdict bands, stability heatmaps, comparison tables, and collapsible appendix patterns — use `subskills/dashboard-designer/`. The sub-skill also provides opinionated archetype layouts and an assembly guide that maps design-preflight outputs into finished dashboard structure.
