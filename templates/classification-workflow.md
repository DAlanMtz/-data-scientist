# Classification Workflow

Use this workflow for binary or multiclass prediction where the target is a discrete class, event, status, or decision category.

## Required Inputs

- Business decision and action triggered by the classification.
- Target definition, positive class, classes, and outcome window.
- Prediction timestamp and population.
- Candidate features available at prediction time.
- Cost of false positives and false negatives.
- Data source, grain, and split constraints.

## Expected Outputs

- Baseline and candidate model comparison.
- Validation results with appropriate metrics.
- Threshold or operating policy for binary classification.
- Confusion matrix and error analysis.
- Calibration assessment if probabilities matter.
- Deployment or reporting recommendation.

## Step-By-Step Workflow

### 1. Define Target

Specify:

- Binary or multiclass target.
- Positive class or class hierarchy.
- Outcome window.
- Exclusions and ambiguous labels.
- Label source and label delay.
- Prediction point.

Reject target definitions that include future information or inconsistent outcome windows.

### 2. Assess Class Balance

Measure:

- Class counts and shares overall.
- Class balance by time, segment, source, and split.
- Rare classes and label noise.

For severe imbalance, prefer PR-AUC, precision@k, recall@k, lift, and cost-based metrics over accuracy.

### 3. Split Data

Choose:

- Random/stratified split only for independent rows.
- Time-aware split for future deployment.
- Group-aware split for repeated customers, accounts, sessions, documents, or devices.
- Nested CV when tuning and unbiased estimation both matter.

Record split logic, seed/cutoff, row counts, and class rates.

### 4. Baseline Model

Build:

- Majority class baseline.
- Current business rule.
- Simple logistic regression or naive Bayes where appropriate.
- Popularity/rate baseline for multiclass assignment.

All advanced models must beat the baseline in a decision-relevant way.

### 5. Feature Preprocessing

Inside validation folds:

- Impute missing values.
- Encode categorical variables.
- Scale only when the model needs it.
- Handle rare categories.
- Apply text/vector transformations.
- Apply resampling only within training folds.

Do not fit encoders, imputers, target encoders, or feature selectors on the full dataset.

### 6. Candidate Models

Consider:

- Logistic or multinomial regression.
- Regularized linear models.
- Decision trees.
- Random forests.
- Gradient boosting.
- Naive Bayes for some text problems.
- SVM or neural models when justified by data and constraints.

Prefer interpretable models when performance is similar.

### Variable and Feature Selection (If Applicable)

Feature selection in classification follows the same discipline as regression:

- Classical methods (backward elimination, forward selection, stepwise): appropriate for logistic regression in interpretable contexts. Nest the entire selection procedure inside validation when estimating predictive performance.
- Regularization (L1/L2/elastic net): preferred for predictive classification. LASSO logistic regression natively handles selection.
- RFE and permutation importance: valid wrappers; must be nested inside CV folds.
- Domain-driven selection: the safest default starting point.

**Guardrail**: do not select features on the full dataset, then split and report test-set performance as unbiased. The estimate will be optimistic.

### 7. Cross-Validation

Use CV that respects data structure:

- Stratified folds for independent imbalanced classification.
- Group folds for entity overlap.
- Time folds for temporal deployment.

Report mean and variation across folds. Keep final test set untouched.

### 8. Evaluation Metrics

Binary:

- Confusion matrix.
- Precision, recall, F1.
- ROC-AUC.
- PR-AUC for imbalance.
- Log loss and Brier score for probabilities.
- Lift or gains chart for prioritization.

Multiclass:

- Macro, micro, and weighted F1.
- Per-class precision and recall.
- Multiclass log loss.
- Top-k accuracy where review workflows allow it.
- Confusion matrix.

### 9. Threshold Selection

For binary classification:

- Choose threshold using business cost, capacity, or required precision/recall.
- Show tradeoff table across candidate thresholds.
- Avoid default 0.5 unless justified.
- Lock threshold before final test reporting.

### 10. Calibration

Check calibration when scores are used as probabilities or expected value inputs.

Use:

- Calibration curve.
- Brier score.
- Score bands with observed event rates.
- Group-level calibration for consequential decisions.

Apply calibration only with validation discipline.

### 11. Error Analysis

Inspect:

- False positives and false negatives.
- Most confident wrong predictions.
- Error by time, segment, source, and subgroup.
- Feature values in error slices.
- Confusions between multiclass labels.

Turn errors into feature fixes, data quality fixes, threshold changes, or deployment caveats.

### 12. Business Cost Tradeoffs

Translate metrics into:

- Cases caught.
- Cases missed.
- Review volume.
- Cost per alert.
- Expected value.
- Customer or operational impact.

Recommend a policy, not just a model.

### 13. Deployment Considerations

Define:

- Input schema and feature refresh.
- Score meaning.
- Threshold and action owner.
- Monitoring metrics.
- Human review and override path.
- Retraining trigger.
- Rollback or fallback rule.

## Validation And Evaluation Guidance

- Validate leakage before interpreting high scores.
- Compare against baseline.
- Use PR-AUC or lift for rare positive classes.
- Report both threshold-free and threshold-specific metrics.
- Check stability across time and groups.

## Interpretation Guidance

- Explain what predicts the class, not what causes it.
- Provide feature importance with leakage and proxy review.
- Use example-based explanations for text or complex models.
- Convert threshold choices into business tradeoffs.

## Common Failure Modes

- Accuracy reported for imbalanced data.
- Test set used for threshold tuning.
- Random split used despite entity or time leakage.
- Target derived from future status.
- Oversampling before splitting.
- Probabilities used despite poor calibration.
- Model deployed without action workflow.

## Tool-Flexible Notes

- Python/R: use pipelines/recipes so preprocessing stays inside validation.
- SQL: build leakage-safe feature extracts and class-balance checks.
- Excel/Sheets: useful for confusion matrices, threshold tables, and cost scenarios.
- Notebooks: keep model comparison and threshold choice explicit.
- Production pipelines: version preprocessing, model artifact, threshold, and monitoring logic together.

