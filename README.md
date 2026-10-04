# Autoencoders with Keras in R

An R-based deep-learning project that uses **Keras/TensorFlow autoencoders** to learn a compact representation of a high-dimensional dataset and then uses the learned embedding for downstream classification.

## Project overview

The workflow combines modern preprocessing, neural-network representation learning and supervised modelling. A dense autoencoder compresses 112 numeric predictors into a low-dimensional embedding, which is then used as the feature space for a classification model.

## Repository contents

- [`keras_basics.Rmd`](keras_basics.Rmd) — complete R Markdown workflow.

## Methods and tools

The analysis uses:

- `keras` and `tensorflow` for the autoencoder,
- `tidymodels` for preprocessing, splitting and modelling,
- `data.table` for efficient data loading,
- `tidyverse` for data manipulation.

Key steps include:

- stratified train/test splitting,
- Yeo-Johnson transformation and normalization,
- dense autoencoder training with early stopping,
- extraction of the neural-network embedding,
- supervised modelling on the learned features.

## Data requirements

The R Markdown file references a large local CSV file via a machine-specific absolute path. The dataset is not committed to this repository, so that path must be updated before reproduction.

## Reproducing the analysis

1. Install R, TensorFlow/Keras for R and the packages listed in the source file.
2. Update the data path in `keras_basics.Rmd`.
3. Open the project in RStudio and run or knit the document.

## Scope

This repository demonstrates representation learning with autoencoders in R and the integration of deep features with a traditional supervised-learning workflow.
