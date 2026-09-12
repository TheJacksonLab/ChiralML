# Predictive and Interpretable Data-Driven Framework for Deciphering Chiral Emergence of Conjugated Polymers

This repository provides the supporting code and analysis data for the PNAS
manuscript *Predictive and
Interpretable Data-Driven Framework for Deciphering Chiral Emergence of
Conjugated Polymers*. It contains a data-processing example, analysis-ready
features, and figure-reproduction notebooks.

## Dataset

## Processing pipeline

[`processing_pipeline/Feature_Generation.ipynb`](processing_pipeline/Feature_Generation.ipynb)
is a single-data-point example of the feature-generation workflow. The user
supplies polymer and solvent structures, experimental conditions, molecular
weights, manually curated side-chain and backbone counts, and a COSMO-RS
solvation free energy. The notebook calculates RDKit and FASTSOLV descriptors,
applies molecular-weight normalization and family one-hot encoding, and returns
the 77 features used by the machine-learning workflow in a fixed order. Its
last section compares the generated values with a reference row.

Temperature is entered in degrees C and converted to K. Concentration is entered in
mg/mL. A second solvent and a second side chain are optional. The COSMO-RS
value is an external input and is not calculated by this notebook.

### Processing environment

The pipeline was prepared with Python 3.12 and requires:

- NumPy
- pandas
- RDKit
- FASTSOLV 1.0.1
- Jupyter Notebook or JupyterLab

FASTSOLV must have access to its pretrained checkpoints. Run all notebook cells
in order after editing the two input sections.

## Data analysis

[`data_analysis/data/analysis_data.xlsx`](data_analysis/data/analysis_data.xlsx)
contains the analysis-ready data used by all three figure notebooks:

- `Exp_ML_features`: 773 experimental rows with features.
- `Exp_ML_metadata`: labels and experimental metadata aligned by
  `experiment_id`.
- `All_Combination_features`: 3,124 feature combinations used for RF
  prediction and the extended FASTSOLV map.

The classification workflow trains on the labeled experimental features.
Figure 6c uses the all-combination features for both prediction and
plotting. Generated PNG files are written to
`data_analysis/outputs/figures/`.

### Analysis environment

The analysis notebooks were tested with Python 3.12.3 and require:

- NumPy 2.1.2
- pandas 2.3.2
- Matplotlib 3.10.5
- scikit-learn 1.7.1
- SHAP 0.48.0
- Pillow 11.0.0
- openpyxl 3.1.5
- Jupyter Notebook 7.4.7 and ipykernel 6.30.1

### Analysis notebooks

- [`Figure4.ipynb`](data_analysis/notebooks/Figure4.ipynb) reproduces Figure
  4b-d: the absolute g-factor distribution, repeated grouped out-of-fold
  precision-recall curves, and grouped out-of-fold regression parity plot.
- [`Figure6.ipynb`](data_analysis/notebooks/Figure6.ipynb) reproduces Figure
  6a-e: the combined SHAP plot, experimental FASTSOLV assembly map, RF
  prediction map, outcome fractions, and family-level FASTSOLV summary.
- [`Figure7.ipynb`](data_analysis/notebooks/Figure7.ipynb) reproduces Figure
  7a-d: Thiophene- and NDI-family SHAP plots, Thiophene-family outcome
  fractions, and the N2200 concentration series in chlorobenzene.
