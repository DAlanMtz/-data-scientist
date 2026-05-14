# R Clustering Example

## Use Case

Create exploratory segments using R with scaled features, k-means or hierarchical clustering, and cluster profiling.

## Expected Inputs

- Entity-level feature table.
- Segmentation objective and intended use.
- Numeric features measured over comparable windows.

## Expected Outputs

- Scaled feature matrix.
- Candidate cluster count diagnostics.
- Cluster assignments.
- Cluster profile table.
- Business naming notes.

## Concise Workflow

1. Select meaningful features.
2. Impute and scale.
3. Compare candidate cluster counts.
4. Fit k-means or hierarchical clustering.
5. Profile clusters in original units.
6. Review actionability and stability.

## Representative Pattern

```r
library(tidyverse)
library(cluster)

features <- c("orders_90d", "spend_90d", "active_days_30d", "refund_rate", "tenure_days")
X <- df %>% select(all_of(features))

X_clean <- X %>%
  mutate(across(everything(), ~ replace_na(.x, median(.x, na.rm = TRUE))))

X_scaled <- scale(X_clean)

set.seed(42)
scores <- map_dfr(2:8, function(k) {
  km <- kmeans(X_scaled, centers = k, nstart = 25)
  sil <- silhouette(km$cluster, dist(X_scaled))
  tibble(k = k, tot_withinss = km$tot.withinss, silhouette = mean(sil[, 3]))
})
print(scores)

km <- kmeans(X_scaled, centers = 4, nstart = 25)
clustered <- df %>% mutate(cluster = factor(km$cluster))

profile <- clustered %>%
  group_by(cluster) %>%
  summarise(
    n = n(),
    across(all_of(features), list(mean = mean, median = median), na.rm = TRUE),
    .groups = "drop"
  )
print(profile)

hc <- hclust(dist(X_scaled), method = "ward.D2")
plot(hc)
```

## Validation And Quality Checks

- Check sensitivity to scaling, features, outliers, and random seed.
- Use silhouette and elbow diagnostics, but do not let them replace actionability.
- Confirm clusters are not just missingness or data source artifacts.
- Review segment sizes and stability.

## Interpretation Notes

- Cluster names should describe behavior, not imply causality or worth.
- Hierarchical dendrogram helps inspect structure; k-means gives operational labels.
- Profile in original units so stakeholders can understand segments.

## Common Mistakes To Avoid

- Clustering at transaction grain when customer grain is intended.
- Using unscaled features with different units.
- Choosing too many tiny clusters.
- Overinterpreting a 2D plot.

