---
name: dashboard-designer
description: Use when producing a stakeholder-facing HTML dashboard, dashboard prototype, or dashboard redesign. Provides copy-paste-complete component recipes, layout patterns, and assembly guidance. Requires parent data-scientist design preflight context before use.
---

# Dashboard Designer

## Purpose

This sub-skill provides concrete implementation patterns for building stakeholder-facing dashboards. The parent `data-scientist` skill handles analytical methodology, design system selection, metric definitions, and design preflight. This sub-skill takes those decisions as inputs and turns them into correctly structured, decision-led HTML.

The sub-skill's primary deliverable is a component library: proven HTML/CSS patterns that can be assembled into publish-quality dashboards without improvising layout, token names, or chip semantics from scratch.

## When To Use This Sub-Skill

Use this sub-skill when:

- The request is to generate, redesign, polish, or QA a stakeholder-facing dashboard.
- The output is an HTML dashboard, dashboard prototype, or dashboard layout spec.
- Design preflight has at least identified: audience, decision supported, artifact type, dashboard archetype, and design system.
- Metric definitions and data grain are known or stated explicitly as assumptions.

## When Not To Use This Sub-Skill

Do not use this sub-skill for:

- Quick EDA charts or internal exploratory plots.
- One-off model diagnostic charts (calibration curves, residual plots, confusion matrices).
- Written narrative reports that do not include dashboard components.
- Data quality audits without a dashboard deliverable.
- General modeling methodology or validation work.

For those, stay in the parent `data-scientist` skill.

## Relationship to Parent Skill

This sub-skill does not replace the parent skill's workflow — it extends it for the dashboard implementation step.

| Responsibility | Owner |
|---|---|
| Framing, audience, decision definition | Parent skill |
| Design system selection and token values | Parent skill (`design-systems/`) |
| Design preflight protocol | Parent skill (`workflow/design-preflight.md`) |
| Metric definitions and data contract | Parent skill (`templates/dashboard-discovery-brief-template.md`) |
| Self-critique rubric | Parent skill (`checklists/dashboard-self-critique-checklist.md`) |
| KPI strip, chip vocabulary, heatmap patterns | **This sub-skill** (`components/`) |
| Dashboard assembly and section sequencing | **This sub-skill** (`workflow/assembly-guide.md`) |
| Opinionated archetype layouts | **This sub-skill** (`archetypes/`) |

## Required Parent Preflight Context

Before using this sub-skill, confirm these inputs from the parent design preflight:

1. **Audience and decision cadence** — Who uses this? What action does it support?
2. **Decision supported** — One sentence: "This dashboard helps [audience] decide [decision]."
3. **Artifact type** — Dashboard (interactive/recurring) or visual report (static/narrative)?
4. **Dashboard archetype** — Which pattern fits? See `archetypes/` below.
5. **Design system** — Which system's tokens apply? Default: `clean-saas-analytics`.
6. **KPI hierarchy** — Primary (1–3), secondary, diagnostic metrics.
7. **Metric definitions and data contract** — All KPIs defined; data grain, freshness, caveats noted.

If any of these are missing, return to the parent skill's `workflow/design-preflight.md` to complete them before proceeding.

## Dashboard Assembly Workflow

1. **Confirm preflight context.** Verify all 7 inputs above are present. If not, surface the gap and resolve it first.
2. **Choose archetype.** Match the dashboard purpose to an archetype in `archetypes/`. The archetype defines section composition — what sections to include and in what order.
3. **Load design system tokens.** Open `../../design-systems/<name>/DESIGN.md`. Copy the Token Summary into the `<style>` block. Use the correct CSS custom property names from `components/token-setup.md` — do not invent new names.
4. **Select needed components.** Choose the components from `components/` that match the sections in the archetype. Each component file is self-contained and copy-paste complete.
5. **Assemble the first screen.** The first screen must answer the supported decision. Lead with: verdict band (if a recommendation is required) → KPI strip → primary section with takeaway header. Do not put more than 5 cards in the KPI strip. Do not put diagnostic content on the first screen.
6. **Add secondary and diagnostic sections.** Use takeaway-first section headers throughout. Secondary sections provide driver decomposition and segment context. Diagnostic sections expose data quality, coverage, and stability.
7. **Move long tables and methodology into the collapsible appendix.** Any table over 15 rows, any feature-level diagnostic, any raw data listing, and any methodology note belongs in a `<details>` appendix. See `components/collapsible-appendix.md`.
8. **Apply accessibility and responsive rules.** Every interactive element has a label or title. Color is not the only encoding. The layout degrades gracefully at 800px. Print styles suppress nav and interactive elements.
9. **Run the self-critique checklist.** Open `../../checklists/dashboard-self-critique-checklist.md`. Score all 5 dimensions. Fix any dimension below 4 before delivering. Analytical Integrity below 4 is blocking.

