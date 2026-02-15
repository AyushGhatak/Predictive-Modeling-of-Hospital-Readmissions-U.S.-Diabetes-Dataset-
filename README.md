# Predictive-Modeling-of-Hospital-Readmissions-U.S.-Diabetes-Dataset-
(U.S. Diabetes Dataset – 30-Day Readmission Prediction)

## Project Overview
Hospital readmissions within 30 days significantly impact healthcare costs and hospital reimbursement policies in the United States. Under the Hospital Readmissions Reduction Program (HRRP), hospitals face financial penalties for excessive readmissions.

This project builds predictive models to identify high-risk diabetic patients likely to be readmitted within 30 days, using clinical, demographic, and treatment-related features.

The goal is to:
* Predict 30-day readmission
* Identify key risk factors
* Provide actionable recommendations for hospitals

## Dataset
The dataset used is the U.S. Diabetes 130-Hospitals Dataset, containing over 100,000 hospital encounters of diabetic patients.

**Feature Categories**

-> Clinical Features
* num_lab_procedures
* num_procedures
* num_medications
* number_outpatient
* number_emergency
* number_inpatient
* number_diagnoses

-> Treatment-Related Features
* admission_type_id
* discharge_disposition_id
* admission_source_id
* time_in_hospital
* change
* diabetesMed
24 medication-related features (metformin to metformin.pioglitazone)

-> Demographic Features
* race
* gender
* age
* weight

## Objective
To determine:

**Which features best predict whether a diabetic patient will be readmitted within 30 days?**

This is formulated as a binary classification problem: <br>
0 → No readmission within 30 days <br>
1 → Readmission within 30 days

## Exploratory Data Analysis
**Overview** 

Exploratory Data Analysis was conducted using:
* Python (Pandas, Matplotlib, Seaborn) for statistical exploration.
* Power BI for interactive dashboard development and demographic segmentation. <br>
The objective was to uncover patterns influencing 30-day hospital readmission among diabetic patients and identify high-risk segments before model building.

**-> Correlation Heatmap**

Key Findings: 
* time_in_hospital and num_medications show a strong positive correlation (~0.6)
* num_lab_procedures moderately correlates with num_medications (~0.34)
* num_lab_procedures has a weak negative correlation with number_inpatient (-0.17)
* Readmission itself shows very weak linear correlation with individual variables:
    * time_in_hospital (~0.048)
    * num_lab_procedures (~0.052)
    * num_medications (~0.037)
    * number_inpatient (~0.04)

Interpretation: 
* No single feature linearly explains readmission.
* Readmission is likely driven by complex, non-linear interactions. <br>
This justifies the use of ensemble models like Random Forest and XGBoost rather than relying solely on logistic regression.

**-> Readmission Count by Age**

Observations:
* Readmission counts increase significantly from age 45 onwards.
* Peak readmission appears in the 65–75 age group.
* Very low readmission among younger groups (5–35).
* Slight decline in extreme elderly (85+), likely due to smaller sample size.

Interpretation:
* Older diabetic patients have higher readmission vulnerability.
* Age acts as a risk amplifier, likely interacting with:
    * Number of medications
    * Inpatient history
    * Comorbidities <br>
This supports including age as an important predictive variable.

**-> Readmission by Gender & Race**

Race-Based Observations:
* Caucasian patients show the highest absolute readmission count (due to larger representation in dataset).
* African American patients also show substantial readmission counts.
* Other racial groups have lower absolute counts.

Gender-Based Observations:
* Readmission counts are relatively balanced across male and female.
* Slight variation exists but gender alone is not a dominant predictor.

Interpretation: 

Demographic variables alone are not strong predictors. However, they may interact with healthcare access, treatment patterns, and socioeconomic factors. These variables are useful when combined with clinical features.

**-> Readmission by Weight**

Observations:
* Highest readmission counts observed in:
   * 75–100 lbs range
   * 50–75 lbs range
* Extremely high weight ranges show lower counts (likely fewer observations).
* Weight distribution was skewed with significant missing values.

