## Reliable Machine Learning Across Domains for Electrochemical Energy Storage Materials: Uncertainty, Transferability, and Deployment Risk

---

[![Python](https://img.shields.io/badge/Python-3.13.3-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.11.0-red.svg)](https://pytorch.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.8.0-yellow.svg)](https://scikit-learn.org/stable/)
[![Plotly](https://img.shields.io/badge/Plotly-6.7.0-orange.svg)](https://plotly.com/)
[![License: CC BY--SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-green.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.20448825-blue.svg)](https://doi.org/10.5281/zenodo.20448825)

---

This repository contains the inference-only analysis pipeline used in the manuscript:

Reliable Machine Learning Deployment Across Domains for Electrochemical Energy Storage Materials: Uncertainty, Transferability, and Deployment Risk

Submitted to iScience.

The code performs a reliability and deployment-safety audit of pretrained machine-learning representations applied to heterogeneous electrochemical energy-storage materials. The analysis includes experimentally measured porous carbons, experimentally measured and simulated metal–organic frameworks (MOFs), additional external porous carbon datasets, and external covalent triazine framework (CTF) datasets.

No model training, retraining, fine-tuning, or hyperparameter optimization is performed in this repository. All analyses operate on pretrained latent representations and fixed preprocessing artifacts generated in prior work.

---

## 🎯 Scientific Scope

This repository is designed to address the question:

When should machine-learning predictions for electrochemical energy-storage materials be trusted, treated cautiously, or rejected under domain shift?

The analysis is based on the following principles:

- Deployment reliability is governed by latent-space geometry and local representational support.
- Latent distance, local density, nearest-neighbor target-property discrepancy, and epistemic uncertainty jointly inform transferability.
- Safe interpolation-like and unsafe extrapolative regimes can be identified in learned representation space.
- Deployment-risk diagnostics can be applied to external inference-only datasets without retraining the model.

--- 

### Datasets

The analysis uses the following datasets:

- Experimentally measured porous carbons - carbon_dataset_experimental.xlsx
- Experimentally measured metal–organic frameworks - mof_dataset_experimental.xlsx
- Simulated metal–organic frameworks - mof_dataset_simulation.xlsx
- Additional external experimentally measured porous carbons - extra_carbon_exp.xlsx
- External experimentally measured covalent triazine framework materials - extra_CTF_exp.xlsx

The internal datasets are used for latent-space reliability auditing, whereas the additional porous carbon and CTF datasets are used as external inference-only datasets for deployment-risk assessment.

---

### 🔬 Core Analyses Implemented

1. Latent Geometry Diagnostics
- Latent radius and distance from the global latent centroid.
- k-nearest-neighbor latent distance.
- Local latent density.
- Domain-resolved latent-space structure.

2. Epistemic Uncertainty
- Monte Carlo dropout applied to the frozen latent encoder.
- Latent epistemic uncertainty estimated from repeated stochastic forward passes.

3. Neighborhood Connectivity
- k-nearest-neighbor graph construction.
- Domain-pair connectivity analysis.
- Quantification of local representational support across material domains.

4. Target-Property Smoothness and Transferability
- Nearest-neighbor target-property discrepancy, defined as the absolute difference in target property between a query sample and its latent-space neighbor.
- Distance-dependent discrepancy envelopes.
- Analysis performed for:
    - Gravimetric capacitance, (C_g)
    - Volumetric capacitance, (C_v)

This quantity is used as a local representation-smoothness diagnostic rather than as a direct supervised prediction error.

5. Density-Aware Reliability
- Relationship between nearest-neighbor target-property discrepancy and latent density.
- Neighborhood-based target-property variability.
- Local uncertainty trends as a function of latent distance and density.

6. Deployment Safety Mapping
- Distance–uncertainty safety maps.
- Safe, caution, and unsafe regimes defined by empirical thresholds.
- External inference-only datasets projected onto the internal safety map.
- Identification of unsupported or high-risk deployment regimes.

7. Sensitivity Analysis
- Relaxed neighborhood-size and binning thresholds.
- Robustness assessment of domain-pair discrepancy envelopes.
- Evaluation of whether reliability trends persist under reasonable analysis-parameter changes.

8. Internal Leave-One-Out Validation
- Leave-one-out latent-neighborhood validation for samples with available (C_g) and (C_v) labels.
- Comparison of absolute neighborhood-prediction error with latent distance, local density, epistemic uncertainty, and nearest-neighbor target-property discrepancy.

---

### 📁 Repository Structure

models_disentangled/
│
├── models/
│   └── latent_encoder_*.pt
│
├── results/
│   ├── core_latent_metrics.csv
│   ├── transfer_discrepancy_vs_latent_distance.csv
│   ├── domain_pair_reliability_table.csv
│   ├── safety_map_classification.csv
│   ├── representative_reliability_cases.csv
│   ├── figure_*.png
│   ├── figure_*.html
│   └── supplementary_*.csv
│
├── X_input.npy
├── domains.pkl
├── Y_targets.npy
├── target_cols.pkl
├── feature_scaler.pkl
├── feature_cols.pkl
├── predictions_ann_uncertainty.pkl
├── environment_versions.txt
└── run_manifest.json

--- 

## ⚙️ Requirements

The final analysis was performed using Python 3.13.3.

- numpy==2.4.4
- pandas==3.0.2
- scipy==1.17.1
- scikit-learn==1.8.0
- joblib==1.5.3
- torch==2.11.0
- umap-learn==0.5.12
- plotly==6.7.0
- openpyxl==3.1.5
- nbformat==5.10.4
- kaleido==1.3.0

To install the required packages:

pip install -r requirements.txt

---

### 🚀 Usage

Run the full analysis notebook:

Latent_Space_Transfer.ipynb

The notebook performs the following steps:

- Loads fixed preprocessing artifacts and pretrained latent encoder.
- Computes latent embeddings in inference mode.
- Calculates latent geometry, local density, and neighborhood connectivity.
- Estimates epistemic uncertainty using Monte Carlo dropout.
- Computes nearest-neighbor target-property discrepancy for available targets.
- Generates domain-pair reliability diagnostics.
- Constructs internal and external deployment safety maps.
- Runs sensitivity analyses.
- Exports all figures, tables, and reproducibility files.

Generated outputs are saved to:

models_disentangled/results/

---

### 🔁 Reproducibility

The analysis is designed for reproducibility and auditability:

- No retraining or hyperparameter optimization is performed.
- The pretrained encoder is used as a frozen representation model.
- Fixed preprocessing artifacts are loaded explicitly.
- Random seeds are fixed where applicable.
- Software versions are recorded in environment_versions.txt.
- Analysis settings and selected artifacts are recorded in run_manifest.json.
- Figures and tables are exported automatically from the notebook.

---

## 📜 License

Creative Commons Attribution Share Alike 4.0 International
Permits almost any use subject to providing credit and license notice. Frequently used for media assets and educational materials. The most common license for Open Access scientific publications. Not recommended for software.

---

## 📬 Author

For questions or clarifications related to the methodology or scripts, please contact the corresponding author listed in the manuscript.

- Developed By: Henry Reynolds Nana Benyin Enninful
- 📧 Email: hrnbenninful@gmail.com
- 🐙 GitHub: @HRNBEnninful
- 💼 LinkedIn: https://www.linkedin.com/in/henryrnbenninful/

---
