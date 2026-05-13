# Unsupervised Learning Checklist

Use for clustering, dimensionality reduction, segmentation, topic discovery, or pattern mining when no target label is used.

## Objective And Use

- [ ] Unsupervised objective is clear: segmentation, compression, exploration, anomaly support, visualization, or feature creation.
- [ ] Intended business action or analysis use is stated.
- [ ] Entity grain is defined.
- [ ] Population and time window are defined.
- [ ] Stakeholders can explain how outputs will be used.

## Feature Selection

- [ ] Features represent meaningful behavior or attributes.
- [ ] Observation windows are comparable across entities.
- [ ] IDs and arbitrary codes are excluded unless intentionally encoded.
- [ ] Outcome-like fields are excluded unless creating descriptive outcome segments intentionally.
- [ ] Highly redundant features are reviewed.
- [ ] Missingness artifacts are not driving the structure.

## Preprocessing

- [ ] Numeric features are scaled when distance matters.
- [ ] Skewed variables are transformed or handled deliberately.
- [ ] Categorical encoding is appropriate for method and cardinality.
- [ ] Outliers are identified before fitting.
- [ ] Sparse text or event features are represented appropriately.
- [ ] Preprocessing choices are documented.

## Dimensionality Reduction

- [ ] PCA/factor/embedding/UMAP/t-SNE purpose is stated.
- [ ] PCA or factor analysis uses appropriate scaling.
- [ ] Explained variance or loadings are reviewed where applicable.
- [ ] 2D projections are treated as exploratory, not proof.
- [ ] Dimensionality reduction is fit inside validation if used for supervised downstream modeling.

## Clustering Methods

- [ ] K-means assumptions are reasonable if used.
- [ ] Hierarchical clustering is reviewed with dendrogram or linkage rationale.
- [ ] DBSCAN/HDBSCAN is considered when density/noise structure matters.
- [ ] Gaussian mixture or soft membership is considered when uncertainty matters.
- [ ] Business-rule segmentation is considered as a baseline.

## Number Of Clusters

- [ ] Inertia/elbow is reviewed where relevant.
- [ ] Silhouette score is reviewed where relevant.
- [ ] Dendrogram is reviewed for hierarchical clustering.
- [ ] Minimum segment size is checked.
- [ ] Number of clusters is usable by stakeholders.
- [ ] Choice of `k` is not based on one metric alone.

## Stability And Validation Without Labels

- [ ] Results are stable across seeds.
- [ ] Results are stable across samples or bootstrap runs.
- [ ] Results are stable across time if operationalized.
- [ ] Cluster profiles remain meaningful under reasonable preprocessing changes.
- [ ] External variables not used in clustering are used for interpretation.
- [ ] Stakeholder review confirms usability.

## Cluster Profiling And Naming

- [ ] Each cluster has size/share.
- [ ] Each cluster has top differentiating features.
- [ ] Representative examples are reviewed.
- [ ] Business names are plain-language and non-pejorative.
- [ ] Recommended action or interpretation is attached to each segment.
- [ ] Uncertain or border cases are acknowledged.

## Claims And Interpretation

- [ ] Clusters are described as constructed segments, not natural truth.
- [ ] No causal claims are made from unsupervised structure.
- [ ] Cluster membership is not treated as a protected-class proxy without review.
- [ ] Results are not used for eligibility or high-impact decisions without responsible review.

## Minimum Acceptable Standard

- [ ] Objective, grain, feature set, preprocessing, cluster quality, profiles, and actionability are documented.
- [ ] Stability has been checked enough for the intended use.

## Strong Practice

- [ ] Business-rule baseline is compared to algorithmic clusters.
- [ ] Segment drift monitoring is defined for recurring use.
- [ ] Cluster assignment process for new records is documented.

## Red Flags

- [ ] Clustering is used because there is no target, not because segments are useful.
- [ ] Features at larger scales dominate results accidentally.
- [ ] Clusters mainly reflect missingness or source system.
- [ ] Segment names imply unsupported causal or value judgments.
- [ ] Stakeholders cannot say what they would do differently by segment.

