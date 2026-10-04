# Data directory

The raw datasets used by this project are intentionally not committed here.

Expected layout:

```text
data/
├── wave_functions.csv
└── validation/
    └── shock_4.csv
```

`wave_functions.csv` is the large source dataset used to build the training/test sample. `shock_4.csv` is an external validation dataset with the target in the final column.

Keep these filenames and paths, or update the `file.path(...)` declarations in `keras_basics.Rmd`.
