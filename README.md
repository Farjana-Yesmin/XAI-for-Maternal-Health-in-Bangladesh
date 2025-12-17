# XAI for Maternal Health Risk Prediction in Bangladesh

[![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)
[![Paper Status](https://img.shields.io/badge/Paper-Under%20Review-orange)](LINK_TO_PREPRINT_IF_ANY)

**Repository for the paper:** *"Explainable AI for Maternal Health Risk Prediction in Bangladesh: A Hybrid Fuzzy-XGBoost Framework with Clinician Validation"*

> **A hybrid AI framework designed to provide transparent risk predictions for maternal health in resource-constrained settings, combining interpretable fuzzy logic with powerful machine learning.**

## 📋 Overview

This repository contains the implementation for a research project addressing a critical challenge in global health: **making AI-assisted maternal health risk assessment trustworthy and actionable for clinicians in Bangladesh**.

In many low-resource settings, complex "black-box" AI models are met with skepticism. Our work bridges this gap by developing a **novel hybrid framework** that integrates an interpretable, rule-based Fuzzy Inference System (reflecting clinical guidelines) with a high-performance XGBoost classifier. This approach aims to deliver both strong predictive performance and clear, intuitive explanations for its predictions, facilitating potential clinical adoption.

## 🏗️ Methodology at a Glance

The core innovation is a two-stage model:
1.  **Ante-hoc Interpretability**: A fuzzy logic system translates clinical parameters (like blood pressure and age) into a human-readable "fuzzy risk score" based on established medical knowledge.
2.  **Hybrid Prediction**: This fuzzy score, along with the original clinical features and contextual data, is used to train an XGBoost model. For final predictions, we employ **post-hoc explanation tools** (SHAP, LIME) to provide detailed, case-specific reasoning.

**Key Features of the Framework:**
*   **Explainability-by-Design**: Combines intuitive rules with model-agnostic explanations.
*   **Context-Awareness**: Incorporates regional healthcare access data to address disparities.
*   **Clinician-Centered**: Designed and validated with feedback from healthcare professionals in Bangladesh.

## 📁 Repository Structure


## 📁 Repository Structure
.
├── maternal_health.py # Main Python module with model implementation
├── requirements.txt # Python dependencies
├── data/ # Data processing utilities
├── notebooks/ # Jupyter notebooks for EDA and prototyping
└── README.md # This file

## 🚀 Getting Started

### Prerequisites
*   Python 3.8+
*   pip

### Installation

1.  Clone the repository:
    ```bash
    git clone https://github.com/Farjana-Yesmin/XAI-for-Maternal-Health-in-Bangladesh.git
    cd XAI-for-Maternal-Health-in-Bangladesh
    ```

2.  Install required packages:
    ```bash
    pip install -r requirements.txt
    ```

### Basic Usage

The main module `maternal_health.py` provides a class to train and use the hybrid model.

```python
import maternal_health as mh
import pandas as pd

# Load your data
# data = pd.read_csv('path_to_your_data.csv')

# Initialize and train the model
# hybrid_model = mh.HybridFuzzyXGBoost()
# hybrid_model.train(training_data)

# Get a prediction with an explanation for a new case
# prediction, explanation = hybrid_model.predict_explain(new_patient_data)


or detailed examples on data preparation and advanced usage, please refer to the example notebooks in the notebooks/ directory.

📄 Associated Publication

The methodology and findings of this project are detailed in a companion paper:

Farjana Yesmin, Suriya Shabnam Bristy. "Explainable AI for Maternal Health Risk Prediction in Bangladesh: A Hybrid Fuzzy-XGBoost Framework with Clinician Validation."
Currently under review.
A preprint will be made available upon submission. Please cite this paper if you use the code or ideas from this repository.

🤝 Contributing & Issues

We welcome questions and discussions about the code! Please use the GitHub Issues page for:

Reporting bugs in the implementation.
Asking clarifying questions about the code.
Suggesting minor improvements.
Please note that as the associated paper is under review, detailed discussions of the methodology and results should be directed to the authors privately.

📜 License

This project's code is released under the MIT License.

🙏 Acknowledgments

We extend our sincere gratitude to the healthcare professionals in Bangladesh who provided valuable feedback during the development of this framework. This work also acknowledges the use of publicly available health data from the Bangladesh Directorate General of Health Services (DGHS).

