# Recommendation Workflow

Use this workflow to recommend products, content, offers, actions, people, documents, next-best actions, or ranked items for users or contexts.

## Required Inputs

- Recommendation objective and business action.
- User, item, and event data.
- Feedback type: explicit ratings or implicit behavior.
- Candidate set and eligibility rules.
- Time window and deployment context.
- Evaluation metric and business guardrails.

## Expected Outputs

- Baseline recommender.
- Candidate recommendation approach.
- Offline ranking evaluation.
- Cold-start and coverage assessment.
- Diversity, novelty, fairness, and business constraint review.
- Online testing or deployment recommendation.

## Step-By-Step Workflow

### 1. Frame The Recommendation Problem

Define:

- Who receives recommendations.
- What can be recommended.
- Where recommendations appear.
- How many items are shown.
- What action counts as success.
- Business rules: eligibility, inventory, compliance, margin, freshness.

Recommendation quality depends on the user experience and decision context.

### 2. Prepare User, Item, And Event Data

Build:

- User table with stable attributes.
- Item table with content attributes and availability.
- Event table with user-item interactions and timestamps.
- Exposure data if available.

Measure:

- Sparsity.
- Interaction volume.
- Active users/items.
- Time coverage.
- Popularity concentration.

### 3. Define Feedback

Explicit feedback:

- Ratings, likes, survey preferences.
- Usually cleaner but sparse.

Implicit feedback:

- Clicks, views, purchases, watch time, saves, replies.
- Abundant but biased by exposure and interface.

Define positive, negative, and unknown interactions carefully. A missing interaction is not always dislike.

### 4. Build Popularity Baseline

Start with:

- Overall popularity.
- Recent popularity.
- Segment-specific popularity.
- Business-rule ranking.

This baseline is hard to beat and exposes offline evaluation issues.

### 5. Candidate Methods

Consider:

- Content-based filtering using item/user attributes.
- Collaborative filtering.
- Matrix factorization.
- Sequence or session-based recommenders.
- Hybrid recommenders combining content, collaborative, and business rules.
- Two-stage systems: candidate generation plus ranking.

Choose based on data volume, sparsity, cold-start needs, and interpretability.

### 6. Content-Based Filtering

Use when:

- Item metadata is rich.
- User history is limited.
- Cold-start items matter.
- Explanations are important.

Features may include categories, text embeddings, tags, price, brand, topic, or attributes.

### 7. Collaborative Filtering And Matrix Factorization

Use when:

- User-item interaction matrix has enough density.
- Similar users/items are meaningful.
- Historical behavior predicts future preference.

Guardrails:

- Use time-aware validation.
- Account for popularity bias.
- Avoid recommending unavailable or already-consumed items unless repeat behavior is valid.

### 8. Hybrid Recommenders

Use when combining:

- Collaborative score.
- Content score.
- Popularity/recency.
- Business value.
- Diversity constraints.
- Eligibility filters.

Keep the final ranking formula auditable.

### 9. Cold Start

Handle:

- New users: onboarding preferences, contextual recommendations, popularity, segment rules.
- New items: content-based similarity, editorial boosts, exploration slots.
- Sparse users/items: backoff to broader segment.

Report cold-start performance separately.

### 10. Offline Evaluation

Use:

- Time-aware holdout.
- Precision@k.
- Recall@k.
- NDCG@k.
- MAP or MRR.
- Hit rate@k.
- Coverage.
- Diversity and novelty.

Evaluate at the actual number of recommendations shown.

### 11. Online Evaluation

Offline metrics may not predict business impact.

Use:

- A/B test where possible.
- CTR, conversion, revenue, retention, satisfaction.
- Guardrails: complaints, unsubscribes, returns, fatigue, latency.
- Long-term metrics for recommendation loops.

Do not launch solely on offline lift if the decision is consequential or customer-facing.

### 12. Business Constraints

Apply:

- Inventory and availability.
- Margin or value constraints.
- Policy exclusions.
- Frequency caps.
- Diversity minimums.
- Fair exposure rules.
- Freshness requirements.

Business constraints should be explicit, versioned, and monitored.

## Validation And Evaluation Guidance

- Use time-aware splits.
- Compare to popularity baseline.
- Separate candidate-generation and ranking metrics.
- Evaluate cold-start and high-activity users separately.
- Watch exposure bias in implicit feedback.

## Interpretation Guidance

- Explain recommendations through similar items, content attributes, user behavior, or business rule.
- Avoid presenting inferred preferences as certain.
- Report coverage and diversity alongside relevance.

## Common Failure Modes

- Random split leaks future interactions.
- Missing interaction treated as negative without reason.
- Popularity bias improves clicks but reduces discovery.
- Offline metric ignores availability or UI position.
- Recommender repeats stale items.
- Cold-start users receive poor recommendations.
- Feedback loops narrow user experience.

## Responsible-Use Notes

- Monitor fairness in exposure and opportunity.
- Avoid sensitive inference or manipulative targeting.
- Provide user controls where appropriate.
- Watch for filter bubbles and harmful amplification.

## Tool-Flexible Notes

- Python/R: build sparse matrices, ranking evaluation, and model comparison.
- SQL: create interaction tables, candidate sets, and popularity baselines.
- Excel/Sheets: useful for business-rule review and stakeholder examples.
- Notebooks: show example recommendations for representative users.
- Production pipelines: separate candidate generation, ranking, filtering, logging, and monitoring.

