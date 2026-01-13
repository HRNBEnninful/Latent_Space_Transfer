## Reliable Machine Learning Across Domains for Electrochemical Energy Storage Materials: Uncertainty, Transferability, and Deployment Risk

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/)  
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.5.2-yellow.svg)](https://scikit-learn.org/stable/)  
[![Plotly & Dash](https://img.shields.io/badge/Plotly-Dash-orange.svg)](https://plotly.com/dash/) 
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)  
[![DOI](https://zenodo.org/badge/18178231.svg)](https://doi.org/10.5281/zenodo.18178231)

---

This repository contains the inference-only analysis pipeline used in the manuscript:

Reliable Machine Learning Across Domains for Electrochemical Energy Storage Materials: Uncertainty, Transferability, and Deployment Risk
(submitted to Joule)

The code performs a systematic reliability and deployment-safety audit of pre-trained machine-learning models applied to heterogeneous energy storage materials, including:

. Experimentally measured porous carbons - carbon_dataset_experimental.xlsx
. Simulated metal–organic frameworks (MOFs) - mof_dataset_simulation.xlsx
. Experimentally measured metal–organic frameworks (MOFs) - mof_dataset_experimental.xlsx
. Experimentally measured Covalent triazine frameworks (CTFs) - extra_CTF_exp.xlsx
. Extra Experimentally measured porous carbons - extra_carbon_exp.xlsx

No model training, retraining, or hyperparameter optimization is performed.
All analyses operate strictly on pre-trained representations developed in prior work. (Enninful 2026)

---

## 🎯 Scientific Scope

This repository is designed to answer: "When should machine-learning predictions for energy storage materials be trusted, and when should they be rejected?"

Key principles:
. Reliability is governed by latent geometry, not domain labels
. Latent distance, local density, and epistemic uncertainty jointly determine transferability
. Safe interpolation and unsafe extrapolation emerge naturally in representation space
. Deployment decisions can be made without access to target labels

--- 

### 🔬 Core Analyses Implemented

1. Latent Geometry Diagnostics
. Latent radius and centroid distance
. k-nearest-neighbor (kNN) distance and density
. Domain-resolved latent structure

2. Epistemic Uncertainty
. Monte Carlo dropout applied to the pre-trained latent encoder
. Optional loading of stored ANN uncertainty estimates

3. Neighborhood Connectivity
. kNN graph construction
. Domain-pair connectivity analysis

4. Transferability and Error Growth
. Neighbor-based transfer error |Δtarget|
. Distance-dependent error inflation
. Distance-binned error envelopes for:
    - Gravimetric capacitance
    - Volumetric capacitance

5. Density-Aware Reliability
. Transfer error vs latent density
. Local uncertainty proxy vs density and radius

6. Deployment Safety Mapping
. Distance–uncertainty “traffic-light” safety maps
. Safe / caution / unsafe regions defined by data-driven thresholds
. Projection of external experimental datasets (Figure 2f)

7. Sensitivity Analysis
. Relaxed neighborhood size and binning thresholds
. Robustness of conclusions to analysis hyperparameters

---

### 📁 Repository Structure

models_disentangled/
│
├── models/
│   └── latent_encoder_*.pt        # Pretrained latent encoder
│
├── results/                       # All generated outputs
│   ├── core_latent_metrics.csv
│   ├── transfer_error_vs_latent_distance.csv
│   ├── domain_pair_reliability_table.csv
│   ├── SI_Table_S1_safe_fraction_by_domain.csv
│   ├── SI_Table_S2_OOD_separation_score.csv
│   ├── fig*.png / fig*.html
│
├── X_input.npy                    # Model input features
├── domains.pkl                    # Domain labels
├── Y_targets.npy                  # Target values (optional)
├── target_cols.pkl                # Target names
├── feature_scaler.pkl             # Pretrained scaler
├── feature_cols.pkl               # Feature list
└── predictions_ann_uncertainty.pkl (optional)

--- 

## ⚙️ Requirements

. Python ≥ 3.9
. PyTorch
. NumPy, pandas
. scikit-learn
. Plotly
. joblib
. Optional:
. kaleido (for PNG export)

---

### 🚀 Usage

Run the full analysis
Latent_Space_Transfer.ipynb

This will:
. Compute latent geometry and uncertainty
. Generate all main-text figures
. Generate all supplementary figures and tables
. Save all outputs to models_disentangled/results/
. Run sensitivity analysis

---

### 🔁 Reproducibility

. All random seeds fixed
. Deterministic inference
. No retraining or tuning
. All preprocessing artifacts loaded explicitly

---

### 🧠 Optional Extensions (Clearly Non-Core)

The repository includes optional analyses for completeness:
. Calibrated probability of safety (logistic regression)
. Risk–coverage curves
. SHAP alignment with latent safety space

These are not required for the core conclusions and are reported as optional extensions in the Supplementary Information.

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
