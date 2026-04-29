# maryam
A practical starter ML project for tabular classification with multiple supervised models.

## What is implemented

- CSV dataset loading
- Numeric and categorical preprocessing
- Train/validation split
- Model training and comparison across logistic regression, KNN, decision tree, random forest, and naive Bayes
- Evaluation metrics (accuracy, precision, recall, f1, ROC-AUC, confusion matrix counts)
- Saved model pipeline artifact
- Comparison SVG generation from the summary CSV

## Setup

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Run with your CSV

```bash
python -m src.ml_project.train \
  --data-path /path/to/data.csv \
  --target-col target
```

To compare all supported models in one run, use the default:

```bash
python -m src.ml_project.train --data-path /path/to/data.csv --target-col target --model all
```

## Quick run without a CSV

If `--data-path` is omitted, a synthetic dataset is generated:

```bash
python -m src.ml_project.train --target-col target
```

Model artifacts are written to `artifacts/`.

To generate the comparison chart:

```bash
python -m src.ml_project.visualize --summary-path artifacts/model_comparison.csv
```

## Single command for Heart + Diabetes

If you have `data/heart.csv` and `data/diabetes.csv`, run everything in one step:

```bash
python -m src.ml_project.domain_run
```

This command will:
- train all supported models on both datasets
- generate comparison tables and charts in `artifacts/heart` and `artifacts/diabetes`
- create a combined presentation report at `artifacts/domain_summary.md`

Optional flags:

```bash
python -m src.ml_project.domain_run \
  --heart-path data/heart.csv \
  --heart-target target \
  --diabetes-path data/diabetes.csv \
  --diabetes-target Outcome \
  --output-dir artifacts
```

## Web App UI (Flask)

Launch a browser-based interface to upload a CSV, select target/model, and train:

```bash
python -m src.ml_project.webapp
```

Then open http://127.0.0.1:5000 in your browser.

The app lets you:
- upload a custom CSV or use a local file path
- run a single model or compare all models
- view metrics and best-model summary
- write artifacts to a custom output folder
- load a saved `.joblib` model and run single-row prediction from CSV input

## Notes

- The loader accepts any tabular CSV with a binary target column.
- For KNN, the pipeline automatically scales numeric features.
- The comparison run saves one model per classifier plus a `model_comparison.csv` summary.
