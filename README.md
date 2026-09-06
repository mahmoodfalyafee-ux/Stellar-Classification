# Stellar Classification ML

This repository contains a notebook and exported artifacts for a machine-learning
stellar classification project.

## Contents

- `stellar_classification.ipynb` — analysis, preprocessing, model training, and evaluation
- `stellar_classification_report.pdf` — exported project report
- `model_result_*.png` — exported result figures

## Reproducibility and safety

Run the notebook in an isolated environment with dependencies pinned before
reproducing the analysis. The notebook currently installs LightGBM at runtime;
see [`SECURITY-REVIEW.md`](SECURITY-REVIEW.md) for the associated supply-chain
and reproducibility risk. Do not commit source datasets, credentials, local
paths, or notebook outputs containing sensitive records.
