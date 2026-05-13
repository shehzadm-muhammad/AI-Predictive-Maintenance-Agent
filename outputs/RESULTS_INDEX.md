# Results Index

This folder contains cleaned summary CSV files generated from the AI Predictive Maintenance Agent workflow.

The files in this folder are summary outputs only. Raw datasets, coursework submission files, student identifiers, and private university documents are not included.

---

## Files

| File | Purpose |
|---|---|
| `maintenance-agent-decisions.csv` | Final AI maintenance agent recommendations for the operational feed |
| `eda-summary.csv` | Dataset size and missingness summary |
| `split-summary.csv` | Development, validation, final test, and operational feed split summary |
| `validation-benchmarking-all-models.csv` | Validation benchmarking results for all tuned models using default and cost-aware thresholds |
| `validation-cost-aware-comparison.csv` | Cost-aware validation comparison used for champion model selection |
| `final-test-champion-comparison.csv` | Final test comparison for the selected Extra Trees champion at default vs cost-aware threshold |
| `final-test-all-models-comparison.csv` | Final test comparison of all tuned models using validation-selected thresholds |
| `agent-action-distribution.csv` | Distribution of final maintenance recommendations on the operational feed |

---

## Main Result Summary

Extra Trees was selected as the official champion model using validation-only evidence.

| Model | Selection Basis | Selected Threshold | Validation Cost |
|---|---|---:|---:|
| Extra Trees | Official champion | 0.07 | 910 |

On the locked final test set, the Extra Trees cost-aware threshold improved recall and reduced operational cost compared with the default threshold.

| Threshold Type | Threshold | Recall | F1 | Operational Cost |
|---|---:|---:|---:|---:|
| Default | 0.50 | 0.5500 | 0.7040 | 36,020 |
| Validation-selected cost-aware | 0.07 | 0.9250 | 0.8997 | 6,210 |

---

## Operational Agent Summary

The final AI maintenance agent produced recommendations for 200 operational records.

| Action | Count |
|---|---:|
| A0: Continue monitoring | 174 |
| A1: Schedule inspection | 13 |
| A2: Immediate intervention / safety escalation | 13 |

The output is intended as a decision-support prototype, not a production maintenance system.