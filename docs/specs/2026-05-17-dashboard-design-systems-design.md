# Design Spec: Dashboard Design Systems and Multi-Format Visual Workflow

**Date:** 2026-05-17  
**Status:** Approved — ready for implementation  
**Commit target:** `Add dashboard design systems and multi-format visual workflow`  
**Repo:** `/Users/dalanma/Documents/Skills/data-scientist`

---

## Goal

Add a reusable design-system and visual workflow layer to the `data-scientist` skill. The layer must:

- Improve the skill's ability to generate beautiful, structured dashboards and visual reports across all output formats.
- Be universal and tool-flexible — no vendor dependency, no proprietary brand, no single dashboard tool.
- Not override analytical correctness — design systems guide appearance, not analytical decisions.
- Be routable by an agent without asking unnecessary discovery questions when context is sufficient.

---

## Approved Approach

**Single atomic commit, full scope.** All files land together so cross-references are correct from the moment everything exists. HTML examples are deferred.

**Design system relationship model:** Complete tables, noted inheritance (Approach C). Each `DESIGN.md` is standalone and copy-paste complete. Tokens marked ★ intentionally differ from the base system (`references/chart-style-system.md`). Unmarked tokens follow the base system unless the surrounding guidance further constrains their use.

**Default design system selection:**

| Situation | Default |
|---|---|
| Dashboard, no stated preference | `clean-saas-analytics` |
| Stakeholder / PDF-style visual report | `executive-editorial` |
| Monitoring / alerting dashboard | `operational-command-center` |
| Academic / research-heavy report | `research-paper` |
| Finance / risk / trading dashboard | `financial-terminal` |
| Narrative / explanatory nontechnical | `warm-narrative` |

---

## File Structure

### New files

```text
skills/data-scientist/
├── design-systems/
│   ├── README.md
│   ├── clean-saas-analytics/DESIGN.md
│   ├── executive-editorial/DESIGN.md
│   ├── operational-command-center/DESIGN.md
│   ├── research-paper/DESIGN.md
│   ├── financial-terminal/DESIGN.md
│   └── warm-narrative/DESIGN.md
├── references/
│   └── dashboard-output-formats.md
├── workflow/
│   └── design-preflight.md
├── templates/
│   └── dashboard-discovery-brief-template.md
└── checklists/
    └── dashboard-self-critique-checklist.md
```

Each design system lives in its own subdirectory (not flat files at `design-systems/` root) to leave room for future additions without cluttering the directory.

### Updated existing files

```text
skills/data-scientist/SKILL.md
skills/data-scientist/workflow/stage-index.md
skills/data-scientist/workflow/response-patterns.md
skills/data-scientist/references/visual-report-design-system.md
skills/data-scientist/references/chart-style-system.md
skills/data-scientist/templates/dashboard-design-brief-template.md
skills/data-scientist/templates/dashboards/README.md
skills/data-scientist/templates/dashboards/html-dashboard-starter-template.md
skills/data-scientist/templates/html-report-template.md
README.md
INSTALL.md
```

---

## Spec: `design-systems/README.md`

**Purpose:** Entry point for the design system layer. Explains what design systems are, when to use them, and how to choose one.

**Required content:**

1. Opening paragraph: design systems are optional visual direction presets. They guide typography, spacing, color, visual density, dashboard layout, chart style, and writing tone. They do not override analytical correctness. If no design system is specified, use `clean-saas-analytics` for dashboards or `executive-editorial` for stakeholder reports.

2. Chooser table — one row per system:

