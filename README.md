# Zircon Age Prediction with Machine Learning

This project explores the application of machine learning to geochronological data, with the goal of predicting zircon ages from isotopic ratios.

## Context

This project was inspired by a university activity on a related topic. The class is **Physics IV**, but I decided to extend the idea and develop this notebook as an additional independent exploration.

## Objective

The main goal is to predict zircon ages using U–Pb isotopic measurements and evaluate how well a machine learning model can approximate relationships that are usually described through physical geochronological methods.

## Project Files

This repository currently contains:

- `geoclassification.ipynb` — the main notebook with data loading, preprocessing, model training, evaluation, and visualization
- `data/Database_v2.1_part1.xlsx` — the dataset file used in the analysis
- `requirements.txt` — required Python libraries
- `README.md` — project documentation

## Dataset

The dataset used in this project is part of the **Global Zircon U–Th–Pb Database**.

Main input features used:
- `isotope206Pb/238U`
- `isotope207Pb/235U`
- `isotope207Pb/206Pb`

Target variable:
- `age207Pb/206Pb`

## Methodology

The workflow in the notebook includes:

1. Loading the Excel dataset
2. Fixing the correct header row
3. Selecting isotopic features
4. Handling missing values
5. Training a Random Forest regression model
6. Evaluating model performance using MAE and R²
7. Plotting real vs predicted ages
8. Filtering physically inconsistent and extreme outliers
9. Retraining the model after data refinement

## Results

### Initial model performance
- **MAE:** ~34.4 Ma
- **R²:** ~0.892

### Performance after outlier filtering
- **MAE:** ~25.6 Ma
- **R²:** ~0.980

These results show that filtering unrealistic values significantly improved the model's performance and produced a more physically consistent prediction pattern.

## Visualization

The notebook includes a scatter plot comparing real and predicted ages:

- each blue point represents one sample
- the red diagonal line represents perfect predictions (`y = x`)

After filtering unrealistic values, the points became much more concentrated around the ideal line.

## How to Run

Install the dependencies:

```bash
pip install -r requirements.txt
