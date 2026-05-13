# Interpretation Templates

Use these templates to translate technical output into stakeholder-ready language. Replace bracketed text with project-specific details and avoid causal wording unless the design supports it.

## Regression

Template:

> The model predicts [numeric outcome] for [population] using information available at [prediction point]. On the validation set, typical error was [MAE/median error], with larger misses around [segments or conditions]. The strongest predictive signals were [features], which means the model is mainly distinguishing [plain-language pattern]. This should be used for [decision], not as a precise value for every individual case.

Coefficient phrasing:

> Holding the modeled inputs constant, a one-unit increase in [feature] is associated with an estimated [change] in [outcome]. This is predictive association, not proof that changing [feature] will cause [outcome] to change.

## Logistic Classification

Template:

> The model estimates the probability that [event] will occur within [outcome window]. A score of [x] means the model ranks this case as higher risk than lower-scored cases; use calibration diagnostics before treating it as an exact probability. At threshold [t], the model identifies [recall] of true positives and [precision] of flagged cases are true positives.

Threshold phrasing:

> Lowering the threshold catches more [events] but increases false positives and workload. Raising it reduces workload but misses more [events]. The recommended threshold is [t] because it best matches [cost/capacity/business objective].

## Multiclass Classification

Template:

> The model assigns each case to one of [classes]. Overall performance was [metric], but the important pattern is class-level performance: it performs best on [classes] and struggles with [classes]. The most common confusion is [class A] predicted as [class B], which matters because [business consequence].

Top-k phrasing:

> When the correct class only needs to appear among the top [k] suggestions, performance improves to [top-k metric]. This supports [human review/triage workflow] better than fully automated assignment.

## Confusion Matrices

Template:

> At the selected threshold, the model produced [TP] true positives, [FP] false positives, [FN] false negatives, and [TN] true negatives. The main business tradeoff is between [false positive consequence] and [false negative consequence]. The largest concern is [dominant error type], especially for [segment].

Use counts and rates. Do not show only percentages when the base rate matters.

## ROC And AUC

Template:

> ROC AUC of [value] means the model generally ranks positive cases above negative cases. It does not say whether the selected threshold is operationally good, and it can look strong even when rare-event precision is weak. For action planning, pair this with precision-recall, lift, calibration, and threshold metrics.

## Precision, Recall, And F1

Precision:

> Of the cases the model flags, [precision] are true [events]. This answers, "How much review effort is productive?"

Recall:

> Of all actual [events], the model catches [recall]. This answers, "How much of the problem do we find?"

F1:

> F1 summarizes precision and recall at one threshold. It is useful as a compact comparison, but it does not replace a cost or capacity-based threshold decision.

## Clustering

Template:

> The analysis groups [entities] into [k] segments based on [feature families]. Segment [name] represents [size/share] and is characterized by [top differentiators]. The segment appears actionable because [recommended action or decision]. Cluster labels are descriptive, not ground truth; stability and business usefulness matter more than the algorithm's assigned number.

Avoid:

- "The algorithm discovered true customer types."
- "Cluster 3 causes higher retention."

## PCA

Template:

> PCA reduced [number] correlated variables into components that summarize the main variation. Component [n] is most strongly loaded on [variables], so it can be interpreted cautiously as [plain-language theme]. The first [k] components explain [share] of variance. Use this for compression or exploration, not as proof of causal drivers.

## Factor Analysis

Template:

> Factor analysis suggests [k] latent constructs in the survey/items. Factor [name] is supported by high loadings from [items] and weak loadings from unrelated items. Reliability is [value/assessment]. Treat this as evidence that the items measure [construct], subject to survey design and sampling limitations.

## Forecasting

Template:

> The forecast estimates [metric] for [horizon] using data through [cutoff]. Backtests show typical error of [metric] and bias of [bias]. Accuracy is strongest for [segments/horizons] and weakest for [segments/horizons]. Forecast intervals show the plausible range, so planning should use [point forecast/upper bound/lower bound] depending on risk tolerance.

Baseline phrasing:

> The model improves over the [naive/seasonal naive/current process] baseline by [amount], which indicates it adds value beyond repeating recent history.

## Recommendation Systems

Template:

> The recommender ranks [items/actions] for [users/contexts]. Offline evaluation shows [metric@k], but final value depends on online behavior and exposure. The recommendations are driven by [similar users/items/content/recent behavior]. Monitor coverage, diversity, freshness, and feedback loops, not only clicks.

## Anomaly Detection

Template:

> The system flags this case because [features] differ from expected behavior for [entity/peer group/time]. The anomaly score indicates unusualness, not confirmed fraud/error/failure. Recommended next step is [review/action], with priority based on [severity/value/risk].

Alert performance:

> At the current threshold, the system creates about [n] alerts per [period], with reviewed precision of [precision] and known-incident recall of [recall if available].

## Association Rules

Template:

> The rule [A] -> [B] appears in [support] of transactions. Among transactions with [A], [confidence] also include [B]. Lift of [lift] means the combination occurs [lift] times more often than expected if independent. Consider this rule only if support is large enough and the action is plausible.

## Causal Analysis

Template:

> Under the assumptions of [experiment/design], [treatment] is estimated to change [outcome] by [effect] for [population] over [window]. This causal interpretation depends on [randomization/parallel trends/balance/instrument validity/running variable assumptions]. The strongest validity risks are [risks].

Non-causal fallback:

> This analysis shows an association between [feature] and [outcome]. It should not be interpreted as the effect of changing [feature].

## Feature Importance

Template:

> The most important features for prediction were [features]. Importance means these variables helped the model reduce error or separate classes; it does not mean they are causal, fair to use, or actionable. Review availability, stability, and proxy-risk before using them for decisions.

## Model Limitations

Template:

> The main limitations are [data limitation], [validation limitation], and [operational limitation]. These mean the results are reliable for [supported use] but not for [unsupported use]. Before deployment or broad use, address [required next step].

## Business Recommendations

Template:

> Based on the validation results and business constraints, the recommended action is [action]. Expected benefit is [benefit] with primary risk [risk]. Use [threshold/ranking/segment/policy] for [population], monitor [metrics], and revisit after [time/outcome volume/trigger].

Keep recommendations tied to a decision owner, an action, and a measurement plan.

