# Project Brief Template

## Purpose

Document the business framing of a data science project before any data, modeling, or analysis work begins. The project brief is the reference document for all subsequent decisions — target definition, metric selection, validation design, and deployment scope all follow from it.

## When to Use

At **Stage 0: Intake and Framing**. Produce this before reviewing data or suggesting approaches. Update it if scope, stakeholders, or success criteria change.

## Required Inputs

- Business request or problem statement from the stakeholder
- Named decision-maker or operational user of the output
- Any prior analysis, current process, or baseline performance information
- Known constraints: timeline, budget, interpretability, latency, fairness, regulatory

## Minimum Contents

### 1. Problem Statement

Write the problem as a decision or action, not as a model type.

> **Bad:** "Build a churn model."
> **Good:** "Identify which subscribers are at high risk of canceling in the next 30 days so the retention team can offer targeted interventions."

- Decision being supported:
- Who makes the decision:
- What action follows from the output:

### 2. Unit of Analysis

- One row represents: `[entity type — customer, transaction, store, session, etc.]`
- Grain: `[e.g., one row per customer per month]`
- Time window: `[e.g., observations from 2023-01-01 to present, outcome window 30 days forward]`
- Population: `[e.g., active subscribers with at least 3 months of tenure]`
- Exclusions: `[e.g., trial accounts, internal users, fraud-flagged accounts]`

### 3. Success Metric

- Primary metric: `[e.g., Recall at top-10% risk tier]`
- Business rationale: `[e.g., missing a high-risk churner costs $X; a false positive costs $Y in call-center time]`
- Minimum useful performance: `[e.g., must outperform current rule by >15% recall at same contact rate]`

### 4. Constraints

| Constraint | Present? | Detail |
|---|---|---|
| Interpretability required | Yes / No | `[e.g., must explain to customer why they were contacted]` |
| Latency requirement | Yes / No | `[e.g., batch weekly is acceptable; real-time not needed]` |
| Fairness / protected attributes | Yes / No | `[e.g., must not discriminate by geography as a proxy for race]` |
| Regulatory or legal | Yes / No | `[e.g., CCPA data use restriction applies]` |
| Data access limits | Yes / No | `[e.g., cannot use PII in training data]` |
| Infrastructure constraints | Yes / No | `[e.g., must run in Snowflake; no external APIs]` |

### 5. Open Questions

List unresolved questions that must be answered before Stage 1 can begin:

- `[Question 1]`
- `[Question 2]`

---

## Strong Version Additions

### Decision Hierarchy

Beyond the primary decision, list sub-decisions and downstream actions the output enables:

| Level | Decision | Owner | Action if Yes | Action if No |
|---|---|---|---|---|
| Primary | `[high-level decision]` | `[stakeholder]` | `[action]` | `[action]` |
| Sub-decision | `[sub-decision]` | `[owner]` | `[action]` | `[action]` |

### Stakeholder Map

| Role | Name | Relationship to output |
|---|---|---|
| Project sponsor | `[name]` | Approves go/no-go |
| Decision user | `[name]` | Uses scores for action |
| Data owner | `[name]` | Provides and controls data |
| Engineering partner | `[name]` | Owns deployment |
| Risk / legal / compliance | `[name]` | Reviews fairness and policy |

### Current Process Baseline

- How is this decision made today: `[manual rule / prior model / human judgment / not made]`
- Current performance (if known): `[e.g., 18% recall at 10% contact rate]`
- Cost of current process: `[e.g., $X per contact, $Y per missed churner]`

### Out-of-Scope Items

Explicitly list what is not in scope to prevent scope creep:

- `[Out-of-scope item 1]`
- `[Out-of-scope item 2]`

### Assumptions Log

| Assumption | Owner | Risk if Wrong |
|---|---|---|
| `[assumption]` | `[person]` | `[consequence]` |

---

## Output Format

A written document (Markdown, Word, or slide) shared with the stakeholder before data work begins. Should fit on 1–2 pages. Expand sections only where the project warrants detail.

## Quality Checks

- [ ] Problem is framed as a decision, not a model type
- [ ] A named person is accountable for the decision
- [ ] Unit of analysis is unambiguous
- [ ] Primary metric has a business rationale, not just a technical one
- [ ] At least one constraint is documented or "unconstrained" is stated explicitly
- [ ] Open questions are listed — not silently assumed away

## Common Mistakes

- Stating the problem as "build X model" — reframe as the decision it supports
- Accepting "improve performance" as a success criterion — name the metric and threshold
- Skipping the exclusions — they define scope as much as inclusions do
- Treating interpretability as optional until deployment — surface it here
- No named stakeholder — output will have no accountable consumer

## Related Workflow Stage / Gate

- **Stage:** 0 — Intake and Framing
- **Gate:** Framing Gate — must pass before Stage 1 (Data Understanding and Quality Audit) begins

## Related References / Checklists

- `workflow/lifecycle.md` — Stage 0 exit criteria
- `workflow/quality-gates.md` — Framing Gate pass requirements
- `checklists/pre-modeling-checklist.md` — Business and Decision Clarity section
- `checklists/responsible-ai-checklist.md` — fairness and risk review
