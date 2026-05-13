# Clustering Workflow

Use this workflow for segmentation or pattern discovery without labels, such as customer segments, product groups, behavioral archetypes, document clusters, or operational profiles.

## Required Inputs

- Segmentation objective and intended action.
- Entity grain: customer, account, product, session, document, store, or transaction.
- Candidate features measured over comparable windows.
- Exclusions and population scope.
- Business constraints on number and size of segments.

## Expected Outputs

- Clustering-ready feature matrix.
- Candidate clustering comparison.
- Cluster profiles and business names.
- Stability and quality assessment.
- Recommended segment use and limitations.

## Step-By-Step Workflow

### 1. Frame The Segmentation

Define:

- What entity is being segmented.
- What decision or strategy segments will support.
- Whether segments should be stable, behavior-based, value-based, or exploratory.
- Minimum useful segment size.
- Features that should not define segments.

If no action can differ by segment, clustering may not be useful.

### 2. Select Features

Choose features that represent meaningful differences:

- Behavior, frequency, recency, value, preferences, usage, content, or operational patterns.
- Avoid raw identifiers.
- Avoid target/outcome fields unless intentionally creating outcome-based segments.
- Align observation windows across entities.
- Remove redundant features when they dominate distance.

Document why each feature family belongs.

### 3. Clean And Scale

Prepare:

- Missing values.
- Skewed numeric variables.
- Categorical encoding.
- Feature scaling for distance-based methods.
- Outlier handling.
- High-cardinality text or sparse features.

Scaling choice can determine clusters. Record it.

### 4. Dimensionality Reduction

Use when features are high-dimensional, correlated, sparse, or hard to visualize.

Options:

- PCA for numeric compression.
- Factor analysis for survey constructs.
- UMAP/t-SNE for exploratory visualization.
- Embeddings for text or item similarity.

Do not treat a 2D projection as proof that clusters exist.

### 5. Candidate Methods

Use:

- K-means for compact spherical clusters.
- Hierarchical clustering for nested structure and small/medium data.
- Gaussian mixtures for soft membership.
- DBSCAN/HDBSCAN for density-based clusters and noise points.
- Business rules when interpretability and actionability matter more than algorithmic grouping.

Match method to feature geometry and business need.

### 6. Choose Number Of Clusters

Use:

- Elbow plot.
- Silhouette score.
- Stability across seeds/samples.
- Minimum segment size.
- Business interpretability.
- Downstream KPI separation.

Do not select `k` using one metric alone.

### 7. Evaluate Cluster Quality

Check:

- Silhouette score.
- Davies-Bouldin or Calinski-Harabasz.
- Cluster sizes.
- Distance/membership uncertainty.
- Stability across seeds and samples.
- Stability across time.
- Business usefulness.

Internal metrics are secondary to stability and actionability.

### 8. Profile Clusters

For each cluster:

- Size and share.
- Top differentiating features.
- Important behaviors.
- Business value or risk.
- Representative examples.
- Recommended action.
- Caveats.

Compare clusters to features not used in clustering to understand external meaning.

### 9. Name Clusters

Use names that are:

- Plain language.
- Behavior-based.
- Non-pejorative.
- Actionable.
- Stable enough for reporting.

Avoid names that imply causality or moral judgment.

### 10. Validate Use

Test:

- Can stakeholders recognize and use the segments?
- Are segments stable enough over time?
- Do actions differ by segment?
- Does segment assignment work for new entities?
- Are there fairness or proxy concerns?

## Validation And Evaluation Guidance

- Use multiple random seeds.
- Refit on bootstrap samples.
- Compare cluster profiles across time.
- Check sensitivity to scaling, feature set, and outliers.
- Measure segment stability before operational use.

## Interpretation Guidance

- Clusters are constructed summaries, not natural laws.
- Explain each cluster by differentiating features and examples.
- State whether membership is hard or uncertain.
- Use segments to guide hypotheses or actions, not to stereotype people.

## Common Failure Modes

- Clustering because there is no target, not because segments will be used.
- Features at different scales dominate results.
- Clusters reflect missingness or data source artifacts.
- Too many small segments.
- Projection plot oversold as validation.
- Segment names imply unsupported causal stories.

## Tool-Flexible Notes

- Python/R: use scaling pipelines and reproducible seeds.
- SQL: create entity-level feature tables and profile clusters after assignment.
- Excel/Sheets: useful for cluster profile tables and stakeholder naming workshops.
- Notebooks: keep method comparison and cluster profiles together.
- Production pipelines: define how new entities receive cluster labels and monitor segment drift.

