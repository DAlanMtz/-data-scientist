# Recommendation Checklist

Use for recommender systems, ranking, next-best-action, personalization, or content/product matching review.

## Objective And Grain

- [ ] Recommendation objective is stated.
- [ ] User, item, and event grain are defined.
- [ ] Placement/interface and number of recommendations are known.
- [ ] Candidate set and eligibility rules are documented.
- [ ] Success action is defined: click, purchase, save, retention, value, etc.
- [ ] Business guardrails are defined.

## Feedback And Data

- [ ] Explicit feedback is distinguished from implicit feedback.
- [ ] Missing interaction is not automatically treated as negative.
- [ ] Exposure data is used or its absence is documented.
- [ ] Interaction timestamps are available.
- [ ] User/item metadata quality is checked.
- [ ] Popularity concentration and sparsity are measured.
- [ ] Train/test split is time-aware.

## Baselines And Methods

- [ ] Popularity baseline is included.
- [ ] Recent popularity or segment popularity baseline is considered.
- [ ] Content-based filtering is considered.
- [ ] Collaborative filtering is considered when interaction data supports it.
- [ ] Matrix factorization is considered for sparse interaction matrices.
- [ ] Hybrid ranking is considered when business rules matter.
- [ ] Candidate generation and ranking are evaluated separately when two-stage.

## Cold Start

- [ ] New user strategy is defined.
- [ ] New item strategy is defined.
- [ ] Sparse user/item fallback is defined.
- [ ] Onboarding or contextual signals are considered.
- [ ] Cold-start performance is reported separately.

## Evaluation

- [ ] Offline metrics match actual `k`.
- [ ] Precision@k, recall@k, NDCG, MAP, MRR, or hit rate are used appropriately.
- [ ] Coverage is measured.
- [ ] Diversity is measured.
- [ ] Novelty or long-tail exposure is considered.
- [ ] Business value metrics are included.
- [ ] Offline-online mismatch is acknowledged.
- [ ] Online A/B test or shadow evaluation is planned when user-facing.

## Business Constraints

- [ ] Availability/inventory filters are applied.
- [ ] Already-consumed item behavior is defined.
- [ ] Frequency caps are considered.
- [ ] Policy/compliance exclusions are applied.
- [ ] Margin/value constraints are explicit.
- [ ] Freshness requirements are defined.
- [ ] Ranking formula or business rules are auditable.

## Fairness And Feedback Loops

- [ ] Popularity bias is measured.
- [ ] Exposure fairness is reviewed where relevant.
- [ ] Creator/supplier/item group coverage is monitored where relevant.
- [ ] Filter bubble or over-personalization risk is considered.
- [ ] Feedback loops are monitored after launch.
- [ ] User controls or explanations are considered.

## Monitoring

- [ ] Recommendation coverage is monitored.
- [ ] Click/conversion/retention metrics are monitored.
- [ ] Diversity, novelty, and freshness are monitored.
- [ ] Latency and failure rate are monitored.
- [ ] Guardrails such as unsubscribes, complaints, returns, or fatigue are monitored.
- [ ] Model and candidate-set versions are logged.

## Minimum Acceptable Standard

- [ ] Popularity baseline, time-aware split, ranking metrics at actual `k`, cold-start review, and business constraints are included.

## Strong Practice

- [ ] Online experiment measures primary value and guardrails.
- [ ] Candidate generation, ranking, filters, and logging are versioned separately.
- [ ] Recommendations include reason codes or user-facing explanations where useful.

## Red Flags

- [ ] Random split leaks future interactions.
- [ ] Offline evaluation ignores exposure bias.
- [ ] Metric improves only by recommending the most popular items.
- [ ] Recommender suggests unavailable or ineligible items.
- [ ] No plan for cold-start users or items.
- [ ] User-facing launch planned with no guardrail monitoring.

