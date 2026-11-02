# SVM Experiment Log

Key findings for the risk-theme classifier. The experiments were run in an earlier, experiment-only version of `notebooks/svm_review_classifier.ipynb`. The current notebook contains only the final model.

## Setup

- **Data:** `notebooks/annotated_training_test_set_600_samples.csv`.
  - 600 reviews with unique UIDs; review text matches the MHARD source.
  - Labels were audited against the codebook.
  - Positive labels: dependence 37, attachment 34, isolation/displacement 52, crisis-response frustration 53, other/none 427.
- **Input:** review text only.
- **Evaluation:** 12 separate evaluation sets of 50 reviews, so every review is scored exactly once by a model that never saw it.
  - For each set, the model is tuned and trained on the other 550 reviews.
  - Results are totalled over all 600 reviews, which contain 176 risk labels.
  - Single small test sets were too noisy to compare models: on 50-review sets, the same model's macro-F1 ranged from 0.48 to 0.66.
- **Metrics:**
  - Risk labels caught, out of 176.
  - False risk flags: risk labels predicted on reviews that don't have them.
  - Risk precision: the share of risk flags that are correct.
  - Macro-F1 across all five labels.
  - Exact match: all five labels right. Always predicting other/none scores 71.2%.
- **Tuning:** settings are chosen by 5-fold cross-validation (seeds 0, 1, 2) on the training reviews only, with the cleanup rule applied during tuning. The rule removes other/none when a risk theme is predicted and assigns other/none when nothing is predicted.

## Finding 1: Embeddings vs. No Embeddings

Embedding SVM: sentence embeddings (`all-MiniLM-L6-v2`) with a linear SVM. TF-IDF SVM: word-frequency (TF-IDF) features with a linear SVM, no embeddings.

| Model | Risk caught | False flags | Precision | Macro-F1 | Exact match |
|---|---|---|---|---|---|
| TF-IDF SVM only (no embeddings) | 91/176 | 129 | 0.41 | 0.521 | 69.0% |
| Embedding SVM only | 100/176 | 142 | 0.41 | 0.547 | 68.5% |
| **Both SVMs blended (final)** | **108/176** | **124** | **0.47** | **0.578** | **72.0%** |

F1 for dependence / attachment / isolation / crisis / other:

| Model | Dependence | Attachment | Isolation | Crisis | Other |
|---|---|---|---|---|---|
| TF-IDF SVM | 0.28 | 0.51 | 0.43 | 0.56 | 0.83 |
| Embedding SVM | 0.30 | 0.54 | 0.47 | 0.61 | 0.81 |
| Blend | 0.26 | 0.56 | 0.53 | 0.69 | 0.85 |

- Embeddings beat TF-IDF on its own: the embedding SVM catches 9 more risk labels and scores higher macro-F1.
- Blending the two is best on every summary measure. It catches the most risk with the fewest false flags, and it is the only setup above the always-other/none exact-match baseline.

## Finding 2: 300 vs. 600 Training Reviews

The earlier 300-row experiment kept every risk-labeled review plus half as many other/none reviews, then split that subset for testing. It scored higher than 600 rows, but that mixed two effects: a different training set, and an easier test set with fewer reviews that could be falsely flagged. Here the two effects are tested separately on the same evaluation sets:

- **Training:** all reviews, or a 300-row-style half that keeps all risk reviews.
- **Evaluation:** all reviews, or a 300-row-style half in which 127 of 300 are other/none.

| Training | Evaluation | Risk caught | False flags | Precision | Macro-F1 |
|---|---|---|---|---|---|
| 600-row (all) | full | 108/176 | 124 | 0.47 | 0.578 |
| 600-row (all) | 300-row-style | 108/176 | 62 | 0.64 | 0.627 |
| 300-row-style | full | 116/176 | 187 | 0.38 | 0.546 |
| 300-row-style | 300-row-style | 116/176 | 87 | 0.57 | 0.622 |

- **The 300-row gain came from the test set, not the model.** The same 600-row model rises from 0.578 to 0.627 macro-F1 when scored on a 300-row-style test set, only because that test set has fewer other/none reviews to falsely flag.
- **Training on fewer other/none reviews makes the model flag more.** It catches 8 more risk labels but raises 63 more false flags, and its macro-F1 is lower on both test sets.
- **Conclusion:** train on all 600 reviews.

## Finding 3: Naive Bayes

Naive Bayes here is ComplementNB on TF-IDF word unigrams and bigrams plus scaled sentence embeddings. This is the stronger variant from `NaiveBayesModel.ipynb`. When cross-validation could choose freely, it gave Naive Bayes a weight of 0 in the blend. For the third row, its weight was required to be at least 0.25.

| Model | Risk caught | False flags | Precision | Macro-F1 | Exact match |
|---|---|---|---|---|---|
| Naive Bayes only | 70/176 | 120 | 0.37 | 0.432 | 66.0% |
| **Two SVMs (final)** | **108/176** | 124 | 0.47 | **0.578** | **72.0%** |
| Two SVMs + Naive Bayes (weight ≥ 0.25) | 97/176 | 109 | 0.47 | 0.555 | 71.2% |

- On its own, Naive Bayes is much weaker than the SVMs, especially on the rarest themes (F1 for dependence 0.10, isolation 0.31).
- Adding it to the SVM blend makes the model more cautious. It removes 15 false flags but misses 11 risk labels, with no gain in precision and lower macro-F1.
- **Conclusion:** leave Naive Bayes out.

## Final Model

- **Model:** the embedding SVM and the TF-IDF SVM blended 50/50, a shared cutoff of −0.1, then the cleanup rule.
- **Training:** tuned and trained on all 600 reviews. Settings chosen by cross-validation: C = 0.3 for both SVMs (CV macro-F1 0.584).
- **Saved file:** `models/two_svm_ensemble.joblib`. To predict, run notebook sections 1, 2 and 4, which use `TwoSVMEnsemble.load(...)` and `label_reviews(...)`.
- **Known weaknesses:**
  - About half of the risk flags are false alarms.
  - Dependence is the weakest theme (F1 about 0.26).
