# Data directory

The raw datasets used by this project are not committed here.

Expected layout:

```text
data/
├── wave_functions.csv
└── validation/
    └── shock_4.csv       # optional
```

`wave_functions.csv` is the large source dataset used to build the training/test sample. It must contain at least 113 columns, with the first 112 treated as predictors and column 113 as the target. `shock_4.csv` is an optional external validation dataset using the same schema.

The historical project materials do not contain a stable public download URL, version identifier or checksum for the original large wave-function files. To avoid pretending that an arbitrary similarly named dataset is identical, this repository documents the required schema but does not claim clean-download reproducibility of the raw data. Use the exact project data if available and record its provenance/checksum when reproducing results.

Keep these filenames and paths, or update the `data_path` / validation path declarations in [`../keras_autoencoder_pipeline.Rmd`](../keras_autoencoder_pipeline.Rmd).