| System | Best for | Avoid when | Density | Color stance | Typography feel | Dashboard/report fit |
|---|---|---|---|---|---|---|
| Clean SaaS Analytics | General analytics, recurring dashboards | High-stakes executive readouts, print | Medium | Blue-neutral, restrained | Clean, functional | Dashboard-primary |
| Executive Editorial | C-suite reports, board readouts, PDF | Operational dashboards, real-time monitoring | Low | Navy + gold, high contrast | Structured, high-contrast headings | Report-primary |
| Operational Command Center | Monitoring, alerting, incident triage, NOC | Executive presentations, academic work | High | Dark mode, electric blue + alert green | Compact, functional | Dashboard-primary, dark |
| Research Paper | Academic reports, methodology writeups, citation-heavy | Recurring dashboards, executive summaries | Very low | Near-monochrome, slate | Legible, spacious | Report-primary |
| Financial Terminal | Finance, risk, trading, quant dashboards | General analytics, non-specialist audiences | Very high | Dark mode, terminal blue + green | Monospace-first, compact | Dashboard-primary, dark |
| Warm Narrative | Explanatory reports, non-technical audiences, newsletters | Operational dashboards, dense data grids | Low | Terracotta + sage, warm | Readable, generous | Report-primary |

3. "Do not use for" callout for each dramatic style (financial-terminal, operational-command-center): explicit statement that these are inappropriate for general analytics, casual chart requests, or exploratory work.

4. Link to `workflow/design-preflight.md` for the full selection protocol.

---

## Spec: DESIGN.md Schema

Every `DESIGN.md` follows this fixed 19-section structure in this order.

### Section order

1. Header with base-relationship note (exact wording — see below)
2. Purpose
3. Best Use Cases
4. Avoid When ← must be concrete and operational
5. Visual Personality
6. Token Summary (21-row table)
7. Typography
8. Spacing and Density
9. Card / Panel Style
10. Chart Style
11. Table Style
12. KPI Style
13. Semantic Color Rules ← dedicated section; explicit guidance for dark systems
14. Dashboard Layout Rules
15. Report Layout Rules
16. Caption / Title Tone
17. Accessibility Rules
18. Format-Specific Guidance (7 subsections)
19. Common Mistakes

### Base-relationship note (exact wording)

> **Base relationship:** [one sentence on how this system relates to `references/chart-style-system.md`].  
> Tokens marked ★ intentionally differ from the base. Unmarked tokens follow the base system unless the surrounding guidance further constrains their use.

### Token Summary table

21 rows. Column headers: `Token | Value | Override`.  
Use `★` in the Override cell for tokens that differ from the base. Leave Override blank for tokens that match the base.

| Token | Notes |
|---|---|
| `background` | Page/canvas background |
| `surface` | Card/panel background |
| `surface_alt` | Secondary surface, table alternating rows, subtle containers |
| `text_primary` | Body text, main labels |
| `text_secondary` | Secondary text, axis titles |
| `border` | Card edges, table borders |
| `chart_grid` | Chart grid line color — differs from `border` in dark systems |
| `muted_fill` | Inactive areas, zero-value bars, empty states, placeholder backgrounds |
| `accent_primary` | Primary highlight, links, selected state |
| `accent_secondary` | Tint/background of accent, secondary highlight |
| `positive` | Favorable metric status |
| `warning` | Needs review, approaching threshold |
| `negative` | Risk, alert, target missed |
| `categorical_palette` | 8-color ordered sequence for multi-series charts |
| `sequential_palette` | 5-stop light-to-dark for density/intensity |
| `diverging_palette` | 5-stop diverging for two-sided data |
| `font_stack` | CSS font-family string |
| `type_scale` | Six sizes in px: micro / small / base / md / lg / display |
| `spacing_scale` | Eight values in px: 4/8/12/16/24/32/40/48 |
| `radius` | Border radius for cards, chips, inputs |
| `shadow` | Box shadow for cards and elevated surfaces |

### Semantic Color Rules section (required in every DESIGN.md)

Must include:
- Green/positive and red/negative encode **metric direction only** — they are not decorative
- In dark-mode systems (operational-command-center, financial-terminal): do not use bright green for non-positive values. Alert green means "metric is favorable" not "data is present."
- `positive`, `warning`, and `negative` must always be paired with a text label or icon — never color alone
- The `categorical_palette` is for categorical series only — do not use categorical colors for positive/negative states

### Avoid When section requirements

Must be concrete and agent-actionable. Examples of sufficient specificity:
- "Do not use for exploratory notebooks or single charts — the dense layout penalizes charts viewed in isolation."
- "Do not use for non-specialist audiences — the monospace-first type and compact spacing assume familiarity with terminal interfaces."
- Avoid vague entries like "Not suitable for all use cases."

