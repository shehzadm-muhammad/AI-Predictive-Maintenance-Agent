# Screenshot Index

This folder contains selected EDA screenshots from the AI Predictive Maintenance Agent project.

The screenshots show the main data-quality and modelling issues identified before model development.

---

## Screenshots

| File | Purpose |
|---|---|
| `01-training-class-distribution.png` | Shows the severe imbalance between negative and positive failure records in the training data |
| `02-top15-missing-sensors.png` | Shows the 15 training sensors with the highest missing-value percentages |
| `03-overall-missingness-by-dataset.png` | Compares overall missing sensor values across the training, test, and operational datasets |

---

## Why These Matter

The class distribution screenshot explains why accuracy was not enough for this problem. The positive failure class was rare, so recall, PR-AUC, and false negatives were more important.

The missingness screenshots explain why missing-value handling was required. Median imputation and missing-value indicators were used in the machine learning pipelines.