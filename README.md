# NMPrediction

This repository contains the NMPrediction executable and its compiled library. It does not contain source code.

The program reads a CSV dataset, imputes missing values, selects features, and reports cross-validated accuracy.

## Requirements

- Python 3.14
- pandas, NumPy, and scikit-learn for that same Python

```bash
python3.14 -m pip install pandas numpy scikit-learn
```

The compiled files were built for Python 3.14. An older `python3` will not load them.

## Run

From this directory:

```bash
python3.14 bin/nmprediction data.csv --decision Outcome
```

`data.csv` is your dataset. `--decision` names the class column. If you omit it, the last column is used.

Missing cells may be blank, `?`, `NA`, or `N/A`.

Optional arguments:

```bash
python3.14 bin/nmprediction data.csv --decision Outcome --folds 10 --seed 42
```

- `--folds` is the number of cross-validation folds. The default is 10.
- `--seed` fixes the random seed. The default is 42.

The result is printed as JSON, including accuracy, sensitivity, specificity, AUC, and the selected features.

`bin/nmprediction` can also be run directly when `python3` on your `PATH` is Python 3.14:

```bash
chmod +x bin/nmprediction
./bin/nmprediction data.csv --decision Outcome
```

## Library

`lib/denguecad/` holds the compiled library used by the executable. You do not need to set `PYTHONPATH` to run `bin/nmprediction`.
