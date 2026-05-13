# AI Predictive Maintenance Agent

This repository contains a portfolio summary of my Level 6 Artificial Intelligence practical coursework.

The project focused on building a machine learning decision-support workflow for predictive maintenance. The system uses data exploration, preprocessing, model benchmarking, validation-based champion model selection, cost-aware thresholding, and an AI maintenance agent output file to recommend maintenance actions for operational records.

> This project was completed for educational purposes as part of my BSc Computer Science degree.

---

## Project Overview

The aim of this project was to apply artificial intelligence and machine learning techniques to a predictive maintenance-style problem.

The task was based on an anonymised heavy-duty vehicle diagnostic dataset. The goal was to identify rare positive failure cases linked to a safety-critical subsystem and convert model outputs into practical maintenance recommendations.

The project focused on:

- understanding the dataset and data quality issues
- handling missing sensor values
- dealing with severe class imbalance
- training and comparing machine learning models
- selecting a champion model using validation-only evidence
- applying cost-aware threshold selection
- generating risk bands
- producing an AI maintenance agent output file
- explaining recommendations using decision rationale fields

The final output was a maintenance decision CSV containing model scores, recommended actions, risk bands, expected costs, selected thresholds, and explanation text.

---

## Dataset Summary

Three datasets were used in the workflow.

| Dataset | Rows | Sensor Features | Overall Missingness | Notes |
|---|---:|---:|---:|---|
| Training | 8,000 | 170 | 8.38% | Labelled data used for development and validation |
| Test | 800 | 170 | 10.45% | Locked labelled test set used once for final evaluation |
| Operational feed | 200 | 170 | 7.41% | Unlabelled records used for final agent recommendations |

The training data was strongly imbalanced. It contained 7,867 negative records and only 133 positive failure cases. Because of this, accuracy alone was not suitable for model selection. Recall, PR-AUC, false negatives, and operational cost were more important.

---

## Main Features

- End-to-end machine learning workflow
- Data quality and missingness analysis
- Handling of severe class imbalance
- Median imputation and missing-value indicators
- Model training and benchmarking
- Cost-aware threshold selection
- Validation-only champion model selection
- Locked final test evaluation
- AI maintenance agent output CSV generation
- Explainable recommendation fields
- Practical decision-support framing

---

## Technologies Used

| Area | Technology |
|---|---|
| Programming language | Python |
| Data handling | pandas, NumPy |
| Machine learning | scikit-learn |
| Development environment | Jupyter Notebook |
| Output format | CSV |
| Evaluation | Classification metrics, PR-AUC, ROC-AUC, confusion matrix, cost-aware logic |

---

## Repository Structure

```text
AI-Predictive-Maintenance-Agent/
├── README.md
├── .gitignore
├── notebooks/
│   └── maintenance-agent-pipeline.ipynb
├── outputs/
│   ├── maintenance-agent-decisions.csv
│   ├── eda-summary.csv
│   ├── split-summary.csv
│   ├── validation-benchmarking-all-models.csv
│   ├── validation-cost-aware-comparison.csv
│   ├── final-test-champion-comparison.csv
│   ├── final-test-all-models-comparison.csv
│   ├── agent-action-distribution.csv
│   └── RESULTS_INDEX.md
├── docs/
│   ├── README_SCREENSHOTS_AND_RESULTS_SNIPPET.md
│   └── screenshots/
│       ├── 01-training-class-distribution.png
│       ├── 02-top15-missing-sensors.png
│       ├── 03-overall-missingness-by-dataset.png
│       └── SCREENSHOT_INDEX.md
└── notes/
    └── methodology-summary.md