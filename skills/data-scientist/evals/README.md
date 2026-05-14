# Data Scientist Skill Evals

These are lightweight behavioral evals for the `data-scientist` skill. They are not automated tests. They are prompts and expected behavior checks for future edits, agent comparisons, or regression review.

## How To Use

1. Run a prompt from `prompts.md` with the skill enabled.
2. Run the same prompt without the skill or with a previous skill version.
3. Compare responses against `expected-behaviors.md`.
4. Check whether the agent follows stage, gate, artifact, and next-action discipline.
5. Check whether it avoids leakage, weak metrics, causal overclaiming, premature modeling, and premature production claims.
6. Mark each response pass, partial, or fail using the qualitative criteria.

## What Good Behavior Looks Like

- Identifies the active lifecycle stage when the request is project-level.
- Names the relevant quality gate.
- Produces or outlines the right artifact.
- Uses severity levels for audits.
- Refuses or redirects invalid shortcuts.
- Ends with the next correct action.

## What Weak Behavior Looks Like

- Jumps directly to algorithms.
- Accepts accuracy, charts, or notebook success at face value.
- Uses causal language for predictive evidence.
- Ignores data quality, leakage, validation, baselines, calibration, responsible AI, or production readiness.
- Gives broad advice without a concrete artifact.

