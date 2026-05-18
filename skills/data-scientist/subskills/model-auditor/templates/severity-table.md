# Severity Reference for Model Audits

Severity levels are defined in `../../workflow/severity-levels.md`. This table maps them to release decision guidance for model audits.

| Severity | Example in model audits | Release decision implication |
|---|---|---|
| Critical | Target leakage confirmed; test set contaminated; fundamental flaw invalidates all reported results | **Block** — must fix before any production use or further decision-making based on this model |
| High | Weak validation design; missing baseline; calibration never checked; no monitoring plan | **Block or Caution** — fix before production; Caution if risk is explicitly mitigated and documented |
| Medium | Subgroup analysis absent; threshold selection undocumented; minor population mismatch | **Caution** — document, track, and address in next iteration |
| Low | Cosmetic metric reporting issues; minor documentation gaps; informational warnings | **Pass with documentation** |
| Informational | Observations, improvement suggestions, non-blocking notes | **Pass** |

## Release Decision Definitions

- **Block:** Do not deploy or use this model for consequential decisions until findings are resolved.
- **Caution:** Proceed with explicit documentation of known risks, mitigations, and a plan to resolve open items.
- **Pass:** No blocking findings. Document any Low / Informational items for future work.

See `../../workflow/severity-levels.md` for full severity definitions.
