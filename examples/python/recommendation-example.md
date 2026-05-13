# Python Recommendation Example

## Use Case

Create a simple recommender baseline from user-item interactions and evaluate ranking quality before considering more complex collaborative filtering.

## Expected Inputs

- Interaction table with `user_id`, `item_id`, timestamp, and event strength.
- Item availability and metadata if available.
- Definition of a successful recommendation.

## Expected Outputs

- Popularity baseline.
- Simple item-similarity or co-occurrence pattern.
- Ranking metrics at `k`.
- Coverage and cold-start notes.

## Concise Workflow

1. Define interaction and candidate set.
2. Split interactions by time.
3. Build popularity baseline.
4. Optionally build item-item co-occurrence.
5. Evaluate hit rate/precision@k against future interactions.
6. Review diversity, novelty, and business constraints.

## Representative Pattern

```python
import pandas as pd

events = interactions.assign(event_time=pd.to_datetime(interactions["event_time"]))
cutoff = events["event_time"].quantile(0.8)
train = events[events["event_time"] <= cutoff]
test = events[events["event_time"] > cutoff]

k = 10
popular_items = (
    train.groupby("item_id")
         .size()
         .sort_values(ascending=False)
         .head(500)
         .index
         .tolist()
)

train_seen = train.groupby("user_id")["item_id"].apply(set).to_dict()
test_items = test.groupby("user_id")["item_id"].apply(set).to_dict()

def recommend_popular(user_id, k=10):
    seen = train_seen.get(user_id, set())
    return [item for item in popular_items if item not in seen][:k]

def precision_at_k(recs, truth, k):
    if not recs:
        return 0.0
    return len(set(recs[:k]) & truth) / k

def hit_rate_at_k(recs, truth, k):
    return float(len(set(recs[:k]) & truth) > 0)

rows = []
for user, truth in test_items.items():
    recs = recommend_popular(user, k)
    rows.append({
        "user_id": user,
        "precision_at_k": precision_at_k(recs, truth, k),
        "hit_at_k": hit_rate_at_k(recs, truth, k),
    })

eval_df = pd.DataFrame(rows)
print(eval_df[["precision_at_k", "hit_at_k"]].mean())

coverage = len(set(popular_items[:100])) / train["item_id"].nunique()
print("catalog coverage among top 100:", coverage)
```

## Validation And Quality Checks

- Use time-aware split; random split leaks future behavior.
- Do not treat missing interactions as dislikes without justification.
- Exclude unavailable or ineligible items.
- Evaluate at the actual number of recommendations shown.
- Report cold-start user/item behavior separately.

## Interpretation Notes

- Popularity is a serious baseline, not a throwaway.
- Precision@k measures relevance density; hit rate measures whether at least one recommendation works.
- Offline metrics may not predict online impact because exposure is biased.

## Common Mistakes To Avoid

- Evaluating on items users already consumed in training.
- Ignoring item availability or policy constraints.
- Optimizing clicks while harming diversity or user trust.
- Launching without online guardrails.
- Reporting relevance without coverage/diversity.

