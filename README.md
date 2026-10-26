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

## Test datasets

CSV files for a trial run are in `datasets/`. Run these from the repository directory.

A small example, with the decision in the last column:

```bash
python3.14 bin/nmprediction datasets/data.txt
```

Dengue datasets:

```bash
python3.14 bin/nmprediction datasets/dataset.csv --decision Outcome
python3.14 bin/nmprediction datasets/Dengue_clinical_dataset.csv --decision Outcome
python3.14 bin/nmprediction datasets/Dengue_diseases_dataset_modified.csv --decision dengue_label
python3.14 bin/nmprediction datasets/Dengue_hematology.csv --decision Result
python3.14 bin/nmprediction datasets/dengue.csv --decision Dengue
```

`datasets/dengue.csv` has 1,000,000 rows. The other dengue files are about 500 to 1,500 rows and are the practical tests. Columns named `Name` or `Id` are not used as features.

## Library

`lib/denguecad/` holds the compiled library used by the executable. You do not need to set `PYTHONPATH` to run `bin/nmprediction`.
