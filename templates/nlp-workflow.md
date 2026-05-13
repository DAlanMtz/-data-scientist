# NLP Workflow

Use this workflow for text mining, text classification, entity extraction, topic discovery, sentiment, semantic search, retrieval, text clustering, or document analysis.

## Required Inputs

- Text source and document grain.
- Business question or action.
- Labels if supervised.
- Language, domain, and privacy constraints.
- Metadata for time, source, author/customer/account, or segment.
- Evaluation criteria and human review expectations.

## Expected Outputs

- Clean text dataset with metadata.
- Baseline text representation.
- Candidate NLP method results.
- Evaluation metrics and error examples.
- Bias/privacy review.
- Recommendation for analysis, deployment, or human review.

## Step-By-Step Workflow

### 1. Define Text Unit And Objective

Specify:

- Text unit: message, review, ticket, document, paragraph, query, transcript.
- Task: classify, extract, cluster, retrieve, summarize, score sentiment, or explore themes.
- Intended action.
- Label source and quality, if any.
- Whether output is advisory or automated.

### 2. Inspect Text Data

Check:

- Document counts.
- Duplicates and near-duplicates.
- Empty or boilerplate text.
- Language mix.
- Length distribution.
- Encoding issues.
- PII or sensitive content.
- Time/source/segment coverage.

Repeated text across train/test can inflate results.

### 3. Text Cleaning

Decide deliberately:

- Lowercasing.
- HTML or markup removal.
- Punctuation handling.
- Number handling.
- URL/email/phone masking.
- Lemmatization or stemming.
- Domain-specific replacements.

Do not over-clean when capitalization, punctuation, or numbers carry meaning.

### 4. Tokenization, Stopwords, And N-Grams

Use:

- Word or subword tokenization.
- Character n-grams for noisy text.
- Word n-grams for phrases.
- Stopword removal for bag-of-words tasks when useful.

Keep negation words when sentiment or intent depends on them.

### 5. Represent Text

Options:

- Keyword/rule flags for transparent baselines.
- Bag-of-words.
- TF-IDF.
- Topic model features.
- Static or contextual embeddings.
- Domain-specific embeddings where available.

Start with interpretable baselines before opaque embeddings.

### 6. Topic Modeling And Text Clustering

Use for exploration:

- Topic models.
- Embedding clustering.
- Term/keyphrase extraction.
- Representative document review.

Validate topics with human review. Do not treat topics as ground truth.

### 7. Sentiment Analysis

Use sentiment only when it matches the business question.

Check:

- Domain language.
- Sarcasm/negation.
- Mixed sentiment in long documents.
- Label or lexicon validity.
- Segment bias.

Report examples, not only sentiment scores.

### 8. Text Classification

For supervised tasks:

- Define labels and ambiguous cases.
- Split by entity or time when text repeats.
- Build baseline: keyword, TF-IDF + linear model, or current rule.
- Compare candidate models.
- Evaluate per class.
- Review false positives and false negatives.

Use calibration if probabilities drive action.

### 9. Entity Extraction

For NER or information extraction:

- Define entity schema.
- Create annotation rules and examples.
- Evaluate exact and partial matches.
- Review false positives/negatives by entity type.
- Protect extracted PII.

High-impact extraction needs human review or confidence thresholds.

### 10. Retrieval-Style Use Cases

For search, semantic retrieval, or RAG-like retrieval:

- Define query types and corpus.
- Build relevance test set.
- Compare keyword, vector, and hybrid retrieval.
- Evaluate recall@k, precision@k, MRR, and qualitative examples.
- Monitor stale, duplicated, restricted, or low-quality documents.

Retrieval quality is measured against user information needs, not embedding elegance.

## Validation And Evaluation Guidance

- Classification: precision, recall, F1, PR-AUC, confusion matrix.
- Extraction: precision/recall/F1 by entity type.
- Retrieval: recall@k, precision@k, MRR, NDCG.
- Topics/clusters: coherence, representative examples, human validation.
- Sentiment: label agreement and example review.

Always include error examples.

## Interpretation Guidance

- Explain models with top terms, representative examples, nearest neighbors, or local explanations.
- State label ambiguity and annotation limits.
- Avoid claiming intent, emotion, or sensitive traits beyond evidence.
- Separate theme discovery from quantified population conclusions.

## Common Failure Modes

- Duplicate text leakage.
- Label definitions are inconsistent.
- Boilerplate dominates features.
- Stopword removal deletes meaningful negation.
- Embeddings used without evaluation.
- Word clouds treated as evidence.
- PII appears in reports or logs.
- Model works on one source but fails on another.

## Responsible-Use Notes

- Review privacy before storing text or embeddings.
- Do not infer sensitive traits without legitimate purpose and safeguards.
- Use human review for high-impact text decisions.
- Monitor language and topic drift.

## Tool-Flexible Notes

- Python/R: use text pipelines, vectorizers, embeddings, and reproducible splits.
- SQL: prefilter, sample, deduplicate, and join metadata.
- Excel/Sheets: useful for annotation review and error analysis tables.
- Notebooks: pair metrics with representative text examples.
- Production pipelines: version preprocessing, model, labels, prompt/rules if used, and retrieval corpus.

