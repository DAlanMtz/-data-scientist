# Installation Guide

This skill is a markdown-based instruction set for AI agents. Installation means making the skill files available to your agent system.

## GitHub CLI Install (recommended)

If your agent supports `gh skill install`, use the appropriate command below:

```bash
# OpenCode
gh skill install DAlanMtz/data-scientist data-scientist --agent opencode --scope user

# Codex
gh skill install DAlanMtz/data-scientist data-scientist --agent codex --scope user

# Claude Code
gh skill install DAlanMtz/data-scientist data-scientist --agent claude-code --scope user
```

The skill files live under `skills/data-scientist/` in this repo — the GitHub CLI discovery convention requires this layout.

---

## Manual Install

Clone the repo, then copy the skill folder into your agent's skills directory:

```bash
git clone https://github.com/DAlanMtz/data-scientist.git
cp -R data-scientist/skills/data-scientist /path/to/your/agent/skills/
```

---

## Agent-Specific Instructions

### OpenCode

OpenCode-style agents load skills from a local directory. To install:

1. Copy or clone the skill folder into your skills directory (e.g., `~/.opencode/skills/` or your project's `skills/` folder).
2. Keep the folder structure intact — `SKILL.md` is the entrypoint and supporting files are organized under `workflow/`, `references/`, `templates/`, `checklists/`, and `examples/`.
3. Start with `prompts/quickstart-prompts.md` for copy-paste prompts that activate the skill correctly.
4. Use `workflow/stage-index.md` as the orientation file for project-level work.
5. Use `workflow/definition-of-done.md` before treating an artifact as complete.

```bash
git clone https://github.com/DAlanMtz/data-scientist.git /tmp/ds-skill
cp -R /tmp/ds-skill/skills/data-scientist ~/.opencode/skills/data-scientist
```

### Claude Code

Claude Code can use this skill as a project instruction source:

1. Copy the skill folder into your project's `.claude/skills/` directory or a shared skills folder.
2. In your project, reference `skills/data-scientist/SKILL.md` as the primary instruction file.
3. Tell Claude Code: *"Read SKILL.md first, then use workflow/stage-index.md to orient the current work."*
4. Start with `prompts/quickstart-prompts.md` for common audit, modeling, validation, reporting, and production-readiness prompts.
5. Use `workflow/definition-of-done.md` before declaring a deliverable complete.
6. For visual reports or dashboards, start with `templates/visual-analysis-workflow.md`, then route to the visual report, HTML report, dashboard design brief, or dashboard QA template. For stakeholder-facing HTML dashboard generation, use `subskills/dashboard-designer/` after completing the design preflight.
7. Supporting files under `workflow/`, `prompts/`, `evals/`, `references/`, `templates/`, `checklists/`, and `examples/` will be referenced on demand.

```bash
git clone https://github.com/DAlanMtz/data-scientist.git /tmp/ds-skill
cp -R /tmp/ds-skill/skills/data-scientist .claude/skills/data-scientist
```

### Codex and Coding Agents

For Codex or similar coding agents that support instruction files:

1. Copy the skill folder into your agent's instructions or context directory.
2. Set `SKILL.md` as the primary instruction file.
3. When starting a data science task, instruct the agent: *"Use the workflow files (workflow/stage-index.md) before starting implementation to identify the correct project stage, artifact, and quality gate."*
4. Use `workflow/definition-of-done.md` to check deliverable completeness.
5. Start from `prompts/quickstart-prompts.md` when you want a ready-made prompt for audit, modeling, reporting, validation, or production-readiness work.

```bash
git clone https://github.com/DAlanMtz/data-scientist.git /tmp/ds-skill
cp -R /tmp/ds-skill/skills/data-scientist ~/instructions/data-scientist
```

### Generic AI Agents (Any Markdown-Skill System)

For any agent that supports custom instruction files:

1. Provide `SKILL.md` as the primary instruction.
2. Attach or reference supporting files from `workflow/`, `references/`, `templates/`, `checklists/`, or `examples/` as needed for the specific task.
3. Use `workflow/stage-index.md` to orient the agent to the current project stage before starting work.
4. Use `workflow/definition-of-done.md` to check whether the expected artifact is complete enough to trust or hand off.
5. Use `prompts/quickstart-prompts.md` for copy-paste prompts that activate stage, gate, artifact, and next-action discipline.

The minimum viable install is `SKILL.md` alone. For full functionality, keep the folder structure intact.

---

## File Structure Reference

```text
skills/data-scientist/
├── SKILL.md                          ← Primary entrypoint
├── workflow/
│   ├── README.md                     ← Workflow layer overview
│   ├── stage-index.md                ← Quick reference: stage → gate → artifact → template
│   ├── lifecycle.md                  ← Full lifecycle with exit criteria
│   ├── stages.md                     ← Stage-by-stage do/don't lists
│   ├── quality-gates.md              ← Gate pass/fail criteria
│   ├── artifacts.md                  ← Deliverable definitions
│   ├── definition-of-done.md         ← Completion checks for common artifacts
│   ├── rationalization-guardrails.md ← Shortcut prevention layer
│   ├── response-patterns.md          ← How to handle common request types
│   └── severity-levels.md            ← Audit finding classification
├── prompts/
│   └── quickstart-prompts.md         ← Copy-paste prompts for common tasks
├── evals/
│   ├── README.md                     ← How to use behavioral evals
│   ├── prompts.md                    ← Evaluation prompts
│   └── expected-behaviors.md         ← Qualitative pass/fail criteria
├── references/                       ← Domain guides (methodology, validation, metrics, etc.)
├── design-systems/                   ← Optional visual direction presets; apply one to adapt typography, color, spacing, and chart style to the project context
├── templates/                        ← Reusable deliverable and workflow templates
├── checklists/                       ← Audit and quality-control checklists
├── examples/                         ← Python, R, SQL, Excel examples
└── subskills/
    ├── dashboard-designer/           ← Sub-skill for HTML dashboard generation: CSS token setup, component recipes (KPI strip, chips, heatmap, comparison table, appendix), archetype layouts, and assembly guide
    └── model-auditor/                ← Sub-skill for auditing models, notebooks, backtests, experiments, and model claims
```

---

## Keeping the Skill Updated

```bash
cd data-scientist
git pull
```

Then re-copy if using a manual install:

```bash
cp -R skills/data-scientist /path/to/your/agent/skills/data-scientist
```

## License

MIT — see LICENSE file.
