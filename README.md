# Autoencoder Representation Learning with Keras 3 in R

An R-based deep-learning project that uses **Keras 3 with the TensorFlow backend** to learn a compact representation of high-dimensional wave-function data, then trains an XGBoost classifier on the learned embedding.

## Project overview

The workflow combines training-only preprocessing, neural-network representation learning and supervised classification. A dense autoencoder compresses 112 numeric predictors into a six-dimensional embedding, which becomes the feature space for downstream classification.

## Repository contents

- [`keras_autoencoder_pipeline.Rmd`](keras_autoencoder_pipeline.Rmd) — audited R Markdown workflow.
- [`data/README.md`](data/README.md) — expected dataset layout and provenance note.
- [`R-packages.txt`](R-packages.txt) — version-pinned direct R package dependencies.
- [`.github/workflows/r-ci.yml`](.github/workflows/r-ci.yml) — R 4.6.1 dependency/syntax CI.
- [`.gitignore`](.gitignore) — local R/Keras and raw-data exclusions.

## Validation design

The pipeline creates a stratified held-out test set **before** learned preprocessing. The preprocessing recipe and autoencoder are fitted using training data only. The autoencoder uses 20% of the training partition for early stopping, and its best weights are restored before embeddings are extracted.

The downstream XGBoost classifier uses a **fixed, pre-specified baseline configuration**. It is not tuned by cross-validation on an embedding that has already been learned from the complete outer training partition. This removes the earlier validation-boundary mismatch and leaves the untouched held-out test set as the single performance-evaluation set.

Optional external validation data are transformed using the already-fitted preprocessing recipe, autoencoder and classifier; the workflow does not refit on validation data.

## Reproducibility

The direct R package versions are pinned in [`R-packages.txt`](R-packages.txt). CI uses R 4.6.1 and `pak` to install those exact direct versions, then extracts and parses the canonical R Markdown source.

The workflow uses `keras3::set_random_seed()` so the main R, Python, NumPy and backend random-number generators are seeded together. XGBoost is also run single-threaded with a fixed seed. Exact bit-for-bit neural-network results can still depend on the resolved Python Keras/TensorFlow backend, hardware and accelerator operations. The R package manifest therefore improves reproducibility without overstating full backend determinism.

`R-packages.txt` pins direct R dependencies; it is not a complete `renv.lock` for recursive R dependencies or a Python backend lockfile.

## Methods and tools

The analysis uses `keras3` with a TensorFlow backend for representation learning, `tidymodels` for splitting/preprocessing/workflow construction, XGBoost for a fixed downstream classification baseline, `data.table` for efficient loading and `caret` for confusion-matrix reporting.

## Data requirements

The raw datasets are not stored in this repository. Place them under the `data/` structure described in [`data/README.md`](data/README.md). The external validation file is optional; the main train/test workflow runs without it.

## Running the analysis

1. Install R 4.6.1.
2. Install `pak` and the pinned direct R dependencies:

```r
install.packages("pak")
pak::pkg_install(readLines("R-packages.txt"), upgrade = FALSE)
```

3. Install/configure the TensorFlow backend with `keras3::install_keras(backend = "tensorflow")` if it is not already available.
4. Place the dataset under `data/`.
5. Run or knit `keras_autoencoder_pipeline.Rmd` from top to bottom.

## Scope

This project demonstrates representation learning with explicit train/test boundaries and a deliberately fixed downstream baseline. It is a data-science portfolio project rather than a production inference service.
