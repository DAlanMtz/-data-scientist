# Model Audit Report

**Audit date:** [date]
**Audited by:** [agent / analyst name]
**Model / artifact audited:** [name, version, notebook path, or description]

---

## Model Claim

[What the model was said to do. What performance was claimed. Source of the claim — notebook, README, team communication, or verbal assertion.]

## Data Population

[Who. When (date range). Grain (one row = ?). Any known population changes, shifts, or exclusions. Where data was sourced from.]

---

## Findings

[Add one row per finding. If there are no findings in a domain, add a row with Severity = Informational and note "No issues identified."]

| # | Severity | Domain | Finding | Evidence | Why it matters | Required fix | Retest plan |
|---|---|---|---|---|---|---|---|
| 1 | Critical | Leakage | ... | ... | ... | ... | ... |
| 2 | High | Validation | ... | ... | ... | ... | ... |

**Severity levels:** Critical / High / Medium / Low / Informational
See `../../workflow/severity-levels.md` for definitions.

**Domain options:** Leakage | Validation | Metrics | Calibration | Production

---

## Open Items

**Required section.** List every item that could not be verified due to missing code, missing data, missing logs, missing baseline, or missing experiment details. If nothing was unverifiable, state that explicitly: "All items were verifiable from the available evidence — no open items."

| # | Item | What is missing | Impact if unresolved | Recommended next step |
|---|---|---|---|---|
| 1 | ... | ... | ... | ... |

---

## Release Decision

**Block / Caution / Pass**

[State the decision and the rationale. Reference the highest-severity finding(s) that drove it. If open items exist that prevent a definitive decision, state that here.]

Release decision guidance (see `severity-table.md` for the full table):
- **Block:** any Critical finding, or High findings that cannot be mitigated before release
- **Caution:** High findings with documented mitigations, or multiple Medium findings
- **Pass:** only Medium / Low / Informational findings, all documented

---

## Next Correct Action

[One specific action: what to fix first, who does it, what the output will be, and what retest is required before re-evaluation. Example: "Remove `account_closed_flag` from the feature set, retrain the model, and re-evaluate AUC on the clean holdout. Owner: [name]. Output: updated notebook with clean feature set and held-out AUC reported. Retest: re-run this audit after the retrain."]
