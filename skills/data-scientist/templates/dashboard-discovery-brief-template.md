# Dashboard Discovery Brief Template

Use this template to capture essential context before building or commissioning a dashboard or visual report. Fill it out in one sitting — it should take 15–30 minutes. This brief feeds into `templates/dashboard-design-brief-template.md`, which covers the full planning artifact including page layout, drill-down needs, and access rules.

**This brief does not replace the design brief. It is an upstream scoping artifact.**

---

## Dashboard / Report Name

- **Name:**
- **Prepared by:**
- **Date:**
- **Status:** `[Draft / In review / Approved]`

---

## Audience

Who will use this deliverable? Name the role(s), not just "the team."

- **Primary audience:**
- **Secondary audience (if any):**
- **Technical level:** `[executive / analyst / operator / non-technical / technical specialist]`
- **Usage cadence:** `[daily / weekly / monthly / one-time]`

---

## Decision Supported

Complete this sentence: "This dashboard/report helps [audience] decide [decision]."

- **Decision supported:**
- **Recommended action or threshold (if known):**
- **What changes in user behavior if this dashboard exists?**

If the decision cannot be stated, do not proceed. Resolve this before building.

---

## Primary KPI

The single most important metric for this decision.

- **Metric name (business language):**
- **Plain-language definition:**
- **Why this metric and not another?**

---

## Secondary Metrics

Up to 5 additional metrics. For each, state what decision it supports.

| Metric | Plain-language definition | Decision use |
|---|---|---|
| | | |
| | | |
| | | |
| | | |
| | | |

---

## Metric / Data Contract

This block is required. "Unknown" is acceptable for a field that will be resolved in the design brief — but list it explicitly rather than leaving it blank.

- **Metric definitions (one line per metric):**
- **Data grain** (entity and row level — e.g., "one row per customer per day"):
- **Refresh cadence** (how often data updates):
- **Filters / date range defaults** (what the dashboard opens to):
- **Data freshness indicator** (location and format in the dashboard):
- **Metric owner or source of truth** (who owns the definition; which system is authoritative):
- **Known caveats** (sampling, exclusions, proxy variables, known quality issues):

---

## Required Filters

List the filters users need. Note which are required vs. optional, and what the default value is.

| Filter | Default value | Required? | Notes |
|---|---|---|---|
| | | | |
| | | | |

---

## Data Sources

| Source | Table / file / API | Owner | Refresh cadence | Known quality dependency |
|---|---|---|---|---|
| | | | | |

---

## Refresh Cadence

- **Expected refresh frequency:**
- **Who owns the data pipeline:**
- **What happens if refresh fails? (user-visible behavior):**

---

## Output Format

Select one primary format:

- `[ ]` HTML dashboard (interactive, filter-driven)
- `[ ]` Visual report (static, stakeholder-facing)
- `[ ]` HTML report (polished, PDF-exportable)
- `[ ]` BI tool dashboard (Tableau, Power BI, Looker, etc.)
- `[ ]` Notebook visual section
- `[ ]` Slide deck
- `[ ]` Excel / Sheets dashboard
- `[ ]` Markdown spec (planning artifact, not final output)

See `references/dashboard-output-formats.md` for format-specific constraints.

---

## Design System

Choose a visual direction or state "no preference."

| System | Default for |
|---|---|
| `clean-saas-analytics` | Dashboard, no preference |
| `executive-editorial` | Stakeholder report, PDF |
| `operational-command-center` | Monitoring, alerting |
| `research-paper` | Academic, citation-heavy report |
| `financial-terminal` | Finance, risk, trading |
| `warm-narrative` | Narrative, non-technical |

- **Selected design system:** `[ ]` *(or "no preference")*
- **Brand constraints** (colors, fonts, or logo requirements to accommodate):

---

## Visual Density Preference

- `[ ]` High — maximize information per screen; compact spacing
- `[ ]` Medium — standard; default
- `[ ]` Low — generous spacing; reading-focused

---

## Accessibility Constraints

- **Color blindness:** `[ ]` Must be color-blind safe
- **Font size:** Minimum: ___px
- **Contrast:** `[ ]` WCAG AA required
- **Alt text / written takeaways:** `[ ]` Required for export

---

## Deadline / Use Context

- **Delivery deadline:**
- **How will it be presented or shared?** (screen share, printed, emailed, embedded)
- **Will it be maintained after delivery?** `[Yes / No / Unknown]`

---

## Open Assumptions

List every assumption that has not been confirmed. "None" is not acceptable until the full design brief is complete.

| Assumption | Impact if wrong | Owner to resolve |
|---|---|---|
| | | |
| | | |

---

## Next Steps

- `[ ]` Reviewed by data owner
- `[ ]` Metric definitions confirmed with metric owner
- `[ ]` Advance to `templates/dashboard-design-brief-template.md` for full planning artifact
- `[ ]` Route through `workflow/design-preflight.md` before generating output