### Format-Specific Guidance subsections (7 required)

Each subsection provides 4–8 instructions specific to this design system (not generic advice already in `chart-style-system.md`).

1. **Markdown Report** — how to express the visual personality in plain markdown (heading style, table formatting, emphasis conventions)
2. **HTML Report** — which CSS token overrides to apply; page width, font, spacing adjustments
3. **HTML Dashboard** — dark/light body class, sidebar color, card borders, filter styles
4. **Python / Matplotlib Charts** — rcParam overrides specific to this system (background color, grid color, font, tick color)
5. **R / ggplot2 Charts** — theme_house() overrides; color scale swap; background and grid
6. **Excel / Sheets Dashboard** — cell fill colors, font choices, conditional formatting rules, named styles
7. **BI Dashboard** — background color for canvas/cards, font, accent color, tooltip and legend style

---

## Spec: Six Design System Visual Personalities

All token values are finalized in implementation. Directional personalities approved:

### clean-saas-analytics
- Background: `#f7f8f9` warm off-white
- Surface: `#ffffff`
- Accent primary: `#2952c4` deep blue
- Accent secondary: `#e8edfc` blue tint
- Font: system-ui
- Density: Medium
- Mode: Light
- Override count: 0 (this is the base expression — all tokens match chart-style-system.md)
- Base note: "This system is the closest expression of the base visual system. All tokens match `references/chart-style-system.md`. It is the default for general analytics dashboards."

### executive-editorial
- Background: `#fafaf8` warm cream ★
- Accent primary: `#1a2942` deep navy ★
- Accent secondary: `#c8a96b` warm gold ★
- Font: system-ui, **restrained high-contrast heading weight** (strong size + weight contrast between headings and body; not broadly heavy)
- Content width: 860px (narrower than dashboard, editorial feel)
- Density: Low
- Mode: Light / print-optimized
- Key constraint: print media query required; chart backgrounds must be white

### operational-command-center
- Background: `#0d1117` near-black ★
- Surface: `#161b22` ★
- Accent primary: `#388bfd` electric blue ★
- Accent secondary: `#3fb950` alert green ★ (status only — not decorative)
- Font: system-ui, compact sizes ★
- Density: High
- Mode: Dark
- Semantic color note: bright green = favorable metric status only; not for presence of data or chart fills

### research-paper
- Background: `#ffffff` pure white ★
- Accent primary: `#2c3e50` dark slate ★
- Accent secondary: `#7f8c8d` gray ★
- Font: system-ui (default); optionally Georgia or serif for PDF-style long-form output only ★
- Line height: generous (1.7–1.8 body) ★
- Density: Very low
- Mode: Light
- Radius: minimal (2–4px)

### financial-terminal
- Background: `#0a0c10` terminal black ★
- Surface: `#111418` ★
- Accent primary: `#58a6ff` terminal blue ★
- Accent secondary: `#3fb950` terminal green ★ (positive metric status only)
- Font: monospace-first (`"SFMono-Regular", "Cascadia Mono", Menlo, Consolas, monospace`) ★
- Density: Very high ★
- Spacing scale: compressed (4/6/8/12/16/20/28/36 px) ★
- Mode: Dark
- Radius: `2px` ★
- Semantic color note: terminal green is a status color for favorable metrics only

### warm-narrative
- Background: `#fdf8f3` warm cream ★
- Accent primary: `#c25c2e` terracotta ★
- Accent secondary: `#5c8a5c` sage green ★
- Font: system-ui, generous leading (1.7 body) ★
- Density: Low
- Mode: Light / warm
- Radius: `8px`
- Tone: Conversational, explanation-forward

---

## Spec: `workflow/design-preflight.md`

### Proportionality gates (shown prominently at top)

| Request type | Protocol |
|---|---|
| Single chart, internal or exploratory | Answer directly — no preflight required |
| Polished chart for a presentation or report | Apply chart style only (Steps 5 and 11) |
| Stakeholder dashboard or visual report | Full 11-step preflight |
| Dashboard already in progress | Start at Step 10 (self-critique) |

