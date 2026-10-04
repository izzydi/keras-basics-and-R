# Autoencoder Representation Learning with Keras in R

An R-based deep-learning project that uses a **Keras/TensorFlow autoencoder** to learn a compact representation of high-dimensional wave-function data, then trains an XGBoost classifier on the learned embedding.

## Project overview

The workflow combines reproducible preprocessing, neural-network representation learning and supervised classification. A dense autoencoder compresses 112 numeric predictors into a six-dimensional embedding, which is then used as the feature space for model tuning and evaluation.

## Repository contents

- [`keras_basics.Rmd`](keras_basics.Rmd) — complete R Markdown workflow.
- [`data/README.md`](data/README.md) — expected dataset layout and filenames.

## Methods and tools

The analysis uses:

- `keras` and `tensorflow` for representation learning,
- `tidymodels` and `finetune` for preprocessing, resampling and tuning,
- `xgboost` through tidymodels for classification,
- `data.table` for efficient data loading,
- `tidyverse` for data manipulation,
- `caret` for confusion-matrix reporting.

The pipeline includes:

1. stratified train/test splitting,
2. training-only Yeo-Johnson transformation, normalization and range scaling,
3. dense autoencoder training with early stopping,
4. extraction of a six-dimensional neural embedding,
5. repeated cross-validation on the embedding dataset,
6. XGBoost hyperparameter tuning,
7. held-out test evaluation,
8. external validation without re-fitting on validation data.

## Reproducibility and validation

The source now uses project-relative data paths rather than machine-specific Windows paths. Preprocessing is fitted on the training data and reused unchanged for test and external-validation data. Cross-validation is performed on the learned embedding used by the downstream classifier, and the external validation set is evaluated with the already-trained model to avoid data leakage.

## Data requirements

The raw datasets are not stored in the repository. Place them under the `data/` structure described in [`data/README.md`](data/README.md).

## Running the analysis

1. Install R and the R interface to TensorFlow/Keras.
2. Install the packages loaded at the top of `keras_basics.Rmd`.
3. Add the required data files under `data/`.
4. Open the repository in RStudio and knit or run `keras_basics.Rmd` from top to bottom.

## Scope

This project demonstrates representation learning, careful train/test separation and integration of deep features with a conventional supervised-learning pipeline. It is maintained as a data-science portfolio project rather than a production inference service.