Interpretation:
* Weight alone does not strongly determine readmission. It likely interacts with:
    * Diabetes severity
    * Medication count
    * Hospital stay duration
* Missing values were handled via **cluster-based median imputation**, preserving distribution characteristics.

**-> Top 5 Medications by Readmission Rate**

Observations:
* Repaglinide (Up) → Highest readmission proportion (~54%)
* Glyburide (Up) → Second highest (~27%)
* Insulin variations contribute smaller proportions
* Medication adjustments (Up/Down/Steady) appear influential

Interpretation:
* Medication escalation (“Up”) is strongly associated with readmission. This may indicate:
    * Poor glycemic control
    * Worsening condition
    * Treatment instability
* Medication change is a clinically meaningful predictor.

## Data Cleaning & Preprocessing

-> Columns Removed 

The following columns were removed due to irrelevance or excessive missing values:<br>
* encounter_id
* patient_nbr
* payer_code
* medical_specialty
* max_glu_serum
* A1Cresult

-> Handling Missing Values (Innovative Approach) 

The weight column contained significant missing values but was important for analysis. <br>
Instead of using KNN (not ideal due to high dimensionality), we clustered patients based on similar demographic features. Imputed missing weight values using the median weight of the respective cluster. <br>
This preserved distribution characteristics while avoiding overfitting.

## Models Implemented
We trained and evaluated:
* Logistic Regression
* Random Forest
* XGBoost

Evaluation Metrics:
* Accuracy
* ROC-AUC Score
* Confusion Matrix

## Results
| Model | Accuracy | ROC-AUC |
| :---: | :---: | :---: |
| **Logistic Regression** | Comparable | Moderate |
| **Random Forest** | Comparable | Moderate |
| **XGBoost** | Comparable | **Highest** |

**Why XGBoost Performed Best?** 
* Captures non-linear relationships
* Handles high-dimensional data well
* Uses L1 & L2 regularization
* Robust against overfitting

**Key Predictors of Readmission (according to the feature importances by XGBoost)**

Important features included:
* time_in_hospital
* number_inpatient
* num_medications
* discharge_disposition_id
* number_emergency
* change
* diabetesMed

These variables significantly influenced readmission probability.

## Patient Segmentation (Clustering)
We segmented diabetic patients into clusters based on:
* Age
* Gender
* Race
* Time in hospital
* Lab procedures
* Medications
* Inpatient/outpatient visits
* Emergency visits
* Medication changes

**Purpose:**
* Identify high-risk subgroups
* Personalize post-discharge strategies
* Improve resource allocation

## Actionable Insights for Hospitals
Based on modeling and clustering:
* Implement targeted post-discharge follow-ups
* Improve discharge planning for high-risk groups
* Strengthen outpatient & telehealth services
* Monitor medication adherence
* Improve care coordination
* Educate patients on diabetes self-management
* Optimize ER triage systems

## Tech Stack
* Python
* Pandas
* NumPy
* Scikit-learn
* XGBoost
* Matplotlib / Seaborn

## Repository Structure
├── Dataset/ <br>
│   └── Q1_material_diabetic_data_final.csv <br>
├── EDA - Visualizations <br>
│   └── Correlation Heatmap (correlation between readmission and key factors).png <br>
│   └── Re-admission counts influenced by age.png <br>
│   └── Re-admission counts influenced by gender, race.png <br>
│   └── Re-admission counts influenced by weights.png <br>
│   └── Top 5 medications by readmission rate.png <br>
├── notebooks/ <br>
│   └── Data Cleaning and Modeling.ipynb <br>
├── Results/ <br>
│   └── model summary.png <br>
│   └── feature importances_XGBoost.png <br>
│   └── cluster summary.png <br>
│   └── cluster summary (2).png <br>
├── README.md

## Business Impact
This model can help hospitals:
* Reduce financial penalties under HRRP
* Improve patient care quality
* Optimize hospital resource utilization
* Move toward data-driven healthcare decision-making
