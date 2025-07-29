Installation Guide
This guide walks you through setting up the **BB1C -BB1C: Estimate Phosphate/ Orthophosphate & reduce reliance on time consuming lab testing** project in your local or cloud environment.
 
> **Note:** This repository is shared for transparency and reproducibility.  
> Code contributions are not accepted at this time.
 
--- 
## Installation Instructions
### 1. Clone the repository

## ⚙️ Installation
    Clone the repository:
    ```bash
    git clone https://github.com/Cognizant-RDMAI/BB1C_Phosphate_Orthophosphate_model
    ``` 
### 2. Create a Python Virtual Environment (Optional but Recommended)
 
Using a virtual environment avoids conflicts with other Python packages on your system
    ```
    python3 -m venv venv
    source venv/bin/activate    #macOS/Linux
    venv/Scripts/Activate       #Windows
    ```
This creates an isolated environment where all dependencies will be installed.

### 3. Install dependencies:

    Pre-requisite: Python 3.7 or higher.
    ```bash
    pip install -r requirements.txt
    ```
    *Key libraries: LightGBM, SHAP, ChemDataExtractor, pandas.*
    ```
This includes:
- matplotlib
- pandas
- NumPy: Array and math operations
- yellowbrick
- scikit-learn
- Spacy
- RoBERTa, ChemBERTa
- lightgbm
- rdkit
- chemDataExtractor
- lightgbm
- PubChemPy
- xgboost
- tensorflow, tf_keras

## 🛠️ Usage
### Load the Pre-Trained Model
```python
import lightgbm as lgb
model = lgb.Booster(model_file='models/orthophosphate_lightgbm_v1.3.txt')
```

### Make Predictions
```python
import pandas as pd
# Load sample data (ensure features match trained model)
data = pd.read_csv('data/validation_sample.csv')
predictions = model.predict(data)
```

### Explain Predictions with SHAP
```python
import shap
explainer = shap.TreeExplainer(model)
shap_values = explainer.shap_values(data)
shap.summary_plot(shap_values, data, feature_names=data.columns)
```

### 3. Ingest Real Time Data and Run E2E pipeline
Input data should be either API callable via JSON or in the form of CSV:
```
Directory & File Structure
    └── BB1C_Phosphate_Orthophosphate_model
       └──01_ingest_wq_data (Contains the code to ingest the 24 years of dataset into single file. Obtaining unique Water Quality Determinand list
          |──01_nb_ingest_24yrs_wq_data.ipynb
          |──02_nb_comb_single_csv_file.ipynb
          └──03_nb_get_unique_dminands.ipynb
       └──02_eda (Contains code for Agglomerative analysis on the chemical based 
          |──04_nb_extract_chem_name.ipynb
          |──05_nb_chem_cluster_llm.ipynb
          |──06_nb_final_chem2.ipynb
          |──07_nb_transpose_2959_all1.ipynb
          |──08_nb_transpose_2959_all2.ipynb
          └──09_nb_correlation_2959_all.ipynb
       └──03_prediction_model
          |──encoders (Contains all the encoders used in training data preparation. This is used to construct input data for the prediction
          |──pkls (Contains the Pre-Trained models using 35+ Million datapoints
          |──src (Contains the Trained model code)
          |──templates (Contains the templates guiding user input format)
          └──11_nb_validate_orthop2959_pred_lgbm.ipynb (Main Model used for orthophosphate prediction. Insights generation using SHAP framework)
       └──CHANGELOG.md
       └──CONTRIBUTING.md
       └──INSTALL.md
       └──LICENSE
       └──README.md
       └──reqiorements.txt

```
