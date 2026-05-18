# Dashboard Assembly Guide

This guide explains how to wire components together into a complete, decision-led HTML dashboard. It assumes the parent skill's design preflight has been completed and all 7 required inputs are confirmed.

---

## Step 1 — Verify Preflight Inputs

Before touching HTML or CSS, confirm these are known:

| Input | Source | Required |
|---|---|---|
| Audience and decision cadence | Parent preflight Step 1 | Yes |
| Decision supported (one sentence) | Parent preflight Step 2 | Yes — **blocking** |
| Artifact type | Parent preflight Step 3 | Yes |
| Dashboard archetype | Parent preflight Step 4 | Yes |
| Design system | Parent preflight Step 5 | Yes |
| KPI hierarchy (primary / secondary / diagnostic) | Parent preflight Step 6 | Yes |
| Metric definitions and data contract | Parent preflight Step 9 | Yes |

If the decision sentence is missing, stop. A dashboard without a supported decision is a chart collection. Return to `../../workflow/design-preflight.md` Step 2.

---

## Step 2 — Choose an Archetype

The archetype defines which sections to include and in what order. Choose from:

| Archetype | Use when |
|---|---|
| `archetypes/analytical-research-dashboard.md` | Research findings, model results, analytical conclusions, multi-family or multi-model summaries |
| `archetypes/executive-kpi-dashboard.md` | Leadership status summary, KPI reporting, decisions with a single primary metric |
| `archetypes/model-monitoring-dashboard.md` | ML model health, drift, calibration, performance tracking |

If none fits exactly, use `analytical-research-dashboard.md` and adapt the section list.

---

## Step 3 — Apply Design System Tokens

1. Open `../../design-systems/<selected-system>/DESIGN.md`.
2. Copy the Token Summary table values.
3. Apply the `<style>` block from `components/token-setup.md` as the base.
4. Override the token values that differ in your selected system (marked ★ in the Token Summary).
5. Keep all token **names** unchanged — only values change.

```
Default → clean-saas-analytics  (no changes needed)
Report  → executive-editorial   (override ~8 tokens)
Monitor → operational-command-center  (override all tokens — dark mode)
```

**Critical:** Do not use `Inter`, `Roboto`, or any other web font unless the design system explicitly lists one. `clean-saas-analytics` uses `system-ui`. Do not hardcode hex values outside the `:root {}` block.

---

## Step 4 — Select Components

Map each archetype section to the component(s) it needs:

| Archetype section | Components |
|---|---|
| Page header + verdict | `components/verdict-band.md` |
| KPI strip | `components/kpi-strip.md` |
| Primary finding section | `components/section-header.md` + table or chart |
| Status table with classifications | `components/status-chips.md` + table base |
| Comparison or benchmark section | `components/comparison-table.md` |
| Stability / segment heatmap | `components/stability-heatmap.md` + `components/filter-bar.md` |
| Data quality / coverage section | `components/coverage-bar.md` + table base |
| Appendix sections | `components/collapsible-appendix.md` |

Load only what the specific dashboard needs. Do not include components the archetype does not call for.

---

## Step 5 — Assemble the First Screen

The first visible screen must answer the supported decision. This is non-negotiable.

**Standard first-screen composition:**

```
1. Page header
   - H1: dashboard name (descriptive, not a project code)
   - Metadata line: date, source, scope
   - Verdict band (if there is a top-level recommendation)

2. KPI strip (3–5 cards)
   - Slot 1: volume / scale
   - Slot 2: primary outcome metric (semantic color)
   - Slot 3: readiness or status summary
   - Slot 4: risk or exception count
   - Slot 5: data quality or completeness

3. Primary section
   - Takeaway-first section header
   - The table or chart the recommendation is based on
```

**What does not belong on the first screen:**
- Raw data tables with many rows
- Feature-level diagnostic content
- Correlation / MI tables
- Methodology notes
- Any section the viewer needs only to verify, not to act

---

## Step 6 — Add Secondary and Diagnostic Sections

Below the first screen, add sections in this sequence from `../../workflow/design-preflight.md` Step 7:

```
context → status → driver → uncertainty → action
```

