# Example: Notebook Audit Prompt

Use this prompt to activate the `model-auditor` sub-skill against a notebook or modeling workflow.

---

## Copy-paste prompt

Use the `model-auditor` sub-skill to audit the attached notebook / modeling code.

Check the following:
1. **Leakage and target integrity** — are any features derived from post-event data? is the target clearly defined and consistently applied? is there entity overlap between train and test?
2. **Validation and splits** — is the split strategy appropriate for the data structure? was any preprocessing done outside the validation fold? was the holdout ever used during development?
3. **Metrics and baselines** — is the reported metric aligned with the business cost? is there a naive baseline to compare against? is the current process baseline included?
4. **Calibration and thresholds** — if the model outputs probabilities or scores, are they calibrated? how was the threshold chosen?
5. **Production readiness** — if this model is intended for production, are the input/output contracts defined? is there a monitoring plan and rollback criteria?

Produce a severity-ranked findings table (Critical / High / Medium / Low / Informational) using `workflow/severity-levels.md`.

For anything that cannot be verified from the available code or data, mark it as an open item and specify what evidence is needed.

Do not assume the model is valid or invalid where the notebook does not provide enough evidence. Mark unverifiable items as open items and recommend the needed retest.

End with a release decision: **Block / Caution / Pass**, and one specific next action.

---

## What good output looks like

- The audit names the model claim and data population before diving into findings
- Every finding has a severity level, the evidence for it, and a required fix
- Open items explicitly state what is missing (no code, no logs, no baseline, no held-out data description)
- The release decision is tied to the highest-severity findings, not a blanket judgment
- The next action is specific: what to fix, who does it, what the retest looks like
