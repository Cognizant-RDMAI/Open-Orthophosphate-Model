# 🌊 AI-Driven Open Model for Predicting Orthophosphate from Water Quality Monitoring Data

## 🧪 Overview

**Open Orthophosphate Model** 

***Transforming Water Quality Monitoring: AI-Driven Prediction of Orthophosphate Concentrations in River Catchments.***

## 📖 Introduction

Phosphorus chemical species serve as key indicators of nutrient pollution in aquatic systems, often measured as orthophosphate by regulators. Traditional methods of monitoring phosphorus chemical species are labour intensive and expensive. Consequently, measures of orthophosphate are spatially and temporally sparse, representing approximately 2% of all records in the Environment Agency’s (EA’s) water quality database for England over 24 years. To address this, River Deep Mountain AI has developed a predictive framework, the Open Orthophosphate Model, using AI/ML (Artificial Intelligence & Machine Learning. The Open Orthophosphate Model estimates orthophosphate from other monitored water quality parameters, leveraging the water quality data collected by the EA over 24 years. The Open Orthophosphate Model integrates molecular chemistry, spatiotemporal analysis, and regulatory compliance to support scalable, cost-effective monitoring. This work helps to address environmental, regulatory, and technical gaps in water quality monitoring.

This repository hosts an AI/ML framework that predicts orthophosphate (OrthoP) levels in river surface water in England using a pre-trained LightGBM model. This model could be further developed to predict orthophosphate levels in other water body types, such as lakes/ponds/reservoirs and groundwater. The model could also be adapted to predict other chemical forms of phosphorus, such as total phosphorus.

**Key Impact**: 
Supports traditional monitoring practices by inferring orthophosphate levels using easily obtainable water quality parameters. Supports UN Sustainable Development Goal 6 (Clean Water) and the UK's Net Zero targets. 🌍

## 📊 Model Details
- **Algorithm**: LightGBM (Gradient Boosting Decision Tree) outperformed XGBoost, ANN (Artificial Neural Network), and linear regression.
- **Key Features**:
  - 45 most representative features for predicting orthophosphate levels. Please note that not all listed features are needed for the Open Orthophosphate Model to predict orthophosphate: the more that are provided, the more accurate the estimations of orthophosphate will be. These features include:
      - **36 Representative features identified using Machine Learning (ML) algorithms**: e.g., Ammonia, nitrate, pH, dissolved oxygen.
      - **3 Domain expert-curated features: Conductivity, precipitation, temperature.
      - **6 Regulatory features: Section 82 parameters, e.g., un-ionised ammonia, dissolved oxygen, water temperature and pH.

## 🚀 Performance Summary
- **Accuracy**: Predicts orthophosphate with Mean Absolute Error (MAE) of 0.01 and Mean Squared Error (MSE) of 0.00123.**.
- **Hybrid approach**: Combines **ML identified features** (e.g., ammonia, nitrate) with domain-expert insights (e.g., conductivity, precipitation).
- **Explainable AI**: SHapley Additive exPlanations (SHAP) framework reveals drivers such as ammonia (76% impact) and seasonal trends.
- **Scalable**: There are over 64,000 sampling points across England where water quality is being monitored by the EA. The model was trained using orthophosphate data collected from over 18,000 of these sampling points. However, the model can be applied to predict orthophosphate both at points for which some orthophosphate data exist and for points for which no orthophosphate data exist.
- **Open source**: Core algorithms are publicly available for transparency. 🔍

****
- 📈 **Performance Results**:
- **Testing**: Machine Learning Model: LightGBM data volume: 33.7 million (90% for training & 10% testing, stratified split). Sampling point coverage: over 64,000 across England.
  - **Mean Absolute Error**: 0.01
  - **Mean Squared Error**: 0.00123
  - **Root Mean Squared Error**: 0.04
  - **Normalised Root Mean Squared Error**: 8%

- **Validation**: 158 ground-truth observations from EA's data for Northumberland region captured during the years 2000 to 2022.
  - **Mean Absolute Error**: 0.02
  - **Mean Squared Error**: 0.00088
  - **Root Mean Squared Error**: 0.03
  - **Normalised Root Mean Squared Error**: 7.89%

- **Hotspots Identified**: Agricultural runoff in Tees Valley, mining impacts in Durham.
****

## 📜 License
MIT License. See [LICENSE] for details.


## 📊 Data Summary

The open orthophosphate modeling project harnesses an a comprehensive dataset - 24 years of water quality archives from the Environment Agency, measured at 64,000+ sampling points across England. This includes 3,261 water quality parameters — from pH levels to nutrient concentrations—offering a holistic view of catchment dynamics. The Environment Agency dataset was used in Exploratory Data Analysis (EDA) to build training data for this model. EDA data including approximately 70 million samples from 64,000+ sampling points collected during Jan-2000 until May 2024 were analysed, incorporating all water body types. Later, sample data points were restricted for river surface water (classified in the EA database as ‘River / Running Surface’ samples) for final model consumption. Of the extensive analysis on the 3,261 water quality determinands, 45 representative determinands were selected to build the training dataset. Along with this, spatiotemporal metadata such as latitude, longitude, sampling point notation, timestamp, and additional temporal-based feature-engineered parameters were finalised. Below is the list of input parameters to the model.

## ✔️ Acceptable INPUT parameters to the model:

**References and known limitations**: Refer to the Environmental Agency Archive for information on water quality notations. The model uses these notations as per EA's standard notations.

Please note, if an observation has a prefix of < or > to indicate a 'limit of detection', remove these and provide the numerical value as provided by the EA. Currently, the model works based on the weightage for a given numerical value.

        00. samplingPoint_notation  - Sampling point location

The table below illustrates the input variables the model accepts. The Notations ID for the determinands are integers ranging from 1 to 9995. The "Name" and "Descriptions" are taken as such from the Environment Agency's water quality standard notations.

        01. sampleDateOnly          - Date the sample was taken. Acceptable format: dd/mm/yyyy
        02. samplingPoint_easting   - Easting British National Grid (BNG) Coordinates
        03. samplingPoint_northing  - Northing (BNG Coordinates)
        04. purpose_name            - Purpose Name (e.g. 'PLANNED INVESTIGATION (LOCAL MONITORING)')
        05. determinand_unit_name   - Unit of Measure (e.g. mg/l) - Model automatically considers this, no need to give as input
        06. isComplianceSample      - Is this a compliance sample or not (e.g. TRUE or FALSE)

        Other Water Quality Parameters: - 
        **(Please note, the more parameters we provide, the greater the accuracy)**
        ===============================================================================
        SNO Notations ID   Name                 Description
        ===============================================================================
        07. 0116           N Oxidised           Nitrogen, Total Oxidised as N
        08. 0111           Ammonia(N)           Ammoniacal Nitrogen as N
        09. 0117           Nitrate-N            Nitrate as N
        10. 0118           Nitrite-N            Nitrite as N
        11. 0119           NH3 un-ion           Ammonia un-ionised as N
        12. 9924           Oxygen Diss          Oxygen, Dissolved as O2
        13. 0162           Alky pH 4.5          Alkalinity to pH 4.5 as CaCO3
        14. 0085           BOD ATU              BOD : 5 Day ATU
        15. 0135           Sld Sus@105C         Solids, Suspended at 105 C
        16. 0172           Chloride Ion         Chloride
        17. 0241           Calcium - Ca         Calcium
        18. 0237           Magnesium-Mg         Magnesium
        19. 0158           Hardness             Hardness, Total as CaCO3
        20. 0182           SiO2 Rv              Silica, reactive as SiO2
        21. 0348           Phosphorus-P         Phosphorus, Total as P
        22. 0211           Potassium- K         Potassium
        23. 03683          N Inorganic          Nitrogen, Total Inorganic : (Calculated)
        24. 0192           Phosphate            Phosphate :- {TIP}
        25. 9686           Nitrogen - N         Nitrogen, Total as N
        26. 0114           N-Kjeldahl           Nitrogen, Kjeldahl as N
        27. 0113           N Organic            Nitrogen, Organic as N
        28. 0076           Temp Water           Temperature of Water
        29. 0301           C - Org Filt         Carbon, Organic, Dissolved as C :- {DOC}
        30. 0061           pH                   pH
        31. 9901           O Diss %sat          Oxygen, Dissolved, % Saturation
        32. 0183           Sulphate SO4         Sulphate as SO4
        33. 0143           Sld NV@500C          Solids, non-volatile at 500 C
        34. 0461           DtrgtAncSyn          Detergents, Anionic
        35. 0207           Sodium - Na          Sodium
        36. 0463           Dtrgt NncSyn         Detergents, Non-ionic
        37. 0177           Fluoride - F         Fluoride
        38. 0077           Cond @ 25C           Conductivity at 25 C
        39. 6450           Cu Filtered          Copper, Dissolved
        40. 6455           Zinc - as Zn         Zinc
        41. 0749           Phenols Mono         Phenols : Monohydric as Phenol
        42. 0209           K- Filtered          Potassium, Dissolved
        43. 0205           Na- Filtered         Sodium, Dissolved
        44. 9856           OrthophsFilt         Orthophosphate, Dissolved
        45. 7859           SO4dis               Sulphate, Dissolved as SO4
        46. 1183           WethPresPrec         Weather : Precipitation
        47. 0239           Ca Filtered          Calcium, Dissolved
        48. 0175           Cyanide - CN         Cyanide as CN
        49. 0235           Mg Filtered          Magnesium, Dissolved
        50. 1181           WethPresTemp         Weather : Temperature
        51. 0082           O Dissolved          Oxygen, Dissolved : (Laboratory) as O2
        52. 0068           Turbidity            Turbidity

- **Please note, the following parameters can be supplied if available**

        53. 0180           OrthoP     (Supplied to validate the model accuracy, but is not required for predictions)
        54. 0192           Phosphate  (optional)
        55. 0348           Phosphorus (optional)
    
- **In the above acceptable input variables, the following are the Section-82 Regulatory parameters**

        Notation ID Description
        ===================================================
        0119        Ammonia un-ionised as N
        9924        Oxygen, Dissolved as O2
        0076        Temperature of Water
        0061        pH
        9901        Oxygen, Dissolved, % Saturation
        0082        Oxygen, Dissolved : (Laboratory) as O2
        0068        Turbidity

    **Samples considered for the model training**:
    - This model currently considers samples only from river surface water (classified as ‘River / Running Surface Water’ in the EA database).
    - It includes all samples under this category, including 'Reactive Monitoring Samples'.
    - The model eliminates sampling points with fewer than 100 observations over the past twenty-four years (2000 to 2024).

    **Input template**:
    - The format of the input template for obtaining orthophosphate predictions can be found in the "../03_prediction_model/templates" folder. 
    - A file named "input_template_orthop2959_pred_lgbm.csv" contains sample values for Eastings, Northings, Sampling point IDs, Purpose Names, and Unit of measure metrics are also available in the same folder.

**Output**:
Predicted orthophosphate value along with the metrics including SHAP explainable framework.

## **Key Findings, Strengths and Weaknesses**

**Key Findings**
- In England, of the 70 million water quality monitoring samples contained in the Environment Agency (EA) water quality monitoring database spanning 24 years of monitoring, phosphate (P) and orthophosphate (OrthoP) account for only 0.2% and 2% of those samples, respectively. 
- The dataset includes 70 million observations (2000-2024) from 55 rivers and 25 aquifers with 3,261 physico-chemical parameters and spatiotemporal metadata.
- Clustering: Identified 6 chemically distinct groups based on molecular similarity using Kmeans++ and agglomerative clustering. 
- Advanced techniques: Using SMILES text, Morgan Fingerprints, ChemBERTa (chemical-specific transformer), ChemDataExtractor, and PubChemPy enabled clustering of 370+ orthophosphate related determinands.
- Dimensionality reduction: PCA retained 93% variance after converting SMILES to Morgan Fingerprints (molecular bitmaps).
- Hybrid feature selection: A comprehensive hybrid approach was employed. This included incorporating feedback from domain experts, utilising advanced feature selection methods such as agglomerative clustering, and traditional correlation-based analysis, combined with multiple experiments. This approach was used to finalise the representative features.
- Exclusions: Non-reactive metals (e.g. zinc) were removed after domain expert review due to misclassification. Only ‘River Running / Surface Water’ samples were trained in the model.
- Model performance: LightGBM model outperformed XGBoost, Random Forest, ANN and linear regression models achieving:
    - MSE 0.00123
    - MAE 0.01
    - NRMSE 8%

**Strengths** 
- Predicts orthophosphate at 72% of unmonitored locations (MAE = 0.02, NRMSE = 7%).
- Combines ML with domain expertise for actionable insights. 
- Transparent via SHAP, critical for regulatory compliance.

**Weaknesses** 
- Struggles with extreme events (Since our training data is event driven).
- Mean Absolute Percentage Error (MAPE) undefined due to zero-value observations.

**Planned validations**: 
- Different zones of mean base flow index per WFD Operational Catchments.
- Different rainfall Zones – Wet versus Dry areas. 
- Benchmark catchments containing National River Flow Archive (NRFA) benchmark gauges. 
- Highly urbanised catchments for a few suggested WFD operational catchments.

**Extensibility**:
- The model predicts orthophosphate for a given sample dataset but currently cannot forecast based on past historical trends. However, this capability can be implemented in the future with minimal effort by changing the time lags.
- Although this model currently predicts orthophosphate, it can also be used to predict over 900 phosphorus family determinands by adjusting the target parameter. This is a core benefit of the chemical-based (Agglomerative) cluster analysis.
- The model currently predicts orthophosphate for river surface water but can be extended to predict orthophosphate in other water body types, such as lake/pond/reservoir water and groundwater.
- The model uses 2% of orthophosphate data sampled over the last 24 years (2000 to 2024) from 22,000 sampling points. However, there are 64,000 sampling points across England that the EA monitors for water quality. Hence, this model can retrospectively predict orthophosphate concentrations for the remaining 42,000 sampling points.
- The model training dataset does not currently include data in the EA water quality dataset from May 2024 onwards. This data may be used to ground truth the model.
- The model's current accuracy level is MSE - 0.00123, MAE - 0.01, and NRMSE - 8%, surpassing industry standards. (The acceptable AIML standards in general is less than 15%.)
- The model uses the SHAP framework to explain the reasons behind the predictions.
- The SHAP outcomes from this model can be integrated into a Generative AI Agentic workflow to easily obtain actionable insights and compare them with pollution incidents that occurred during the predicted orthophosphate period.
- The model uses water quality samples observed from catchments in England over the last 24 years. Therefore, it does not require additional data such as runoff, land use, or rainfall, as these effects are accurately reflected in the water quality database the model was trained with. Adding such data might cause the model to overlearn redundant information.

For further questions or support, please refer to the documentation or reach out to: pasupathi.narayanan@cognizant.com, nicolai.tarp@cognizant.com.

## Disclaimer

River Deep Mountain AI (“RDMAI”) consists of 10 parties. The parties currently participating in RDMAI are listed at the end of this section, and they are collectively referred to in these terms as the “consortium”.

This section provides additional context and usage guidance specific to the artificial intelligence models and / or software (the “Software”) distributed under the MIT License. It does not modify or override the terms of the MIT License. In the event of any conflict between this section and the terms of the MIT licence, the terms of the MIT licence shall take precedence.


#### 1. Research and Development Status

The Software has been created as part of a research and development project and reflects a point-in-time snapshot of an evolving project. It is provided without any warranty, representation or commitment of any kind including with regards to title, non-infringement, accuracy, completeness, or performance. The Software is for information purposes only and it is not: (1) intended for production use unless the user accepts full liability for its use of the Software and independently validates that the Software is appropriate for its required use; and / or (2) intended to be the basis of making any decision without independent validation. No party, including any member of the development consortium, is obligated to provide updates, maintenance, or support in relation to the Software and / or any associated documentation.

#### 2. Software Knowledge Cutoff

The Software was trained on publicly available data up to May 2025. It may not reflect current scientific understanding, environmental conditions, or regulatory standards. Users are solely responsible for verifying the accuracy, timeliness, and applicability of any outputs.

#### 3. Experimental and Generative Nature

The Software may exhibit limitations, including but not limited to:

- Inaccurate, incomplete, or misleading outputs;
- Embedded biases and / or assumptions in training data;
- Non-deterministic and / or unexpected behaviour;
- Limited transparency in model logic or decision-making

Users must critically evaluate and independently validate all outputs and exercise independent scientific, legal, and technical judgment when using the Software and
/ or any outputs. The Software is not a substitute for professional expertise and / or regulatory compliance.

#### 4. Usage Considerations

- Bias and Fairness: The Software may reflect biases present in its training data. Users are responsible for identifying and mitigating such biases in their applications.
- Ethical and Lawful Use: The Software is intended solely for lawful, ethical, and development purposes. It must not be used in any way that could result in harm to individuals, communities, and / or the environment, or in any way that violates applicable laws and / or regulations.
- Data Privacy: The Software was trained on publicly available datasets. Users must ensure compliance with all applicable data privacy laws and licensing terms when using the Software in any way.
- Environmental and Regulatory Risk: Users are not permitted to use the Software for environmental monitoring, regulatory reporting, or decision making in relation to public health, public policy and / or commercial matters. Any such use is in violation of these terms and at the user’s sole risk and discretion.

#### 5. No Liability

This section is intended to clarify, and not to limit or modify, the disclaimer of warranties and limitation of liability already provided under the MIT License.

To the extent permitted by applicable law, users acknowledge and agree that:

- The Software is not permitted for use in environmental monitoring, regulatory compliance, or decision making in relation to public health, public policy and / or commercial matters.
- Any use of the Software in such contexts is in violation of these terms and undertaken entirely at the user’s own risk.
- The development consortium and all consortium members, contributors and their affiliates expressly disclaim any responsibility or liability for any use of the Software including (but not limited to):
  - Environmental, ecological, public health, public policy or commercial outcomes
  - Regulatory and / or legal compliance failures
  - Misinterpretation, misuse, or reliance on the Software’s outputs
  - Any direct, indirect, incidental, or consequential damages arising from use of the Software including (but not limited to) any (1) loss of profit, (2) loss of use, (3) loss of income, (4) loss of production or accruals, (5) loss of anticipated savings, (6) loss of business or contracts, (7) loss or depletion of goodwill, (8) loss of goods, (9) loss or corruption of data, information, or software, (10) pure economic loss, or (11) wasted expenditure resulting from use of the Software —whether arising in contract, tort, or otherwise, even if foreseeable.

Users assume full responsibility for their use of the Software, validating the Software’s outputs and for any decisions and / or actions taken based on their use of the Software and / or its outputs.

#### 6. Consortium Members 
   
1. Northumbrian Water Limited
2. Cognizant Worldwide Limited
3. Xylem Water Solutions UK Limited
4. Water Research Centre Limited
5. RSK ADAS Limited
6. The Rivers Trust
7. Wessex Water Limited
8. Northern Ireland Water
9. Southwest Water Limited
10. Anglian Water Services Limited

## 🌟 Hashtags
#DataScience #PhosphorusModeling #OrthophosphatePrediction #WaterQuality #MachineLearning #EnvironmentalAI #AIModels #WaterTech #CleanWater #ClimateAction #HighVolumeData #EcoInnovation #SmartAgriculture #GreenTech #AIforGood #Sustainability #OpenScience #AI-Driven #TechForGood #ResponsibleAI #SHAP #PredictiveAnalytics #GitHubProjects

#### V.History:
- Created on 20 May 2025
- Updated on 25 Jun 2025
