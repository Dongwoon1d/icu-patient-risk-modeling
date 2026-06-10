# ICU Mortality Risk Modeling Using MIMIC-IV Demo

Focus: Healthcare Analytics · ICU Patient Risk · Clinical Data Modeling

## Overview

This project uses the MIMIC-IV Clinical Database Demo to build a prototype ICU mortality risk modeling pipeline.

The goal is to create an ICU stay-level dataset, explore basic mortality patterns, and build a baseline classification model to predict in-hospital mortality risk.

This project is designed as a portfolio prototype to demonstrate:

- Healthcare data preparation
- Multi-table clinical data merging
- Exploratory data analysis
- Baseline risk modeling
- Responsible handling of clinical data

> This project is not intended for clinical decision-making. It is a learning and portfolio project using demo data.

## Project Question

Can basic ICU patient information be used to identify patients with higher in-hospital mortality risk?

This project focuses on the following questions:

- How does mortality risk differ by age group?
- How does ICU length of stay relate to mortality outcome?
- Are certain admission types or ICU care units associated with higher mortality?
- Can a baseline Logistic Regression model predict in-hospital mortality using patient and ICU stay-level features?

## Data Source & Privacy Note

This project uses the MIMIC-IV Clinical Database Demo, a small publicly available demo version of the MIMIC-IV clinical database.

MIMIC-IV contains deidentified electronic health record data from hospital and ICU patients. This project uses only the demo dataset for learning and portfolio purposes.

Raw MIMIC-IV data is not included in this repository. The repository includes code, visualizations, and documentation, but not raw clinical data files.

The target variable for this project is hospital_expire_flag.

- 0 = patient did not die during the hospital admission
- 1 = patient died during the hospital admission

> Because this project uses healthcare data, privacy and responsible data use are part of the project design.

## Project Structure

text icu-patient-risk-modeling/ ├── README.md ├── requirements.txt ├── .gitignore ├── notebooks/ │   └── icu-patient-risk-modeling.ipynb ├── visuals/ │   ├── mortality_distribution.png │   ├── mortality_by_age_group.png │   ├── icu_los_by_mortality.png │   ├── mortality_by_admission_type.png │   ├── confusion_matrix.png │   ├── roc_curve.png │   └── logistic_regression_coefficients.png └── data/     └── README.md 

## Methodology

This project uses three core MIMIC-IV Demo tables:

- patients: patient-level demographic information
- admissions: hospital admission information and mortality outcome
- icustays: ICU stay information

These tables were merged to create an ICU stay-level dataset, where each row represents one ICU stay.

Version 1 uses the following features:

- age
- icu_los
- gender
- admission_type
- insurance
- first_careunit

The baseline model uses Logistic Regression with class_weight="balanced" to account for class imbalance between survival and mortality cases.

> The purpose of Version 1 is to build a clean and reproducible baseline pipeline before adding lab results, vital signs, and more advanced clinical features.

## Visualizations

### Mortality Distribution

This chart shows the distribution of survival and mortality cases in the MIMIC-IV Demo ICU stay-level dataset.

Mortality Distribution

### Mortality by Age Group

This chart compares in-hospital mortality rates across patient age groups.

Mortality by Age Group

### ICU Length of Stay by Mortality Outcome

This chart compares ICU length of stay between patients who survived and patients who died during the hospital admission.

ICU Length of Stay by Mortality Outcome

### Mortality by Admission Type

This chart compares mortality rates across different hospital admission types.

Mortality by Admission Type

### Confusion Matrix

This chart shows how the baseline Logistic Regression model classified survival and mortality cases in the test set.

Confusion Matrix

### ROC Curve

This chart shows the model's ability to separate survival and mortality cases across different classification thresholds.

ROC Curve

### Logistic Regression Coefficients

This chart shows which features had the strongest association with the model's predicted mortality risk.

Logistic Regression Coefficients

## Key Findings

- This project created an ICU stay-level dataset by merging patient, admission, and ICU stay records from MIMIC-IV Demo.
- The final Version 1 dataset contained 140 ICU stays, including 120 survival cases and 20 mortality cases.
- Mortality cases represented about 14.29% of the dataset, showing clear class imbalance.
- Mortality rates were highest among patients aged 71–90 and 51–70 in this demo sample.
- Patients who died had a higher median ICU length of stay, about 4.27 days, compared with about 2.05 days for patients who survived.
- URGENT and DIRECT EMER. admissions showed higher mortality rates than elective or surgical same-day admissions in this sample.
- A baseline Logistic Regression model with class_weight="balanced" was built to predict in-hospital mortality.
- The model achieved 0.86 accuracy and 0.948 ROC-AUC on the test set.
- The model identified all mortality cases in the test set, but mortality precision was 0.50, showing a trade-off between identifying high-risk patients and creating false positives.
- The model provides a prototype risk modeling pipeline rather than a clinical decision-making tool.

> The main value of this version is building a clean, reproducible healthcare modeling pipeline from raw EHR-style tables.

## Limitations

This project uses the MIMIC-IV Demo dataset, which contains a small subset of patients. Because of the small sample size, model performance should be interpreted carefully.

The test set contained only 28 ICU stays, including 4 mortality cases. This means evaluation metrics such as recall, precision, and ROC-AUC may change substantially with a larger dataset.

This version uses only basic demographic, admission, and ICU stay-level features. It does not yet include:

- Lab results
- Vital signs
- Diagnoses
- Medications
- First 24-hour clinical features

Because this model uses limited features, it should be viewed as a baseline prototype rather than a complete clinical risk model.

The model should not be interpreted as clinical evidence or used for medical decision-making.

## Data Leakage Note

This Version 1 model uses only demographic, admission, and ICU stay-level summary features.

Future versions should carefully limit lab results and vital signs to information available within the first 24 hours of ICU admission.

Using information recorded after the prediction window could create data leakage, making model performance look better than it would be in real clinical use.

> Preventing data leakage is especially important in healthcare risk modeling because feature timing affects whether a model is realistic.

## Future Improvements

Future versions of this project could include:

- Lab results from labevents
- Vital signs from chartevents
- First 24-hour clinical feature engineering
- Diagnosis-based comorbidity features
- Medication and procedure features
- Random Forest or Gradient Boosting models
- SHAP-based model interpretation
- More robust validation using the full MIMIC-IV dataset after completing credentialed access requirements

The next major improvement would be adding first-24-hour labs and vital signs while carefully avoiding data leakage.

## How to Run

1. Clone this repository.

bash git clone https://github.com/Dongwoon1d/icu-patient-risk-modeling.git cd icu-patient-risk-modeling 

2. Install the required packages.

bash pip install -r requirements.txt 

3. Download the MIMIC-IV Clinical Database Demo from PhysioNet.

Place the downloaded dataset in the following local path:

text data/mimic-iv-clinical-database-demo/ 

4. Open the notebook.

text notebooks/icu-patient-risk-modeling.ipynb 

5. Run all cells in the notebook.

The notebook will create the ICU stay-level dataset, generate visualizations, train a baseline Logistic Regression model, and save local processed outputs.

## Tools Used

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- JupyterLab
- MIMIC-IV Clinical Database Demo