| Section role | Content | Position |
|---|---|---|
| Context | Population, time window, baseline | First section or second section |
| Status | Current state vs. target — the verdict | First section |
| Driver | Why — segment decomposition, comparison table | Second section |
| Uncertainty | Stability heatmap, concentration checks | Third section |
| Action | Recommended next steps, decision rules | Final visible section |

Every section must have a takeaway-first `section-title` from `components/section-header.md`. No section title should be a chart type or label.

---

## Step 7 — Move Diagnostic Content to the Appendix

After placing all primary sections, review each remaining data element:

**Move to appendix if:**
- The table has more than 15 rows
- The content is a raw diagnostic (correlation table, feature coverage, concentration check)
- The viewer would look at it only to verify the primary finding, not to make a decision
- Methodology notes, exclusion rules, assumptions, or caveat lists

**Keep in main view if:**
- The viewer needs it to act on the dashboard decision
- It is the primary evidence for the recommendation
- It is a metric definition or data contract item (goes in footer instead)

Use `components/collapsible-appendix.md` for all appendix sections. Stack them at the bottom of the page, below all primary and secondary sections.

---

## Step 8 — Apply Accessibility and Responsive Rules

Before considering the dashboard complete, verify:

**Accessibility checklist:**
- [ ] Every `<section>` or `<article>` with interactive content has an `aria-label`
- [ ] Every `<table>` has `<th scope="col">` and `<th scope="row">` where appropriate
- [ ] Color is not the only encoding — metric cells show the number; chips show a text label; verdict bands show a symbol
- [ ] Filter bar buttons use `<button>` elements with `aria-pressed`
- [ ] Focus states are visible (`:focus-visible` outline)
- [ ] Heading hierarchy is maintained: H1 → H2 → H3

**Responsive checklist:**
- [ ] The KPI strip drops to 2–3 columns below 1024px
- [ ] The heatmap wrapper has `overflow-x: auto` so it scrolls horizontally on small screens
- [ ] The comparison table wrapper has `overflow-x: auto`
- [ ] Sidebar (if present) hides at 800px breakpoint
- [ ] Print styles suppress navigation and interactive elements; set `font-size: 12px; background: #fff`

---

## Step 9 — Run the Self-Critique Checklist

Open `../../checklists/dashboard-self-critique-checklist.md`. Score all 5 dimensions:

| Dimension | Passing score | Blocking? |
|---|---|---|
| Decision Clarity | ≥ 4 | Cannot score > 3 if decision sentence is absent |
| Visual Hierarchy | ≥ 4 | No |
| Analytical Integrity | ≥ 4 | **Yes — blocking. Do not deliver below 4.** |
| Design Craft | ≥ 4 | No |
| Usability | ≥ 4 | No |

Fix any dimension that scores below 4. Analytical Integrity failures must be resolved before the dashboard is shown to any stakeholder — they indicate metric definition gaps, missing denominators, or misleading aggregations.

---

## Avoiding Generic AI Dashboard Patterns

Dashboards that look "AI-generated" share recognizable fingerprints. Before delivering, check for these:

| Anti-pattern | Fix |
|---|---|
| Section titles that are chart types or labels ("Monthly WR Table", "Model Results") | Rewrite as findings: "April shows the widest month-to-month swing" |
| KPI cards with values but no comparison context | Add a target, prior period comparison, or status note to every card |
| All tables at the same visual weight — flat structure | Use section headers, semantic row backgrounds, and appendix to create hierarchy |
| Status values as raw strings ("baseline_52_ready_but_monitor") | Replace with styled chips from `components/status-chips.md` |
| Recommendation buried in the body text | Promote to verdict band near the header |
| No color distinction between favorable and unfavorable metrics | Apply metric color cells from `components/metric-color-cell.md` |
| Identical padding and border-radius on every element | Use the token scale for varied density: section cards are larger, chip radius is 20px, table cells are tighter |
| Dashboard that contains every data point from the report | Apply progressive disclosure: primary → secondary → appendix |

---

## First-Screen Checklist

Before scrolling past the first screen, ask:

- [ ] Can a viewer state the supported decision from what they see?
- [ ] Is there a verdict (if required) visible above the KPI strip?
- [ ] Do the KPI cards have semantic color encoding that matches their state?
- [ ] Does the primary section title state the finding, not the chart type?
- [ ] Are there no more than 5 KPI cards?
- [ ] Is the data contract / metric definitions visible or reachable from the first screen (footer or metadata line)?
