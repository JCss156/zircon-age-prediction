# Zircon Age Prediction with Machine Learning

This project explores the application of machine learning to geochronological data, specifically aiming to predict zircon ages from isotopic ratios.

## Context

I started this project influenced by a university activity related to the same topic. The class is **Physics IV**, but I decided to go further and develop this code as an additional, independent exploration of the subject.

## Objective

The goal is to predict zircon ages using U–Pb isotopic system measurements, applying machine learning techniques to approximate relationships that are traditionally described by physical equations.

## Dataset

The dataset comes from the **Global Zircon U–Th–Pb Database** and includes measurements such as:

- `isotope206Pb/238U`
- `isotope207Pb/235U`
- `isotope207Pb/206Pb`

Target variable:
- `age207Pb/206Pb`

## Methodology

The workflow includes:

1. Loading and cleaning Excel data
2. Fixing the correct header row
3. Selecting relevant isotopic features
4. Handling missing values
5. Training a Random Forest regression model
6. Evaluating performance using MAE and R²
7. Visualizing predictions vs real values

## Results

Current model performance:

- **MAE:** ~25 Ma  
- **R²:** ~0.98  

These results indicate that the model captures most of the variation in zircon ages, despite the natural noise and uncertainty present in geochronological measurements.
After removing unrealistic outliers, the model showed a much clearer alignment between real and predicted zircon ages. MAE 34 -> 25 AND R² 0.89 -> 98
## Visualization

The scatter plot compares real and predicted ages:

- Each blue point represents a sample
- The red line represents perfect predictions (y = x)

## Repository Structure

```text
.
├── data/
├── notebooks/
├── README.md
├── requirements.txt
└── .gitignore
