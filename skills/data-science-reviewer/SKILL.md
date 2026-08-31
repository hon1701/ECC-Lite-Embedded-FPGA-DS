---
name: data-science-reviewer
description: Review Python/Pandas/NumPy and classical machine-learning workflows for data correctness, leakage, split strategy, metrics, reproducibility, and report quality. Use for coursework, notebooks, fraud detection, EDA, preprocessing, model evaluation, or when code runs but conclusions may be wrong.
---

# Data Science Reviewer

The key question is not only "does the notebook run?" but "is the conclusion valid?"

## Review order

### 1. Business/analysis question
State:
- target;
- prediction/analysis unit;
- operational decision;
- success metric.

### 2. Data integrity
Check:
- shape and schema;
- dtypes;
- missing values;
- duplicates;
- impossible values;
- class distribution;
- timestamp/order issues.

### 3. Split before learning
Any transformation that learns from data should be fit on training data only:
- scaling;
- imputation statistics;
- encoding vocabularies when appropriate;
- feature selection;
- resampling.

Flag leakage aggressively.

### 4. Pandas/NumPy correctness
Inspect:
- `loc` vs `iloc`;
- chained assignment;
- index alignment;
- broadcasting;
- view vs copy;
- axis meaning;
- NaN behavior;
- dtype coercion.

### 5. Modeling
Check:
- baseline model exists;
- random seed/reproducibility;
- class imbalance handling;
- hyperparameters separated from final evaluation;
- probability vs hard-label usage.

For ranking/threshold tasks, use probability-like scores when the model supports them, e.g. `predict_proba(X)[:, 1]`, not `predict()`.

### 6. Metrics
Do not let accuracy dominate imbalanced classification.

Review:
- confusion matrix;
- precision;
- recall;
- F1;
- ROC-AUC;
- PR-AUC when imbalance is strong;
- threshold behavior;
- Top-k metrics when operations act on a limited queue.

For fraud-style Top-k:
1. sort descending by score;
2. take top `k%`;
3. compute captured positives and precision in that review set.

### 7. Sanity checks
For score columns:
- expected range if probabilistic;
- enough unique values;
- no NaN/inf;
- ranking direction correct.

### 8. Reporting
Separate:
- observed result;
- interpretation;
- limitation;
- recommendation.

Do not claim causality from predictive association.

## Output format
1. Critical correctness issues
2. Data issues
3. Leakage/split issues
4. Code issues
5. Metric/evaluation issues
6. Reporting issues
7. Fix order

## Related skills
- `project-planner`
- `test-verifier`
- `code-reviewer`