**Key operating rule:** Do not ask every discovery question by default. If enough context exists, choose sensible defaults, state assumptions, and proceed. If required information is missing, apply the closest default from the default-selection table, state the assumption explicitly, and flag it for review.

### 11-step protocol

1. Identify audience and decision cadence
2. Identify decision supported — if the decision cannot be stated, do not proceed to Step 3; surface this gap
3. Choose artifact type: dashboard / visual report / HTML report / notebook section / slide deck
4. Choose dashboard archetype (route to `templates/dashboards/` — see that README for mapping)
5. Choose design system using the default-selection table
6. Define KPI hierarchy: primary → secondary → diagnostic
7. Define chart sequence: context → status → driver → uncertainty → action
8. Define filters, date range, and refresh cadence
9. Confirm metric definitions, data grain, and data freshness indicator (use discovery brief Metric/Data Contract block)
10. Select output format (route to `references/dashboard-output-formats.md`)
11. Apply self-critique before delivery (route to `checklists/dashboard-self-critique-checklist.md`); resolve any dimension scoring below 4 before sharing; treat Analytical Integrity below 4 as a blocking issue

### Default-selection table

| Situation | Default design system |
|---|---|
| Dashboard, no stated preference | `clean-saas-analytics` |
| Stakeholder / PDF-style visual report | `executive-editorial` |
| Monitoring / alerting dashboard | `operational-command-center` |
| Academic / research-heavy report | `research-paper` |
| Finance / risk / trading dashboard | `financial-terminal` |
| Narrative / explanatory nontechnical | `warm-narrative` |

---

## Spec: `checklists/dashboard-self-critique-checklist.md`

### Scoring rule (shown prominently at top)

- Score each dimension 1–5 using the rubric
- Any dimension scoring **below 4** requires a fix before delivery
- **Analytical Integrity below 4 is a blocking issue** — do not share the dashboard or report until resolved
- If the dashboard or report cannot state the decision it supports, score Decision Clarity **no higher than 3**

### Five dimensions

Each with: Scoring Guide (1–5 descriptions), Questions, Pass Criteria (score ≥ 4), Red Flags, Fixes.

**1. Decision Clarity** — Can a first-time reader identify the decision, the answer, and the next action within 10 seconds?

Scoring anchors:
- 5: Decision is stated in the title or first screen; answer is explicit; next action has an owner
- 4: Decision is clear; answer requires minimal interpretation; next action is implied
- 3: Decision can be inferred; answer is buried or implicit — fix required; cannot score above 3 if decision cannot be stated
- 2: Multiple conflicting readings of what the dashboard is for
- 1: No discernible decision or action

**2. Visual Hierarchy** — Is the most important information visually dominant? Is there one clear focal point per view?

Scoring anchors:
- 5: One dominant element per section; KPI strip leads; supporting detail is visually quieter
- 4: Clear hierarchy; main finding is findable without scanning
- 3: Hierarchy present but uneven; some sections compete for attention
- 2: Everything the same visual weight; no focal point
- 1: No hierarchy; chart dump

**3. Analytical Integrity** (blocking) — Are metrics defined, denominators correct, leakage absent, uncertainty visible, and causal claims avoided?

Scoring anchors:
- 5: Every metric has a definition, denominator, time window, and freshness indicator; uncertainty is shown when it affects decisions; no causal overclaiming
- 4: Metrics defined; denominators present; no obvious integrity gaps
- 3: One or more metrics lack definition or denominator; uncertainty absent where it matters — **blocking, do not deliver**
- 2: Multiple metric gaps; potential leakage or causal overclaiming — **blocking**
- 1: Metrics undefined; no validation; findings cannot be trusted — **blocking**

**4. Design Craft** — Are tokens applied consistently? Are chart defaults replaced? Are captions takeaways, not labels?

Scoring anchors:
- 5: Consistent design system; no matplotlib defaults; every chart caption states a finding
- 4: Design system applied; minor inconsistencies acceptable
- 3: Default chart styles present (tab10 colors, DejaVu Sans, box spines); captions describe rather than interpret
- 2: No design system; significant visual inconsistency
- 1: Raw defaults; no design applied

