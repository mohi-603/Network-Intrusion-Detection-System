# Network Intrusion Detection System

## Overview

A machine learning project that detects malicious network traffic using the UNSW-NB15 dataset. The project applies classification algorithms to distinguish between normal network traffic and potential cyberattacks.

## Objective

Build and evaluate machine learning models for binary network intrusion detection.

- `0` — Normal Traffic
- `1` — Malicious Traffic (Attack)

## Dataset

**UNSW-NB15 Dataset**

The dataset contains network traffic records with 42 selected input features after removing the identifier and attack-category columns.

Files used:
- `UNSW_NB15_training-set.csv`
- `UNSW_NB15_testing-set.csv`

Dataset source: [UNSW-NB15 – UNSW Canberra](https://research.unsw.edu.au/projects/unsw-nb15-dataset)

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Joblib
- JupyterLab

## Methodology

1. Dataset loading and exploration.
2. Data quality and duplicate checks.
3. Feature and target selection.
4. Categorical encoding using One-Hot Encoding.
5. Numerical feature scaling using StandardScaler.
6. Missing-value handling using SimpleImputer.
7. Baseline model development.
8. Logistic Regression and Random Forest training.
9. Three-fold stratified cross-validation.
10. Model evaluation and visualization.
11. Model serialization using Joblib.

Preprocessing was implemented using Scikit-learn pipelines to prevent preprocessing leakage. The official test dataset was kept separate from model training and cross-validation.

The `id` and `attack_cat` columns were excluded from model inputs. The latter directly reveals the target class.

## Model Performance

### Official Test Dataset

| Metric | Baseline | Logistic Regression | Random Forest |
|---|---:|---:|---:|
| Accuracy | 55.06% | 81.00% | **87.05%** |
| Precision | 55.06% | 75.37% | **81.66%** |
| Recall | 100.00% | 97.28% | **98.62%** |
| F1-score | 71.02% | 84.93% | **89.34%** |
| ROC-AUC | — | 95.58% | **97.89%** |

### Random Forest Cross-Validation

Three-fold stratified cross-validation on the training dataset:

| Metric | Mean Score |
|---|---:|
| Accuracy | 95.79% |
| Precision | 96.09% |
| Recall | 97.81% |
| F1-score | 96.94% |
| ROC-AUC | 99.33% |

Cross-validation results are higher than official test results. This difference highlights the importance of evaluating generalization on a separate test dataset.

## Confusion Matrix

Random Forest test results:

- True Negatives: 26,960
- False Positives: 10,040
- False Negatives: 626
- True Positives: 44,706

The model detects most malicious traffic but still produces false alarms and misses some attacks.

## Feature Importance

The five most important features identified by Random Forest:

1. `sttl`
2. `ct_state_ttl`
3. `rate`
4. `dload`
5. `sload`

These features represent important characteristics of network traffic and connection behavior.

## Project Structure

```text
Network-Intrusion-Detection/
│
├── data/
│   ├── UNSW_NB15_training-set.csv
│   └── UNSW_NB15_testing-set.csv
│
├── models/
│   └── random_forest_intrusion_detector.pkl
│
├── Network_Intrusion_Detection.ipynb
│
└── README.md
```

## Limitations

- Model performance depends on the quality and characteristics of the UNSW-NB15 dataset.
- Training and testing datasets have different class and attack-category distributions.
- False positives may generate excessive security alerts.
- Some malicious traffic is still missed.
- The default classification threshold is 0.5.
- Cross-validation performance does not guarantee equivalent real-world performance.
- Feature importance does not establish causal relationships.

## Future Improvements

- Experiment with Gradient Boosting and other classification algorithms.
- Investigate the cross-validation and test-performance gap.
- Evaluate different classification thresholds using training-only validation.
- Apply explainability techniques such as SHAP.
- Test on additional network intrusion datasets.
- Explore real-time network traffic detection.

## Author

**Muhammad Mohsin Khan**

BS Software Engineering Student  
City University of Science and Information Technology, Peshawar

