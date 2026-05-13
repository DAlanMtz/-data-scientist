# NLP Checklist

Use for text classification, extraction, clustering, topic modeling, sentiment analysis, search, retrieval, or text mining review.

## Text Source Quality

- [ ] Text unit is defined: message, review, ticket, document, query, transcript, etc.
- [ ] Source and collection process are understood.
- [ ] Language and domain are identified.
- [ ] Encoding issues are checked.
- [ ] Empty, boilerplate, templated, and duplicated text are measured.
- [ ] Text length distribution is reviewed.
- [ ] Metadata coverage is adequate for evaluation.

## Privacy And Sensitive Content

- [ ] PII is identified and handled.
- [ ] Sensitive attributes and proxy text are reviewed.
- [ ] Raw examples in reports are redacted where needed.
- [ ] Embedding storage and retention risk are considered.
- [ ] Consent and permitted use are checked.
- [ ] High-impact use has human review.

## Cleaning And Preprocessing

- [ ] Cleaning choices are documented.
- [ ] Tokenization is appropriate for language/domain.
- [ ] Stopword handling preserves meaningful negation.
- [ ] N-grams are considered for phrases.
- [ ] Numbers, URLs, emails, and punctuation are handled deliberately.
- [ ] Lemmatization/stemming is used only when helpful.
- [ ] Train/test text preprocessing avoids duplicate leakage.

## Representations

- [ ] Keyword or rule baseline is considered.
- [ ] Bag-of-words or TF-IDF baseline is considered.
- [ ] Embeddings are evaluated against simpler baselines.
- [ ] Topic modeling outputs are reviewed with representative examples.
- [ ] Vectorizer/embedding fitting respects validation split.
- [ ] Representation choice is compatible with production constraints.

## Supervised Label Quality

- [ ] Label definitions are documented.
- [ ] Ambiguous cases are handled.
- [ ] Annotator agreement or label consistency is reviewed where possible.
- [ ] Class balance is measured.
- [ ] Split is time-aware or entity-aware when text repeats.
- [ ] Labels are not derived from post-outcome notes unless appropriate.

## Evaluation

- [ ] Classification uses precision, recall, F1, confusion matrix, and PR-AUC when imbalanced.
- [ ] Extraction uses precision/recall/F1 by entity type.
- [ ] Retrieval uses recall@k, precision@k, MRR, or NDCG.
- [ ] Topic/clustering uses coherence plus human review.
- [ ] Error examples are inspected.
- [ ] Performance is checked by language, source, length, time, and segment.

## Retrieval-Specific Checks

- [ ] Corpus scope and freshness are defined.
- [ ] Restricted or private documents are filtered correctly.
- [ ] Query test set covers real user intents.
- [ ] Duplicate or near-duplicate documents are handled.
- [ ] Retrieval evaluation uses relevant negatives.
- [ ] Top-k matches user interface or downstream prompt needs.
- [ ] Failure examples are reviewed.

## Bias, Toxicity, And Human Review

- [ ] Toxic or abusive content handling is defined.
- [ ] Bias across dialect, language, source, or group is checked where relevant.
- [ ] Model does not infer sensitive traits without legitimate purpose and safeguards.
- [ ] Human review is required for high-impact text decisions.
- [ ] Misclassification harms are documented.

## Minimum Acceptable Standard

- [ ] Text quality, privacy, preprocessing, split strategy, baseline, metrics, and error examples are reviewed.

## Strong Practice

- [ ] Representative examples accompany every topic, class, extraction type, or retrieval result.
- [ ] Drift in language, topics, labels, or corpus freshness is monitored.
- [ ] Human annotation guidelines are versioned for supervised tasks.

## Red Flags

- [ ] Duplicate texts appear across train/test.
- [ ] Word clouds are used as primary evidence.
- [ ] Embeddings are accepted without baseline comparison.
- [ ] PII appears in reports or logs.
- [ ] Sentiment scores are used in a domain where they were not validated.
- [ ] Topic names are treated as objective truth.