## Component Library

Load only the components needed. Each file is standalone.

| Component | File | Use when |
|---|---|---|
| CSS token setup | `components/token-setup.md` | Starting any dashboard — must apply first |
| KPI strip | `components/kpi-strip.md` | Summarizing 3–5 decision-critical metrics at the top |
| Status chips | `components/status-chips.md` | Classifying entities, families, models, or states |
| Metric color cell | `components/metric-color-cell.md` | Color-coding values in tables or heatmaps |
| Verdict band | `components/verdict-band.md` | Surfacing a top-level recommendation or conclusion |
| Section header | `components/section-header.md` | Every section that contains a finding |
| Stability heatmap | `components/stability-heatmap.md` | Showing metric or WR stability across time × group |
| Comparison table | `components/comparison-table.md` | Comparing multiple approaches, models, or strategies |
| Collapsible appendix | `components/collapsible-appendix.md` | Progressive disclosure of diagnostic or raw content |
| Coverage bar | `components/coverage-bar.md` | Showing data completeness, feature availability, readiness |
| Filter bar | `components/filter-bar.md` | Allowing group/segment filtering in heatmaps or tables |

## Archetype Routing

| Dashboard purpose | Archetype |
|---|---|
| Research findings, model results, analytical conclusions | `archetypes/analytical-research-dashboard.md` |
| Leadership status summary, KPI reporting, decisions | `archetypes/executive-kpi-dashboard.md` |
| ML model health, drift, calibration, performance tracking | `archetypes/model-monitoring-dashboard.md` |

For dashboards not covered by these three, use `analytical-research-dashboard.md` as the default structure and adapt sections as needed.

## Output Standards

A dashboard produced with this sub-skill must meet:

- **Decision-led first screen.** A viewer can answer the supported decision within the first visible screen.
- **Correct token names.** CSS custom properties match `components/token-setup.md` — no invented names.
- **Takeaway-first section titles.** Every section header states the finding, not the chart type.
- **Semantic chips.** Status chips use the vocabulary from `components/status-chips.md`. Colors are not assigned arbitrarily.
- **Progressive disclosure.** Diagnostic and raw detail tables are in collapsible `<details>` elements, not in the primary view.
- **Metric/data contract visible.** Metric definitions, freshness, and data grain appear in the footer or a visible metadata line.
- **Self-critique score ≥ 4 on all 5 dimensions.** Analytical Integrity below 4 is blocking.

## Common Mistakes to Avoid

**Token mistakes**
- Using `--green`, `--blue`, `--panel`, `--ink`, `--card-bg`, or other invented names instead of the canonical token set.
- Using a font family other than `system-ui` for clean-saas-analytics (do not substitute Inter or Roboto).
- Hardcoding hex values throughout the CSS instead of using custom properties.

**Content mistakes**
- Putting a recommendation inside a KPI card. Recommendations belong in the verdict band near the header.
- Using label-style section titles ("Monthly Stability") instead of takeaway-first ("April is the weakest month in 4 of 6 groups").
- Putting more than 5 cards in the KPI strip.
- Showing 30-row raw tables in the primary view instead of the appendix.
- Using green/red for decorative or categorical color — semantic colors are reserved for status encoding.

**Architecture mistakes**
- Skipping the parent design preflight and inventing metric definitions mid-build.
- Building the dashboard before the supported decision is written as a single sentence.
- Applying a design system token set but keeping the wrong font or radius.
- Generating a dashboard that passes visual inspection but fails Analytical Integrity (metric definitions missing, denominators not stated, cherry-picked date ranges).

## Parent Files Referenced

This sub-skill depends on but does not own:

- `../../workflow/design-preflight.md` — 11-step protocol before generating a dashboard
- `../../design-systems/README.md` — design system chooser
- `../../design-systems/<name>/DESIGN.md` — token values and format-specific guidance
- `../../references/visual-report-design-system.md` — base token reference
- `../../references/chart-style-system.md` — chart code configurations
- `../../references/dashboard-layout-patterns.md` — layout archetypes
- `../../references/dashboard-component-patterns.md` — component patterns
- `../../references/dashboard-output-formats.md` — format-specific constraints
- `../../checklists/dashboard-self-critique-checklist.md` — QA rubric
- `../../templates/dashboards/` — dashboard content templates
