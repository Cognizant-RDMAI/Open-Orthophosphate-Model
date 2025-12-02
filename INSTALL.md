Installation Guide
This guide walks you through setting up the **BB1C: Estimate Phosphate/ Orthophosphate & reduce reliance on time consuming lab testing** project in your local or cloud environment.
 
> **Note:** This repository is shared for transparency and reproducibility.  
> Code contributions are not accepted at this time.
 
--- 
## Installation Instructions
### 1. Clone the repository

## Pre-Installation
    The GitHub version includes Jupyter notebooks. It is assumed that you have Anaconda installed and 
    access to Jupyter if you are running the model on a local machine. Alternatively, you can set up 
    equivalent iPython editors such as Vertex AI in Google Cloud Platform or Azure ML Studio in 
    Azure Cloud to execute these notebooks. Please refer to Anaconda's download and installation 
    instructions on their website: https://www.anaconda.com/download.

## ⚙️ Installation
    Clone the repository:
    ```bash
    git clone "https://github.com/Cognizant-RDMAI/Open_Orthophosphate_model"
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

    Pre-requisite: Python 3.7 and 3.10.
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
model = lgb.Booster(model_file='./Open_Orthophosphate_model/03_prediction_model/pkls/LGBM_WithRMon_R1.pkl')
```

### Make Predictions
#See 11_nb_orthop_predict_main.ipynb for detailed data pre-processing, predictions, and SHAP visuals.
```python
import pandas as pd
# Load sample data (ensure features match trained model)
data = pd.read_csv('./templates/input_template_orthop2959_pred_lgbm.csv')
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
    └── Cognizant-RDMAI/Open-Orthophosphate-Model
       └──01_ingest_wq_data (Includes code to merge a 24-year dataset into a single file and generate a unique Water Quality Determinand list)
          |──01_nb_ingest_24yrs_wq_data.ipynb
          |──02_nb_comb_single_csv_file.ipynb
          └──03_nb_get_unique_dminands.ipynb
       └──02_eda (Includes code for Agglomerative analysis on chemical-based data) 
          |──04_nb_extract_chem_name.ipynb
          |──05_nb_chem_cluster_llm.ipynb
          |──06_nb_final_chem2.ipynb
          |──07_nb_transpose_2959_all1.ipynb
          |──08_nb_transpose_2959_all2.ipynb
          └──09_nb_correlation_2959_all.ipynb
       └──03_prediction_model
          |──bkup (Includes backup files for visuals, validation, and training)
          |──encoders (Contains all the encoders used in training data preparation. This is used to construct input data for the prediction)
          |──pkls (Includes pre-trained models utilising over 35 million data points)
          |──src (Includes a notebook detailing the model training process)
          |──templates (The folder includes templates to guide user input and provides a sample model output)
          └──11_nb_orthop_predict_main.ipynb (Step-by-step guide for prediction, model metrics, and SHAP visuals using a pre-trained model)
       └──99_Common_Utils
          └──99_NB_CommonUtils.ipynb
       └──CHANGELOG.md
       └──CONTRIBUTING.md
       └──INSTALL.md
       └──LICENSE
       └──README.md
       └──requirements.txt
```