# Data Scientist Skill

**Version:** 1.0.0 | **Status:** Ready to use | **License:** MIT

A universal senior data scientist skill for AI agents. Covers the full data science lifecycle — from problem framing through production monitoring — across Python, R, SQL, Excel/Sheets, notebooks, and production pipelines.

Not tied to any course, framework, or domain. Designed to work with Claude Code, Codex, OpenCode, and any agent system that can read markdown skill files.

---

## What This Skill Is For

Use this skill when you need an AI agent to reason and act like a senior data scientist. The skill enforces a decision-first, validation-first, production-aware posture: it requires the agent to frame the problem and define success criteria before selecting a method, design a rigorous validation strategy before interpreting results, and assess production and responsible-AI implications before recommending deployment. It covers the full lifecycle from raw data through monitoring, and applies across languages, domains, and team contexts.

## What It Covers

- Exploratory data analysis and data quality assessment
- Feature engineering and selection
- Classical and modern model selection
- Regression, classification, clustering, dimensionality reduction
- Forecasting, NLP/text mining, recommendation systems
- Anomaly detection and association rules
- Causal analysis and decision science
- Model validation and leakage prevention
- Metrics, diagnostics, and calibration
- Model interpretation and explanation
- Responsible AI and fairness assessment
- Production readiness and deployment review
- Model monitoring and drift detection
- Reporting and stakeholder communication
- Visual reports, dashboard design briefs, dashboard QA, and HTML/PDF-ready reporting
- Dashboard template library for analytics, executive KPI, model performance, forecasting, cohort retention, anomaly monitoring, and HTML prototypes

## Repository Map

```text
skills/data-scientist/
├── SKILL.md                ← Primary entrypoint
├── workflow/               Operating system: stages, gates, artifacts, response patterns, severity levels
├── prompts/                Copy-paste prompts that activate disciplined agent behavior
├── evals/                  Behavioral eval prompts and expected behavior checks
├── references/             Senior data science methodology, judgment, and domain guides
├── templates/              Reusable deliverable and workflow templates (37 files)
├── checklists/             Audit and quality-control checklists (13 files)
└── examples/               Python, R, SQL, and Excel/Sheets implementation examples
```

## Workflow Discipline

The skill guides an agent through a repeatable data science operating workflow:

1. Identify the active lifecycle stage.
2. Check the relevant quality gate.
3. Choose the expected artifact.
4. Apply the right checklist or reference.
5. Confirm deliverable completeness with `skills/data-scientist/workflow/definition-of-done.md`.
6. Use `skills/data-scientist/workflow/rationalization-guardrails.md` to prevent common shortcuts such as premature modeling, weak validation, accuracy-only evaluation, causal overclaiming, and notebook-only production claims.
7. End with the next correct action.

Use this workflow proportionally. Quick conceptual or syntax questions can be answered directly. Project-level modeling, auditing, reporting, validation, visualization, or production-readiness work should use the stage/gate/artifact workflow.

## Quickstart Prompts

See [`skills/data-scientist/prompts/quickstart-prompts.md`](skills/data-scientist/prompts/quickstart-prompts.md) for copy-paste prompts that activate the skill across agents. They cover notebook audits, dataset audits, modeling plans, validation strategy, leakage review, model comparison, error analysis, calibration and thresholds, decision memos, stakeholder reports, dashboard review, production readiness, monitoring, and notebook-to-production conversion.

## Evaluation Prompts

See [`skills/data-scientist/evals/`](skills/data-scientist/evals/) for lightweight behavioral evals. Use them when changing the skill or comparing agents to check whether the agent follows stage/gate/artifact discipline and avoids leakage, weak metrics, causal overclaiming, premature modeling, and premature production claims.

## Installation

### GitHub CLI (recommended)

```bash
gh skill install DAlanMtz/data-scientist data-scientist --agent opencode --scope user
gh skill install DAlanMtz/data-scientist data-scientist --agent codex --scope user
gh skill install DAlanMtz/data-scientist data-scientist --agent claude-code --scope user
```

### Manual install

Clone the repo and copy the skill folder into your agent's skills directory:

```bash
git clone https://github.com/DAlanMtz/data-scientist.git
cp -R data-scientist/skills/data-scientist /path/to/your/agent/skills/
```

See [INSTALL.md](INSTALL.md) for agent-specific paths and setup instructions.

---

## Usage — Agent Compatibility

### Claude Code

1. Install via `gh skill install` (above) or copy `skills/data-scientist/` into `.claude/skills/`.
2. Reference `skills/data-scientist/SKILL.md` as the primary instruction file for your project.
3. Tell Claude Code: *"Read SKILL.md first, then use workflow/stage-index.md to orient the current work."*
4. Supporting files under `workflow/`, `references/`, `templates/`, `checklists/`, and `examples/` are referenced on demand.

### OpenCode

1. Install via `gh skill install` (above) or copy `skills/data-scientist/` into `~/.opencode/skills/`.
2. Keep the folder structure intact — `SKILL.md` is the entrypoint and all supporting files must remain in place.
3. The agent will load `SKILL.md` and route to supporting files as needed.

### Codex and Coding Agents

1. Install via `gh skill install` (above) or copy `skills/data-scientist/` into your agent's instructions directory.
2. Set `skills/data-scientist/SKILL.md` as the primary instruction file.
3. Before starting implementation, instruct the agent to use `workflow/stage-index.md` to identify the correct project stage, artifact, and quality gate.

### Generic AI Agents

1. Provide `skills/data-scientist/SKILL.md` as the primary instruction.
2. Attach or reference supporting files from `workflow/`, `references/`, `templates/`, `checklists/`, or `examples/` as needed.
3. Use `workflow/stage-index.md` to orient the agent to the current project stage before starting work.

The minimum viable install is `SKILL.md` alone. For full functionality, keep the folder structure intact.

---

## Example Prompts

```text
Use the data-scientist skill to audit this notebook for leakage, validation design, metric choice, calibration, and business usefulness.
```

```text
Use the data-scientist skill to create a modeling plan for this dataset. Start with project stage, quality gate, target definition, validation plan, baseline, candidate models, metrics, and expected artifacts.
```

```text
Use the data-scientist skill in audit mode. Produce severity-ranked findings and a next-action plan.
```

```text
Use the data-scientist skill to turn these results into a decision memo for stakeholders.
```

```text
Use the data-scientist skill to review this model for production readiness. Check the input contract, output contract, monitoring plan, rollback plan, and responsible AI considerations.
```

---

## License

MIT — see [LICENSE](LICENSE) file.
