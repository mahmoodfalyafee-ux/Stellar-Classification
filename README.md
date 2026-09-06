# Stellar Classification ML

This repository contains a notebook and exported artifacts for a machine-learning
project that classifies Sloan Digital Sky Survey (SDSS17) observations as
galaxies, stars, or quasars.

## Contents

- `stellar_classification.ipynb` — analysis, preprocessing, model training, and evaluation
- `stellar_classification_report.pdf` — exported project report
- `model_result_*.png` — exported result figures

## Project overview

The study uses 100,000 observations with 18 original features and a moderately
imbalanced target distribution: 59.4% galaxies, 21.6% stars, and 19.0% quasars.
Nine administrative identifier columns are removed, leaving eight candidate
predictive features. Preprocessing includes percentile-based outlier capping,
removal of features with Pearson correlation above 0.95, standardization, and
an 80/20 stratified train/test split. The notebook evaluates Random Forest,
XGBoost, and LightGBM, including tuned configurations, using accuracy,
precision, recall, F1-score, and confusion matrices.

The tuned LightGBM configuration produced the best reported test accuracy:
**97.775%**, with class F1-scores of **0.98** for galaxies, **0.94** for
quasars, and **1.00** for stars. Quasars were the most difficult class and
were most often confused with galaxies; this result should not be interpreted
as production-grade astronomical inference without independent validation.

## Setup

The source dataset is not included in this repository. Obtain the SDSS17
dataset through an appropriate, trusted source and place it at the path
expected by the notebook, or update the notebook's data-loading path locally.
Run the notebook in an isolated Python environment with Jupyter, pandas,
NumPy, scikit-learn, XGBoost, LightGBM, and the plotting dependencies
installed. The notebook currently installs LightGBM at runtime; pin all
dependencies before reproducing the analysis.

## Reproducibility and safety

The reported metrics come from a single stratified holdout and cross-validation
experiments, so they are estimates for this dataset rather than guarantees of
generalization to new surveys or instruments. The source report also describes
binary reframing experiments and comparisons with public work; those details
are documented in the report and notebook rather than presented as a separate
production pipeline here.

See [`SECURITY-REVIEW.md`](SECURITY-REVIEW.md) for the dependency supply-chain
and reproducibility finding. Do not commit source datasets, credentials, local
paths, or notebook outputs containing sensitive records.
