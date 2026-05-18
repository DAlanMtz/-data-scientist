# Dashboard Design Systems

Design systems are optional visual direction presets. Each preset guides typography, spacing, color, visual density, dashboard layout, chart style, and writing tone. They do not override analytical correctness — metric definitions, denominators, uncertainty disclosure, and data grain are always governed by the analytical workflow. Design systems guide how a correct analysis looks and reads.

If no design system is specified, apply these defaults:

| Situation | Default design system |
|---|---|
| Dashboard, no stated preference | `clean-saas-analytics` |
| Stakeholder / PDF-style visual report | `executive-editorial` |
| Monitoring / alerting dashboard | `operational-command-center` |
| Academic / research-heavy report | `research-paper` |
| Finance / risk / trading dashboard | `financial-terminal` |
| Narrative / explanatory nontechnical report | `warm-narrative` |

For the full selection protocol, see `workflow/design-preflight.md`.

---

## Chooser Table

| System | Best for | Avoid when | Density | Color stance | Typography feel | Dashboard / report fit |
|---|---|---|---|---|---|---|
| **Clean SaaS Analytics** | General analytics dashboards, recurring internal reporting, product metrics | High-stakes executive readouts, print, narrative reports | Medium | Blue-neutral, restrained | Clean, functional | Dashboard-primary |
| **Executive Editorial** | C-suite reports, board readouts, PDF/print deliverables, stakeholder summaries | Operational dashboards, real-time monitoring, dense data grids | Low | Navy + warm gold, high contrast | Structured, restrained high-contrast headings | Report-primary |
| **Operational Command Center** | Monitoring dashboards, alerting, incident triage, NOC, SRE, infrastructure | Executive presentations, academic work, narrative reports | High | Dark mode, electric blue + alert green | Compact, functional | Dashboard-primary (dark) |
| **Research Paper** | Academic reports, methodology writeups, citation-heavy analysis, long-form explanations | Recurring dashboards, executive summaries, quick internal reports | Very low | Near-monochrome, dark slate | Legible, spacious, generous line height | Report-primary |
| **Financial Terminal** | Finance dashboards, risk management, trading, quant analysis, P&L monitoring | General analytics, non-specialist audiences, narrative or academic work | Very high | Dark mode, terminal blue + terminal green | Monospace-first, compact, information-dense | Dashboard-primary (dark) |
| **Warm Narrative** | Explanatory reports, non-technical audiences, newsletters, customer-facing summaries | Operational dashboards, dense data grids, real-time monitoring | Low | Terracotta + sage, warm | Readable, generous, conversational | Report-primary |

---

## Important: Do Not Over-Select Dramatic Styles

**Operational Command Center** and **Financial Terminal** are purpose-built for specialist contexts. Do not apply them to:
- General analytics dashboards or exploratory work
- Single charts or notebook cells
- Non-specialist audiences unfamiliar with dark terminal interfaces
- Executive presentations or academic reports

When in doubt, use `clean-saas-analytics` for dashboards or `executive-editorial` for reports.

---

## How to Apply a Design System

1. Choose a system from the chooser table above or use the defaults.
2. Open the system's `DESIGN.md` — it is standalone and copy-paste complete.
3. Apply the Token Summary to HTML/CSS, override Python `HOUSE_RCPARAMS`, or adapt to your BI tool theme.
4. Follow the Format-Specific Guidance section for your output format.
5. Do not mix tokens from different design systems in the same deliverable.

Each `DESIGN.md` contains the full token summary, typography, spacing, chart/table/KPI guidance, layout rules, caption tone, accessibility rules, format-specific guidance for 7 output formats, and common mistakes.
