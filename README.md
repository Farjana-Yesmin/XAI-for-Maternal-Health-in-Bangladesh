# Explainable AI for Maternal Health Risk Prediction in Bangladesh

[![Python 3.8+](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![ICAIHE 2026](https://img.shields.io/badge/ICAIHE-2026%20Waseda-orange.svg)](https://www.researchsquare.com/article/rs-8584734/v1)

Official implementation of:

> Yesmin, F., Shirmin, N. & Bristy, S.S. (2026).
> *Explainable AI for Maternal Health Risk Prediction in Bangladesh:
> A Hybrid Fuzzy-XGBoost Framework with Clinician Validation.*
> Accepted, ICAIHE 2026, Waseda University, Tokyo.
> Preprint: [ResearchSquare rs-8584734/v1](https://www.researchsquare.com/article/rs-8584734/v1)

Part of the [FairHealth](https://github.com/Farjana-Yesmin/fairhealth) library —
`pip install fairhealth`

---

## The Problem

Bangladesh reports a maternal mortality ratio of 156 per 100,000 live births.
Black-box ML models limit clinical adoption in resource-constrained settings
because clinicians cannot understand or trust their reasoning.

**This work:** A hybrid Fuzzy-XGBoost framework combining ante-hoc fuzzy logic
with post-hoc SHAP/LIME explanations, validated by 14 healthcare professionals.

---

## Results

### Model Performance (test set, n=203)

| Metric | Value |
|---|---|
| Accuracy | **88.67%** |
| Precision | 0.8901 |
| Recall | 0.8867 |
| F1-Score | 0.8869 |
| ROC-AUC | **0.9703** |

Cross-validation: 0.8643 ± 0.0162 (robust, consistent with test performance).

### Comparison With Baselines

| Model | Accuracy | F1 |
|---|---|---|
| **Hybrid Fuzzy-XGBoost (ours)** | **88.67%** | **0.8869** |
| Gradient Boosting | 86.21% | 0.8619 |
| Random Forest | 85.22% | 0.8521 |
| Decision Tree | 81.28% | 0.8089 |
| MLP Neural Network | 79.80% | 0.7938 |
| SVM | 75.86% | 0.7572 |
| K-Nearest Neighbors | 72.91% | 0.7289 |

### SHAP Feature Importance

| Feature | SHAP Value |
|---|---|
| Healthcare Access Score | 1.49 (top predictor) |
| Blood Sugar | 0.53 |
| Fuzzy Risk Score | 0.39 |
| Systolic Blood Pressure | 0.29 |

Healthcare access (from DGHS 2024) dominates — maternal outcomes are shaped
by both biological risk and care infrastructure.

### Clinician Validation (N=14)

| Explanation Type | Preference |
|---|---|
| **Hybrid Fuzzy+SHAP (ours)** | **71.4%** |
| SHAP only | 21.4% |
| Score only | 7.1% |

54.8% would trust the system in clinical practice.
Top barrier: internet connectivity (50% of respondents).

### Fairness Analysis (8 Bangladesh Divisions)

- Accuracy σ = 0.0766 (low variation across regions)
- Better performance in underserved areas (r = -0.876 with healthcare access)
- Perfect accuracy (100%) in Sylhet, Rangpur, Barisal, Mymensingh

---

## Hybrid Architecture
Stage 1 — Ante-hoc (Fuzzy Logic)
Clinical parameters (Age, BP, Blood Sugar, HR)
↓
12 fuzzy rules from WHO 2016, ADA 2023, ACC/AHA 2017
↓
Fuzzy Risk Score (centroid defuzzification)
Stage 2 — ML (XGBoost)
6 clinical features + Healthcare Access Score + Fuzzy Risk Score
↓
XGBoost (400 estimators, max_depth=5, lr=0.05, L1/L2 regularization)
↓
Risk Level: Low / Medium / High
Stage 3 — Post-hoc Explanations
SHAP TreeExplainer → global feature importance
LIME → local instance-level explanation
**Sample fuzzy rules:**
IF Age=Optimal AND BP=Normal AND BS=Normal → Risk=Low
IF Age=High-risk OR BP=Stage2              → Risk=High
IF BS=Diabetic AND BP=Elevated             → Risk=High

---

## Data Sources

| Source | What It Provides |
|---|---|
| UCI Maternal Health Risk Dataset | 1,014 patient records (base clinical data) |
| DGHS Dashboard 2024 | Healthcare access scores, ANC rates by division |
| UNFPA MPDSR 2023 | Maternal mortality ratios by division |
| WHO 2016, ADA 2023, ACC/AHA 2017 | Clinical fuzzy rule thresholds |

Dataset on HuggingFace:
[fairhealth/bangladesh-maternal-health](https://huggingface.co/datasets/fairhealth/bangladesh-maternal-health)

---

## Quick Start

```bash
pip install xgboost shap lime scikit-fuzzy scikit-learn pandas numpy matplotlib
```

```python
# Run maternal_health.py
# Or use via FairHealth:
from fairhealth.explain.fuzzy import get_fired_rules

rules = get_fired_rules(age=42, sbp=145, bs=12.0, hr=88)
for r in rules:
    print(f"Rule {r['id']}: {r['condition']} → {r['outcome']}")
```

---

## Files in This Repository

| File | Description |
|---|---|
| `maternal_health.py` | Complete implementation |
| `final_fuzzy_xgboost_model.json` | Trained model weights |
| `final_corrected_results.csv` | Final evaluation results |
| `model_comparison_results.csv` | All 7 models compared |
| `results_summary.csv` | Summary statistics |

Clinician survey data available on request.

---

## Citation

```bibtex
@inproceedings{yesmin2026icaihe,
  author    = {Yesmin, Farjana and Shirmin, Nusrat and Bristy, Suraiya Shabnam},
  title     = {Explainable AI for Maternal Health Risk Prediction in Bangladesh:
               A Hybrid Fuzzy-XGBoost Framework with Clinician Validation},
  booktitle = {ICAIHE 2026, Waseda University, Tokyo},
  year      = {2026},
  note      = {Preprint: https://www.researchsquare.com/article/rs-8584734/v1}
}
```

---

**Authors:** Farjana Yesmin · Nusrat Shirmin · Suraiya Shabnam Bristy (Medical Officer,
Sonargaon Sheba General Hospital, Narayanganj)
· MIT License
