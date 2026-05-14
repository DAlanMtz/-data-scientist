# Python NLP Example

## Use Case

Build a simple supervised text classifier, such as support ticket routing, review classification, complaint detection, or intent classification.

## Expected Inputs

- Text column and label column.
- Label definitions and examples.
- Metadata for time/source/entity split if needed.
- Privacy constraints for raw text.

## Expected Outputs

- TF-IDF baseline pipeline.
- Evaluation metrics.
- Confusion matrix and error examples.
- Interpretation from top terms or example review.

## Concise Workflow

1. Inspect text quality and labels.
2. Split data before fitting vectorizer.
3. Build TF-IDF + linear classifier pipeline.
4. Evaluate per class.
5. Review false positives/false negatives.
6. Check privacy and bias risks.

## Representative Pattern

```python
import pandas as pd
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import classification_report, confusion_matrix
from sklearn.model_selection import train_test_split
from sklearn.pipeline import Pipeline

text_col = "ticket_text"
target = "category"

data = df[[text_col, target]].dropna()
X_train, X_test, y_train, y_test = train_test_split(
    data[text_col], data[target],
    test_size=0.2, stratify=data[target], random_state=42
)

model = Pipeline([
    ("tfidf", TfidfVectorizer(
        lowercase=True,
        ngram_range=(1, 2),
        min_df=3,
        max_df=0.9
    )),
    ("clf", LogisticRegression(max_iter=1000))
])

model.fit(X_train, y_train)
pred = model.predict(X_test)
print(confusion_matrix(y_test, pred))
print(classification_report(y_test, pred))

errors = pd.DataFrame({
    "text": X_test,
    "actual": y_test,
    "predicted": pred
})
display(errors[errors["actual"] != errors["predicted"]].head(20))
```

## Validation And Quality Checks

- Split by customer/account/time if near-duplicate text repeats.
- Review label quality and ambiguous examples.
- Keep negation words if sentiment/intent needs them.
- Redact PII before sharing examples.
- Evaluate by source, language, document length, and class.

## Interpretation Notes

- TF-IDF + linear model is a strong transparent baseline.
- Use top terms, representative errors, and confusion patterns for explanation.
- Do not infer sensitive traits or intent beyond validated labels.

## Common Mistakes To Avoid

- Fitting vectorizer before train/test split.
- Letting duplicate documents leak across splits.
- Treating topic model labels as ground truth.
- Reporting only overall accuracy for imbalanced classes.
- Putting raw private text in reports.

