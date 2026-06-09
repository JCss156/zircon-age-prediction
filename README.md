# Zircon Geochemistry Age Classification

This project explores the use of machine learning to classify zircon samples into geological age ranges based on geochemical and auxiliary isotopic features.

The goal is not to replace radiometric dating methods such as U-Pb geochronology. Instead, this project investigates whether zircon chemistry and isotopic signatures contain enough information to support preliminary age-range classification, large-scale data screening, and geological interpretation.

## Project Motivation

Zircon is one of the most important minerals in geochronology because it commonly incorporates uranium into its crystal structure while excluding initial lead. This makes it highly suitable for U-Pb dating.

An initial version of this project attempted to predict zircon ages directly from U-Pb isotopic ratios. However, this approach was scientifically limited, because U-Pb ages are already calculated from those ratios using radioactive decay equations.

The project was therefore reformulated to avoid directly reproducing the physical age equation. The current version uses geochemical and auxiliary isotopic variables, such as U, Th, Th/U, Hf isotopic ratios, and rare earth elements, to classify zircons into broad age intervals.

## Research Question

Can geochemical and auxiliary isotopic signatures of zircons be used to classify samples into geological age ranges?

## Dataset

This project uses the GEOSCRAPE/Martin zircon database, which compiles published zircon geochronology, geochemistry, and isotopic data.

The dataset includes information such as:

* U-Pb ages;
* U and Th concentrations;
* Th/U ratio;
* Hf isotopic ratios;
* rare earth element concentrations;
* analytical method;
* lithology;
* geographic information;
* sample and publication metadata.

The raw dataset is not included in this repository due to file size. It can be downloaded from the original GEOSCRAPE/Martin zircon database source.

Expected local data files:

```text
2021-10-FWQ7DT_Martin_data.csv
2021-11-FWQ7DT_Martin_data-sources.csv
2021-12_FWQ7DT_Martin_Data-Description.xlsx
```

## Methodology

The project follows these main steps:

1. Load and inspect the zircon database.
2. Identify available geochemical and isotopic features.
3. Remove direct U-Pb age-leakage features from the model inputs.
4. Filter samples with sufficient geochemical data.
5. Create broad geological age classes from U-Pb ages.
6. Train a machine learning classifier.
7. Evaluate the model using accuracy, precision, recall, F1-score, and a confusion matrix.
8. Analyze feature importance to identify the most relevant variables.

## Age Classes

The continuous U-Pb age values were converted into broad geological age intervals:

| Age class    | Approximate interpretation |
| ------------ | -------------------------- |
| 0–250 Ma     | Mesozoic/Cenozoic          |
| 250–541 Ma   | Paleozoic                  |
| 541–1000 Ma  | Neoproterozoic             |
| 1000–1600 Ma | Mesoproterozoic            |
| 1600–2500 Ma | Paleoproterozoic           |
| >2500 Ma     | Archean                    |

The classification approach was chosen because predicting exact ages from geochemistry alone is less realistic and less geologically meaningful than estimating broad temporal groups.

## Model

The main model used in this project is a Random Forest Classifier.

Input features include variables such as:

* `u_ppm`
* `th_ppm`
* `th_u_ratio`
* Hf isotopic ratios
* Lu-Hf related ratios
* rare earth element concentrations when available

The target variable is the zircon age class.

## Results

Using samples with at least five available geochemical or auxiliary isotopic features, the model achieved approximately:

```text
Accuracy: ~77.8%
```

The best-performing classes were:

* 0–250 Ma
* > 2500 Ma
* 1600–2500 Ma

The model had more difficulty separating intermediate age ranges, especially between 541–1000 Ma, 1000–1600 Ma, and 1600–2500 Ma. This is expected because geological age boundaries are artificial and zircon geochemical signatures may vary gradually rather than abruptly.

## Feature Importance

The most important feature in the Random Forest model was:

```text
176Hf/177Hf
```

This result is geologically meaningful because Hf isotopes in zircon are related to crustal evolution and mantle-crust differentiation processes.

Other relevant features included:

* U concentration;
* Th concentration;
* Th/U ratio;
* Lu-Hf and Yb-Hf ratios;
* Ti;
* rare earth elements such as Ce, Nd, Sm, Eu, Gd, and Yb.

## Interpretation

The results suggest that zircon geochemical and auxiliary isotopic signatures contain useful information for broad age-range classification.

However, this model does not replace U-Pb dating. Radiometric dating remains the physical method for determining crystallization ages. The machine learning model should be understood as a complementary tool for:

* preliminary screening of large zircon databases;
* identifying broad temporal patterns;
* supporting geological interpretation;
* selecting samples for further analysis;
* exploring relationships between zircon chemistry and crustal evolution.

## Limitations

This project has several limitations:

* Many geochemical columns in the dataset are highly incomplete.
* The model depends on available published data and may reflect sampling bias.
* Broad age classes simplify continuous geological time.
* Some variables may be indirectly related to age through geological processes rather than directly predictive.
* The model should not be interpreted as a substitute for radiometric dating.
* Additional validation with independent datasets would be necessary before practical use.

## Scientific Relevance

This project demonstrates a more defensible use of machine learning in geochronology than direct prediction of U-Pb ages from U-Pb ratios.

Instead of replacing the physics of radioactive decay, the model explores whether zircon geochemistry can provide complementary information about age populations and geological evolution.

In this sense, machine learning is used not as an alternative to radiometric dating, but as a tool for data exploration, classification, and interpretation.

## Repository Structure

```text
.
├── README.md
├── notebooks/
│   ├── 01_old_upb_age_prediction.ipynb
│   └── 02_geochemical_age_classification.ipynb
├── data/
│   └── README_data.md
├───evolution
├── results/
│   ├── confusion_matrix.png
│   └── feature_importance.png
└── .gitignore
```

## Requirements

Main Python libraries used:

```text
pandas
numpy
scikit-learn
matplotlib
seaborn
openpyxl
```

Install dependencies with:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn openpyxl
```

## Future Work

Possible future improvements include:

* testing other models such as XGBoost, LightGBM, and neural networks;
* using regression and comparing it with classification;
* improving feature engineering with geochemical ratios;
* adding tectonic setting or lithological classification;
* validating the model with independent zircon datasets;
* comparing machine learning results with standard geochemical discrimination diagrams;
* applying the workflow to mineral exploration datasets.

## Author

João Carlos Silva de Souza
Computer Engineering — UFRGS

## License

This repository is intended for academic and educational purposes.

