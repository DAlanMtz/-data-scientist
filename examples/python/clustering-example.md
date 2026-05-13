# Python Clustering Example

## Use Case

Create exploratory customer, product, store, or behavior segments without labels.

## Expected Inputs

- Entity-level feature table.
- Intended segmentation use.
- Numeric/categorical features measured over comparable windows.

## Expected Outputs

- Scaled feature matrix.
- Candidate `k` comparison.
- Cluster labels.
- Cluster profiles and business naming notes.
- Stability/actionability caveats.

## Concise Workflow

1. Choose meaningful entity-level features.
2. Impute and scale.
3. Compare cluster counts using inertia and silhouette.
4. Fit selected clustering model.
5. Profile clusters in original feature space.
6. Name clusters only after stakeholder-friendly profiling.

## Representative Pattern

```python
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
from sklearn.decomposition import PCA
from sklearn.impute import SimpleImputer
from sklearn.metrics import silhouette_score
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler

entity_id = "customer_id"
features = ["orders_90d", "spend_90d", "active_days_30d", "refund_rate", "tenure_days"]
X = df.set_index(entity_id)[features]

pipe = Pipeline([
    ("imputer", SimpleImputer(strategy="median")),
    ("scaler", StandardScaler())
])
X_scaled = pipe.fit_transform(X)

rows = []
for k in range(2, 9):
    km = KMeans(n_clusters=k, n_init=20, random_state=42)
    labels = km.fit_predict(X_scaled)
    rows.append({
        "k": k,
        "inertia": km.inertia_,
        "silhouette": silhouette_score(X_scaled, labels)
    })

scores = pd.DataFrame(rows)
display(scores)

k = 4
km = KMeans(n_clusters=k, n_init=20, random_state=42)
clusters = km.fit_predict(X_scaled)

profile = X.assign(cluster=clusters).groupby("cluster").agg(["count", "mean", "median"])
display(profile)

pca = PCA(n_components=2, random_state=42)
xy = pca.fit_transform(X_scaled)
plt.scatter(xy[:, 0], xy[:, 1], c=clusters, alpha=0.5)
plt.title("PCA view of clusters: exploratory only")
plt.show()
```

## Validation And Quality Checks

- Check sensitivity to scaling, outliers, feature set, and random seed.
- Confirm clusters are not just missingness/source artifacts.
- Review cluster sizes and minimum actionability.
- Use silhouette/inertia as diagnostics, not final proof.
- Profile clusters using variables not used in fitting when possible.

## Interpretation Notes

- Clusters are constructed segments, not natural truth.
- Name clusters from differentiating behaviors, not value judgments.
- PCA plot helps visualization but does not validate cluster reality.

## Common Mistakes To Avoid

- Clustering raw unscaled numeric features.
- Letting spend magnitude dominate all segments unintentionally.
- Choosing `k` only from elbow plot.
- Naming clusters before profiling.
- Making causal claims from cluster membership.