**5. Usability** — Can a target-audience user operate the dashboard without reading documentation?

Scoring anchors:
- 5: Filter defaults are visible; metric names are in business language; actions are self-evident
- 4: Usable with minimal orientation; most labels are clear
- 3: Requires explanation for filters, metric definitions, or actions
- 2: Multiple friction points; likely to be misread by target audience
- 1: Cannot be used without a guide

---

## Spec: `templates/dashboard-discovery-brief-template.md`

**Purpose:** Concise upstream scoping artifact. Filled in one sitting before building. Feeds into `templates/dashboard-design-brief-template.md` (the full planning artifact).

### Required fields

```
Dashboard / Report Name
Prepared by / date

## Audience
## Decision Supported

## Primary KPI
## Secondary Metrics (up to 5)

## Metric / Data Contract
- Metric definitions (one line per metric)
- Data grain (entity, row level)
- Refresh cadence
- Filters / date range defaults
- Data freshness indicator (location and format)
- Metric owner or source of truth    ← required field
- Known caveats

## Required Filters
## Data Sources
## Refresh Cadence
## Output Format
## Design System (or "no preference")
## Visual Density Preference
## Brand Constraints
## Accessibility Constraints
## Deadline / Use Context
## Open Assumptions
```

**Notes:**
- The Metric / Data Contract block is required, not optional
- Open Assumptions must be populated before the brief is complete; "none" is not acceptable until the full design brief is complete
- This brief is upstream of `dashboard-design-brief-template.md`; it does not replace it

---

## Spec: `references/dashboard-output-formats.md`

**Purpose:** Explains how to adapt a single dashboard or report concept across 8 output formats.

### Structure

One section per format. Each section has:
- **When to use**
- **Element map** (what a "card," "filter," and "KPI" become in this format)
- **How to apply design system tokens**
- **Key constraints**
- **Common mistakes**

### Eight formats

| # | Format | Card equivalent | Key constraint |
|---|---|---|---|
| 1 | Markdown dashboard spec | Section heading + pipe table | No CSS; structure communicated in prose and table |
| 2 | HTML dashboard | `<article class="card">` | Apply DESIGN.md CSS tokens directly |
| 3 | PDF-ready visual report | Page section with fixed margins | Print media query; static charts; no interactive filters |
| 4 | Slide / deck layout | One finding per slide | Max 3 visuals per slide; caption = slide headline |
| 5 | Notebook visual section | Markdown cell + chart cell pair | Apply house rcParams; takeaway in markdown cell below chart |
| 6 | Streamlit / Shiny app | `st.metric` / `valueBox` | Map DESIGN.md tokens to theme config; no hardcoded hex in app code |
| 7 | Excel / Sheets dashboard | Named range + formatted table | Conditional formatting for semantic colors; named styles |
| 8 | BI tool specification | Worksheet / report page | Translate DESIGN.md tokens to tool theme; document metric definitions as field descriptions |

---

## Spec: Existing File Updates

### 1. `SKILL.md`
**Edit type:** Add one bullet under Supporting Files.  
**What:** `design-systems/`: optional visual direction presets for dashboards and reports — choose a system before generating stakeholder-facing visual output; route through `workflow/design-preflight.md`.

### 2. `workflow/stage-index.md`
**Edit type:** Update 3 existing quick-reference rows.  
**Rows to update:** "Design a dashboard," "Make a stakeholder visual report," "Create a polished HTML/PDF report."  
**What:** Add `workflow/design-preflight.md` as the first routing step in each of these rows (before the template reference).

### 3. `workflow/response-patterns.md`
**Edit type:** Update the Visualization or Reporting Request pattern — insert 3 steps.  
**What:**
- After Step 1 (identify audience and decision): add Step 1.5 — if the output is stakeholder-facing, run or confirm the discovery brief (`templates/dashboard-discovery-brief-template.md`)
- After Step 2 (select artifact): add Step 2.5 — choose a design system from `design-systems/README.md` or apply the default from the preflight table
- After Step 4 (apply visual design system): add Step 4.5 — before treating output as publishable, apply self-critique checklist (`checklists/dashboard-self-critique-checklist.md`); resolve any dimension below 4; Analytical Integrity below 4 is blocking

