# R Classification Example

## Use Case

Build a binary classification workflow in R with split, preprocessing, model fitting, and evaluation.

## Expected Inputs

- Data frame with target and predictor columns.
- Target definition, positive class, and validation strategy.
- Business cost/capacity notes for threshold choice.

## Expected Outputs

- Baseline and model metrics.
- Confusion matrix.
- Sensitivity/specificity or ROC-AUC.
- Threshold and error-analysis notes.

## Concise Workflow

1. Define target and remove leaky fields.
2. Split data with stratification where appropriate.
3. Preprocess using training data.
4. Fit baseline and candidate model.
5. Evaluate threshold and ranking metrics.

## Representative Pattern

```r
library(tidyverse)
library(caret)
library(pROC)

df <- df %>% mutate(churned = factor(churned, levels = c("no", "yes")))

set.seed(42)
idx <- createDataPartition(df$churned, p = 0.8, list = FALSE)
train <- df[idx, ]
test <- df[-idx, ]

leaky <- c("customer_id", "cancelled_at", "final_status")
features <- setdiff(names(train), c("churned", leaky))

ctrl <- trainControl(
  method = "cv",
  number = 5,
  classProbs = TRUE,
  summaryFunction = twoClassSummary
)

model <- train(
  x = train[, features],
  y = train$churned,
  method = "glm",
  family = binomial(),
  trControl = ctrl,
  metric = "ROC",
  preProcess = c("medianImpute", "center", "scale")
)

probs <- predict(model, newdata = test[, features], type = "prob")[, "yes"]
pred <- factor(if_else(probs >= 0.35, "yes", "no"), levels = c("no", "yes"))

confusionMatrix(pred, test$churned, positive = "yes")
roc_obj <- roc(response = test$churned, predictor = probs, levels = c("no", "yes"))
auc(roc_obj)
```

## Validation And Quality Checks

- Use time-aware or group-aware split when needed; `createDataPartition` is not enough for temporal/entity leakage.
- Keep preprocessing learned from training data.
- Check class balance by split.
- Use sensitivity/recall, specificity, precision, and PR-style metrics for imbalanced data.

## Interpretation Notes

- Sensitivity is event capture; specificity is correctly ignored negatives.
- Threshold should match action capacity and error cost.
- Logistic coefficients are predictive associations, not intervention effects.

## Common Mistakes To Avoid

- Using random split for future prediction.
- Reporting accuracy only.
- Using leaky final status fields.
- Selecting threshold after many test-set attempts.

