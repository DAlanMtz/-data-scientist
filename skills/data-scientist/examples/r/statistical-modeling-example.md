# R Statistical Modeling Example

## Use Case

Run interpretable statistical modeling such as linear regression, logistic regression, or ANOVA-style comparisons with diagnostics and assumption checks.

## Expected Inputs

- Analysis question and outcome.
- Predictor variables and grouping variables.
- Data frame with documented grain and exclusions.

## Expected Outputs

- Fitted statistical model.
- Assumption/diagnostic checks.
- Effect estimates with uncertainty.
- Plain-language interpretation and limitations.

## Concise Workflow

1. State whether the goal is prediction, explanation, or causal estimation.
2. Inspect data and missingness.
3. Fit simple model.
4. Check diagnostics.
5. Interpret estimates with uncertainty.
6. Avoid causal claims unless design supports them.

## Representative Pattern

```r
library(tidyverse)
library(broom)

# Linear model
lm_fit <- lm(revenue ~ spend + tenure_days + plan + region, data = df)
summary(lm_fit)
tidy(lm_fit, conf.int = TRUE)
glance(lm_fit)

par(mfrow = c(2, 2))
plot(lm_fit)

# Logistic model
glm_fit <- glm(churned ~ active_days_30d + plan + support_tickets,
               data = df,
               family = binomial())
tidy(glm_fit, conf.int = TRUE, exponentiate = TRUE)

# ANOVA-style group comparison
aov_fit <- aov(revenue ~ plan, data = df)
summary(aov_fit)
TukeyHSD(aov_fit)
```

## Validation And Quality Checks

- Check outcome type matches model family.
- Review missingness and exclusion impact.
- Inspect residuals, leverage, and heteroscedasticity for linear models.
- Check separation or rare outcomes for logistic models.
- Correct for multiple comparisons when many groups/tests are explored.

## Interpretation Notes

- Linear coefficients are expected outcome differences holding included variables constant.
- Logistic odds ratios are multiplicative changes in odds, not probabilities.
- ANOVA indicates group mean differences; it does not explain why groups differ.
- Association is not causation without design support.

## Common Mistakes To Avoid

- Treating p-values as effect size.
- Ignoring model assumptions.
- Controlling for post-treatment variables in causal questions.
- Overstating observational findings as causal.
- Hiding non-significant but practically important uncertainty.

## Variable Selection

### Classical Methods (Use for Interpretable Statistical Models)

Backward elimination, forward selection, and stepwise selection are classical tools. Use for explanatory modeling where stakeholder interpretability of the variable-selection process is required. Treat as exploratory for prediction — nest inside validation if estimating predictive performance.

```r
library(MASS)  # stepAIC

# Fit full model
full_model <- lm(revenue ~ spend + tenure_days + plan + region + 
                   support_tickets + active_days_30d, 
                 data = train_df)

# Backward elimination by AIC
step_back <- stepAIC(full_model, direction = "backward", trace = FALSE)
summary(step_back)

# Forward selection by AIC
null_model <- lm(revenue ~ 1, data = train_df)
step_fwd <- stepAIC(null_model, 
                    scope = list(lower = null_model, upper = full_model),
                    direction = "forward", trace = FALSE)
summary(step_fwd)

# Stepwise (bidirectional)
step_both <- stepAIC(full_model, direction = "both", trace = FALSE)
summary(step_both)
```

**Guardrail**: The above uses AIC on training data. If you need unbiased predictive performance, repeat the entire stepAIC inside each cross-validation fold — do not select variables on the full dataset and then estimate performance on a held-out set.

### Regularization-Based Selection (Preferred for Prediction)

```r
library(glmnet)

# Prepare matrix form
X_train <- model.matrix(revenue ~ spend + tenure_days + plan + region + 
                          support_tickets + active_days_30d, 
                        data = train_df)[, -1]
y_train <- train_df$revenue

# LASSO: lambda chosen by cross-validation
lasso_cv <- cv.glmnet(X_train, y_train, alpha = 1)
plot(lasso_cv)
coef(lasso_cv, s = "lambda.1se")  # 1-SE rule for parsimony

# Ridge
ridge_cv <- cv.glmnet(X_train, y_train, alpha = 0)

# Elastic net (alpha = 0.5 balances L1 and L2)
enet_cv <- cv.glmnet(X_train, y_train, alpha = 0.5)

# Evaluate on test set
X_test <- model.matrix(revenue ~ spend + tenure_days + plan + region + 
                         support_tickets + active_days_30d, 
                       data = test_df)[, -1]
pred_lasso <- predict(lasso_cv, newx = X_test, s = "lambda.1se")
mae_lasso <- mean(abs(test_df$revenue - pred_lasso))
cat("LASSO MAE:", mae_lasso, "\n")
```

### Best Subsets (Small Predictor Sets Only)

```r
library(leaps)

subsets <- regsubsets(revenue ~ spend + tenure_days + plan + region + 
                        support_tickets + active_days_30d, 
                      data = train_df,
                      nvmax = 8)
summary_sub <- summary(subsets)

# Select by BIC
best_bic <- which.min(summary_sub$bic)
cat("Best model by BIC has", best_bic, "variables\n")
coef(subsets, best_bic)
```