### 4. `references/visual-report-design-system.md`
**Edit type:** Add one paragraph near the top (after the existing intro paragraph).  
**What:** "The base token system defined here is the default for all dashboards and reports. For stronger visual direction, optional design system presets are available in `design-systems/`. Each preset is a complete, standalone token override — apply one in full or use this base system. If no design system is specified, this base system applies."

### 5. `references/chart-style-system.md`
**Edit type:** Add one paragraph near the top (after the existing intro paragraph).  
**What:** "Chart polish rules (spine removal, grid weight, direct labels, export dpi) apply regardless of which design system is active. When a `design-systems/<name>/DESIGN.md` is selected, its `chart_grid`, `muted_fill`, `categorical_palette`, `accent_primary`, and `font_stack` tokens may adapt the chart style — override the corresponding `HOUSE_RCPARAMS` values accordingly. The structural rules do not change."

### 6. `templates/dashboard-design-brief-template.md`
**Edit type:** Add one new section after Dashboard Archetype.  
**What:** Section titled "Visual Direction / Design System" — prompt to choose a design system from `design-systems/README.md`, note the default, and link to the discovery brief for upstream scoping.

### 7. `templates/dashboards/README.md`
**Edit type:** Add one paragraph + short table after Selection Rules.  
**What:** Section titled "Visual Direction" — explain that dashboard archetypes define structure and content; design systems define visual personality. Link to `design-systems/README.md`. List the 6 systems with one-line descriptions.

### 8. `templates/dashboards/html-dashboard-starter-template.md`
**Edit type:** Add one comment at the top of the `<style>` block.  
**What:** `/* CSS tokens below follow the clean-saas-analytics design system (default). To change visual direction, replace token values with those from design-systems/<name>/DESIGN.md. */`

### 9. `templates/html-report-template.md`
**Edit type:** Add one comment at the top of the `<style>` block.  
**What:** `/* CSS tokens below follow the executive-editorial design system (default for stakeholder reports). To change visual direction, replace token values with those from design-systems/<name>/DESIGN.md. */`

### 10. `README.md` (repo root)
**Edit type:** Add one sentence in the Repository Map section.  
**What:** `design-systems/` row — "Optional visual direction presets for dashboards and reports; choose one per project or use the default."

### 11. `INSTALL.md`
**Edit type:** Add one sentence in the File Structure Reference section.  
**What:** `design-systems/` row — "Optional visual direction presets; apply one to adapt typography, color, spacing, and chart style to the project context."

---

## Deferred

HTML examples (`examples/html/`) are deferred. If added later, they should be small (under 200 lines each), demonstrating CSS token swapping from a selected `DESIGN.md` — not full working dashboards.

---

## Implementation Constraints

- No external dependencies — all design system guidance must be applicable without installing a library.
- No vendor-specific guidance that would break if a BI tool changes its interface.
- No copying of proprietary color systems, brand guidelines, or named commercial design systems.
- `SKILL.md` must remain concise after the update — one line added, not a paragraph.
- All 21 token values per design system must be real, usable hex values (or font strings / px values) — no placeholders.
- The `clean-saas-analytics` DESIGN.md token table must match `references/chart-style-system.md` exactly (zero overrides).
- Analytical Integrity below 4 must be described as a **blocking** issue in every location where the self-critique is referenced.
- `gh skill preview DAlanMtz/data-scientist data-scientist` must continue to work after implementation.

---

## Success Criteria

- `design-systems/README.md` chooser table is sufficient for an agent to select a design system without reading individual DESIGN.md files.
- Each DESIGN.md is copy-paste complete — an agent can apply a theme without reading any other file.
- `workflow/design-preflight.md` is self-contained and proportional — quick requests do not require the full protocol.
- The self-critique rubric produces an unambiguous score and a clear fix-or-deliver decision.
- All 11 existing file updates are targeted additions that do not break existing content.
- The system is tool-flexible: guidance applies to HTML, Python, R, Excel, and BI tools without requiring any specific platform.
