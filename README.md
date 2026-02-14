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

Feature Categories

Clinical Features
* num_lab_procedures
* num_procedures
* num_medications
* number_outpatient
* number_emergency
* number_inpatient
* number_diagnoses

Treatment-Related Features
* admission_type_id
* discharge_disposition_id
* admission_source_id
* time_in_hospital
* change
* diabetesMed
24 medication-related features (metformin to metformin.pioglitazone)

Demographic Features
* race
* gender
* age
* weight

## Objective
To determine:

Which features best predict whether a diabetic patient will be readmitted within 30 days?

This is formulated as a binary classification problem:

0 → No readmission within 30 days
1 → Readmission within 30 days

