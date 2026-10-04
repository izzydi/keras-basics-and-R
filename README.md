# Autoencoder Representation Learning with Keras in R

An R-based deep-learning project that uses a **Keras/TensorFlow autoencoder** to learn a compact representation of high-dimensional wave-function data, then trains an XGBoost classifier on the learned embedding.

## Project overview

The workflow combines reproducible preprocessing, neural-network representation learning and supervised classification. A dense autoencoder compresses 112 numeric predictors into a six-dimensional embedding, which becomes the feature space for downstream classification.

## Repository contents

- [`keras_autoencoder_pipeline.Rmd`](keras_autoencoder_pipeline.Rmd) — audited R Markdown workflow.
- [`data/README.md`](data/README.md) — expected dataset layout and filenames.
- [`R-packages.txt`](R-packages.txt) — direct R package dependencies.
- [`.gitignore`](.gitignore) — local R/TensorFlow and raw-data exclusions.

## Validation design

The pipeline creates a stratified held-out test set **before** learned preprocessing. The preprocessing recipe and autoencoder are fitted using training data only. The autoencoder uses 20% of the training partition for early stopping, and its best weights are restored before embeddings are extracted.

XGBoost cross-validation tunes the classifier on the fixed representation learned from the training partition. Because representation learning is not repeated inside every classifier fold, the cross-validation estimate is used for tuning rather than as the final performance claim. The untouched held-out test set is the primary evaluation set.

Optional external validation data are transformed using the already-fitted preprocessing recipe, autoencoder and classifier; the workflow does not refit on validation data.

## Methods and tools

The analysis uses `keras`/`tensorflow` for representation learning, `tidymodels` and `finetune` for resampling and tuning, XGBoost for classification, `data.table` for efficient loading and `caret` for confusion-matrix reporting.

## Data requirements

The raw datasets are not stored in this repository. Place them under the `data/` structure described in [`data/README.md`](data/README.md). The external validation file is optional; the main train/test workflow runs without it.

## Scope

This project demonstrates representation learning with explicit train/test boundaries. It is a data-science portfolio project rather than a production inference service.
