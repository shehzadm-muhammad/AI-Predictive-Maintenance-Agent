# Methodology Summary

This file summarises the methodology used in the AI Predictive Maintenance Agent project.

The project followed an end-to-end machine learning workflow for predictive maintenance decision support. The goal was not only to classify records, but to produce practical maintenance recommendations using model scores, cost-aware thresholds, and explanation fields.

---

## 1. Dataset Understanding

The first stage involved reviewing the dataset structure, target variable, feature columns, and the type of maintenance decision the model needed to support.

The dataset represented anonymised heavy-duty vehicle diagnostic records. The target variable indicated whether a record belonged to the positive failure class or the negative non-failure class.

The dataset contained:

| Dataset | Purpose |
|---|---|
| Training data | Used for development, validation, model training, and threshold selection |
| Locked test data | Used once for final evaluation |
| Operational feed | Used for final maintenance-agent recommendations |

The operational feed was kept unlabelled and was not used for training, validation, threshold selection, or final test evaluation.

---

## 2. Data Quality and Missingness

The dataset contained missing sensor values across the training, test, and operational datasets.

The training dataset had 8.38% missing sensor cells, the locked test set had 10.45%, and the operational feed had 7.41%.

Some individual sensors had very high missingness. Because most rows contained at least one missing value, deleting incomplete rows would have removed most of the dataset. Therefore, imputation was required.

Median imputation was used because the features were numerical and anonymised. Missing-value indicators were also added so the models could learn whether missingness itself carried useful information.

---

## 3. Class Imbalance

The training set was strongly imbalanced.

It contained:

| Class | Count |
|---|---:|
| Negative | 7,867 |
| Positive failure | 133 |

The positive class represented only 1.66% of the training data.

Because of this, accuracy was not a reliable main metric. A model could achieve high accuracy by mostly predicting the negative class while still missing important positive failure cases.

The workflow therefore prioritised:

- recall
- PR-AUC
- false negatives
- operational cost
- practical maintenance impact

---

## 4. Data Splitting

The training data was split into development and validation sets using a stratified 80/20 split.

| Partition | Rows | Positive Cases | Negative Cases | Positive Percentage |
|---|---:|---:|---:|---:|
| Development training | 6,400 | 106 | 6,294 | 1.66% |
| Validation | 1,600 | 27 | 1,573 | 1.69% |
| Final test | 800 | 160 | 640 | 20.00% |
| Operational feed | 200 | N/A | N/A | N/A |

The final test set had a much higher positive-class rate than the development and validation partitions. This was treated as an evaluation limitation and possible distribution shift.

---

## 5. Preprocessing

The preprocessing strategy was designed to be reproducible and leakage-safe.

The main preprocessing steps were:

- separate features and target variable
- encode the target class
- check feature alignment across datasets
- apply median imputation
- add missing-value indicators
- apply scaling for the MLP model only
- keep all transformations inside scikit-learn pipelines

Using pipelines helped prevent data leakage because preprocessing was fitted only on the relevant training data and then applied to validation, test, and operational records.

---

## 6. Model Development

Three machine learning models were trained and compared:

| Model | Reason for Inclusion |
|---|---|
| Extra Trees Classifier | Strong tree ensemble for high-dimensional tabular data |
| Multi-Layer Perceptron | Neural network baseline for non-linear relationships |
| Gradient Boosting Classifier | Sequential ensemble model for structured tabular data |

Hyperparameter tuning was carried out using the development training set. The optimisation metric was average precision / PR-AUC because the positive class was rare.

---

## 7. Validation Benchmarking

The tuned models were first evaluated on the validation set using the default threshold of 0.50.

The default threshold gave high accuracy, but recall was not good enough for the rare failure class. For example, Extra Trees achieved high validation accuracy at threshold 0.50, but missed 14 of the 27 validation failures.

Because missed failures were much more costly than unnecessary inspections, threshold tuning was needed.

---

## 8. Cost-Aware Threshold Selection

The project used asymmetric operational costs:

| Error Type | Cost |
|---|---:|
| False positive / unnecessary inspection | 10 |
| False negative / missed failure | 500 |

The operational cost formula was:

```text
Operational cost = (False Positives × 10) + (False Negatives × 500)