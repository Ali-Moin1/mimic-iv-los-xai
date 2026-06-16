# MIMIC-IV ICU Long-Stay Prediction with Explainable AI

This project uses the MIMIC-IV Clinical Database Demo to build a small explainable machine learning pipeline for predicting whether an ICU stay is likely to last more than 3 days.

The aim is not to build a clinical tool. The aim is to show how healthcare data can be cleaned, prepared, modelled, evaluated, and explained in a transparent way.

## Why I Built This

In healthcare, a prediction is not useful if people cannot understand it. A model may give a risk score, but doctors, nurses, managers, or clinical teams still need to know what influenced that prediction.

This project focuses on both:

* model performance
* model explainability

The idea is to explore how AI could support planning and decision-making without replacing human judgement.

## Important Note

This project uses the MIMIC-IV Clinical Database Demo, which is a small demo version of the full MIMIC-IV dataset.

Because of the small dataset size, the results are not clinically valid and should not be used for real-world medical decisions. This is a portfolio and learning project, not a deployable clinical prediction system.

## Dataset

Dataset used:

* MIMIC-IV Clinical Database Demo 2.2

Main tables used:

* `patients`
* `admissions`
* `icustays`
* `d_items`
* `chartevents`

Approximate table sizes used in the notebook:

* 100 patients
* 275 admissions
* 140 ICU stays
* 4,014 item definitions
* 668,862 charted events

## Prediction Task

The target variable is `longicustay`.

It is created from ICU length of stay (`los`):

* `1` = ICU stay longer than 3 days
* `0` = ICU stay of 3 days or less

This makes the task a binary classification problem.

## Features Used

The project combines ICU stay information with patient and admission data.

It also extracts early vital-sign data from the first 24 hours of ICU care, including:

* heart rate
* systolic blood pressure
* diastolic blood pressure
* mean blood pressure
* respiratory rate
* temperature
* oxygen saturation

For each vital sign, simple summary features are created, such as:

* minimum value
* mean value
* maximum value

These features are then combined with demographic, admission, and ICU stay information for modelling.

## Model Used

The project uses a Random Forest classifier as a baseline model.

I used Random Forest because:

* it works well with structured/tabular data
* it can handle mixed clinical features
* it gives useful feature importance outputs
* it works well with SHAP for explainability

## Evaluation

The notebook includes:

* target distribution
* ICU length-of-stay distribution
* confusion matrix
* ROC curve
* feature importance plot
* correlation heatmap

Accuracy alone is not enough for this type of problem, so the model is also reviewed using classification metrics and explainability outputs.

## Explainability

SHAP is used to explain the model predictions.

The project looks at:

* global feature importance
* how features influence the model overall
* individual prediction explanations
* which factors push a prediction towards a longer or shorter ICU stay

This is important because healthcare AI should not behave like a black box.

## Human-AI Decision-Making Angle

This project links to human-AI decision-making because ICU length-of-stay prediction is not only a technical problem.

In a real setting, this type of prediction could affect:

* bed planning
* workload planning
* escalation discussions
* communication between clinical teams
* trust in AI-supported systems

The model should therefore support human judgement, not replace it.

The project focuses on explainability, transparency, and responsible use of AI in high-stakes environments.

## Limitations

This project has several limitations:

* the dataset is a small demo dataset
* the model is not clinically validated
* the results are not generalisable
* the feature engineering is basic
* no external validation has been done
* no healthcare professionals have evaluated the outputs

Future work could include:

* using the full MIMIC-IV dataset
* testing more models
* improving clinical feature engineering
* adding uncertainty estimates
* building a dashboard for human review
* evaluating explanations with healthcare professionals

## Tools Used

* Python
* pandas
* NumPy
* scikit-learn
* matplotlib
* seaborn
* SHAP
* Jupyter Notebook

## Project Status

This is a proof of concept project for explainable healthcare AI.

The main focus is not just prediction accuracy, but showing how AI predictions can be made easier to understand for human decision-making.
