# MIMIC-IV ICU Long-Stay Prediction with Explainable AI

## Project Overview

This project builds an explainable machine learning pipeline using the MIMIC-IV Clinical Database Demo to predict whether an ICU stay will be longer than 3 days. The model uses demographic, admission, ICU stay, and early vital-sign features derived from the first 24 hours of care.

The workflow combines structured EHR preprocessing, Random Forest modelling, performance evaluation, and SHAP-based interpretation to support transparent healthcare AI rather than black-box prediction alone.

## Important Note

This project uses the MIMIC-IV Clinical Database Demo, which is a small demonstration subset intended for research prototyping and learning the database schema. The results should not be interpreted as clinically valid or generalisable. The purpose of this project is to demonstrate an explainable AI workflow, not to build a deployable clinical prediction system.

## Project Objective

The main goal is to explore how early predictive modelling could support ICU resource planning and clinical decision-making in principle, while highlighting the need for validation before real-world deployment.

The notebook frames explainability as a core requirement, emphasizing transparency, trust, and reduced cognitive burden alongside predictive performance.

## Dataset

The project uses the MIMIC-IV Clinical Database Demo 2.2, a small demonstration subset of MIMIC-IV suitable for prototyping and learning the schema before scaling to the full dataset.

The core source tables used are:

- patients
- admissions
- icustays
- d_items
- chartevents

Reported table sizes:

- 100 patients
- 275 admissions
- 140 ICU stays
- 4,014 item definitions
- 668,862 charted events

## Prediction Task

The target variable is `longicustay`, defined from ICU length of stay (`los`) as a binary label:

- `1` = ICU stay longer than 3 days
- `0` = ICU stay of 3 days or shorter

This makes the project a binary classification problem focused on operationally meaningful ICU duration risk.

## Feature Engineering

The pipeline merges ICU stays with patient-level and admission-level information using `subject_id` and `hadm_id`.

The notebook converts timestamp fields into datetime format before modelling.

It selects common ICU vital-sign item IDs for:

- heart rate
- systolic blood pressure
- diastolic blood pressure
- mean blood pressure
- respiratory rate
- temperature
- oxygen saturation

To represent early physiological status, the notebook keeps measurements from the first 24 hours of ICU stay and aggregates them into summary statistics such as minimum, mean, and maximum values for each vital sign.

The final modelling table combines derived vital-sign features with care unit, demographic, admission, and target-label information.

## Modelling Approach

The project uses scikit-learn for preprocessing, train/test splitting, imputation, model training, and evaluation.

A `RandomForestClassifier` is used as the baseline model for ICU long-stay prediction.

This model was selected because tree-based models can handle mixed clinical features and work naturally with SHAP explanations for both global and local interpretation.

## Evaluation and Visualisation

The notebook includes:

- target distribution plot
- ICU length-of-stay distribution
- confusion matrix
- ROC analysis
- feature-importance visualisation
- correlation heatmap for vital features

These visuals help describe cohort structure and baseline model behaviour, but they do not fully explain individual predictions without an explainability method such as SHAP.

## Explainability with SHAP

SHAP is used to interpret the trained Random Forest model at both global and individual-patient levels.

The SHAP explanations are intended to show how age, admission factors, care unit, and early vital signs push predictions toward longer or shorter ICU stays.

This supports transparent, clinician-facing AI principles rather than relying only on model performance metrics.

## Relevance to Human-AI Decision-Making

This project is relevant to human-AI decision-making because ICU length-of-stay prediction is not only a technical classification task. In practice, prediction outputs may influence workload planning, bed management, escalation decisions, and communication between clinical teams.

For this reason, the model must be interpretable, uncertainty-aware, and presented in a way that supports rather than replaces professional judgement.

The project therefore focuses on SHAP-based explanations and plain-language interpretation of model outputs, linking predictive performance with issues of trust, cognitive burden, and responsible use of AI in high-stakes healthcare environments.

## Limitations

This project is limited by the small size of the MIMIC-IV demo dataset. The results are not clinically generalisable and should not be used for real clinical decision-making.

Further work would require:

- validation on the full MIMIC-IV dataset
- stronger clinical feature engineering
- comparison with additional models
- external validation
- user-centred evaluation with healthcare professionals

## Tools and Libraries

- Python
- pandas
- NumPy
- scikit-learn
- matplotlib
- seaborn
- SHAP
- Jupyter Notebook

## Project Status

This project is a proof-of-concept portfolio project demonstrating explainable AI for healthcare decision support.
