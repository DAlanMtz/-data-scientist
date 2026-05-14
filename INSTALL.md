# Installation Guide

This skill is a markdown-based instruction set for AI agents. Installation means making the skill files available to your agent system.

## Quick Install

Clone the repo:

```bash
git clone https://github.com/DAlanMtz/data-scientist.git
```

Or copy into an existing skills directory:

```bash
cp -R data-scientist /path/to/your/agent/skills/
```

---

## Agent-Specific Instructions

### OpenCode

OpenCode-style agents load skills from a local directory. To install:

1. Clone or copy the `data-scientist` folder into your skills directory (e.g., `~/.opencode/skills/` or your project's `skills/` folder).
2. Keep the folder structure intact — `SKILL.md` is the entrypoint and supporting files are organized under `workflow/`, `references/`, `templates/`, `checklists/`, and `examples/`.
3. The agent will load `SKILL.md` and route to supporting files as needed.

```bash
git clone https://github.com/DAlanMtz/data-scientist.git ~/.opencode/skills/data-scientist
```

### Claude Code

Claude Code can use this skill as a project instruction source:

1. Clone or copy the repo into your project directory or a shared skills folder.
2. In your project, reference or copy `SKILL.md` as the primary instruction file.
3. Tell Claude Code: *"Read SKILL.md first, then use workflow/stage-index.md to orient the current work."*
4. Supporting files under `workflow/`, `references/`, `templates/`, `checklists/`, and `examples/` will be referenced on demand.

```bash
git clone https://github.com/DAlanMtz/data-scientist.git .claude/skills/data-scientist
```

Or add to your project's `.claude/` directory:

```bash
cp -R data-scientist /your/project/.claude/skills/
```

### Codex and Coding Agents

For Codex or similar coding agents that support instruction files:

1. Clone or copy the skill folder into your agent's instructions or context directory.
2. Set `SKILL.md` as the primary instruction file.
3. When starting a data science task, instruct the agent: *"Use the workflow files (workflow/stage-index.md) before starting implementation to identify the correct project stage, artifact, and quality gate."*

```bash
git clone https://github.com/DAlanMtz/data-scientist.git ~/instructions/data-scientist
```

### Generic AI Agents (Any Markdown-Skill System)

For any agent that supports custom instruction files:

1. Provide `SKILL.md` as the primary instruction.
2. Attach or reference supporting files from `workflow/`, `references/`, `templates/`, `checklists/`, or `examples/` as needed for the specific task.
3. Use `workflow/stage-index.md` to orient the agent to the current project stage before starting work.

The minimum viable install is `SKILL.md` alone. For full functionality, keep the folder structure intact.

---

## File Structure Reference

```text
data-scientist/
├── SKILL.md                          ← Primary entrypoint
├── workflow/
│   ├── README.md                     ← Workflow layer overview
│   ├── stage-index.md                ← Quick reference: stage → gate → artifact → template
│   ├── lifecycle.md                  ← Full lifecycle with exit criteria
│   ├── stages.md                     ← Stage-by-stage do/don't lists
│   ├── quality-gates.md              ← Gate pass/fail criteria
│   ├── artifacts.md                  ← Deliverable definitions
│   ├── response-patterns.md          ← How to handle common request types
│   └── severity-levels.md            ← Audit finding classification
├── references/                       ← Domain guides (methodology, validation, metrics, etc.)
├── templates/                        ← 25 reusable templates
├── checklists/                       ← 11 audit and quality-control checklists
└── examples/                         ← Python, R, SQL, Excel examples
```

---

## Keeping the Skill Updated

```bash
cd data-scientist
git pull
```

## License

MIT — see LICENSE file.
