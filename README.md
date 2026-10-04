# Autoencoder Representation Learning with Keras in R

An R-based deep-learning project that uses a **Keras/TensorFlow autoencoder** to learn a compact representation of high-dimensional wave-function data, then trains an XGBoost classifier on the learned embedding.

## Project overview

The workflow combines reproducible preprocessing, neural-network representation learning and supervised classification. A dense autoencoder compresses 112 numeric predictors into a six-dimensional embedding, which is then used as the feature space for model tuning and evaluation.

## Repository contents

- [`keras_autoencoder_pipeline.Rmd`](keras_autoencoder_pipeline.Rmd) — complete R Markdown workflow.
- [`data/README.md`](data/README.md) — expected dataset layout and filenames.
- [`.gitignore`](.gitignore) — local R/TensorFlow and raw-data exclusions.

## Methods and tools

The analysis uses:

- `keras` and `tensorflow` for representation learning,
- `tidymodels` and `finetune` for preprocessing, resampling and tuning,
- `xgboost` through tidymodels for classification,
- `data.table` for efficient data loading,
- `tidyverse` for data manipulation,
- `caret` for confusion-matrix reporting.

The pipeline includes stratified train/test splitting, training-only preprocessing, autoencoder training with early stopping, six-dimensional embedding extraction, repeated cross-validation, XGBoost tuning, held-out test evaluation and external validation.

## Reproducibility and validation

The source uses project-relative paths instead of machine-specific Windows paths. Preprocessing is fitted on training data and reused for held-out and external-validation data, and the external validation set is evaluated with the already-trained classifier rather than refitting on validation data.

## Data requirements

The raw datasets are not stored in the repository. Place them under the `data/` structure described in [`data/README.md`](data/README.md).

## Scope

This project demonstrates representation learning, careful train/test separation and integration of deep features with a conventional supervised-learning pipeline. It is maintained as a data-science portfolio project rather than a production inference service.
