# Diabetes Patient Readmission Analysis 🏥

## Project Overview
This project focuses on analyzing clinical data for diabetic patients to identify key factors leading to hospital readmissions within 30 days. By transforming raw healthcare data into actionable insights, we aim to help hospital administrators reduce costs and improve patient care quality.

## 👥 Team Contributions (Contribution Matrix)
The following team members executed the data engineering and analysis:

| Team Member | Primary Responsibility | Key Tasks |
| :--- | :--- | :--- |
| **Anushka** | Data Quality & Binary Logic | Mode imputation (Race), MaxGlu logic, Readmission binary mapping. |
| **Divya** | Feature Engineering & Documentation | ICD-9 Diagnosis grouping, A1C test logic, Medical status mapping. |
| **Mitul** | Data Cleaning & Reduction | Gender cleaning, Column reduction (21 columns removed), Record deduplication. |
| **Dhruv** | Data Preprocessing & Randomization | Handling missing values (Weight, Payer Code, Medical Specialty) and **dataset randomization**. |
| **Daniel** | Clinical Logic | Discharge disposition mapping and hospice logic. |

---

## 🛠 Data Preprocessing & Cleaning
The raw dataset underwent a rigorous "Data Approval" gate process to ensure high integrity.

### 1. Handling Missing & Invalid Data
* **Weight & Payer Code**: Dropped due to high missingness (>40k-98k nulls).
* **Race**: Imputed missing values using the mode (**Caucasian**).
* **Medical Specialty**: Replaced unknown values (`?`) with **"Missing"**.
* **Gender**: Removed "Unknown/Invalid" rows to maintain demographic accuracy.

### 2. Feature Selection & Reduction
* **Irrelevant Columns**: Removed 21 columns including `diag_2`, and `diag_3` to focus on primary triggers.
* **Medication Cleanup**: Targeted 24 specific medication columns (e.g., Repaglinide, Nateglinide, Acarbose) for removal to simplify the medication change analysis.

### 3. Record Deduplication & Sampling
* **Single Encounter Rule**: Data was sorted by `patient_nbr` and `encounter_id`. Only the **first encounter** for each unique patient was kept to avoid bias from multiple visits by the same individual.
* **Randomized Sampling**: A randomized **14,117-row sample** was generated for the final analysis to ensure a representative subset. 
* **Reproducibility**: The randomization and preprocessing logic can be reviewed in this [Google Colab Notebook](https://colab.research.google.com/drive/1gCpRNL8pt-mFQt_GnxZ_Dkaw_WaMZ91C?usp=sharing).

---

## 🧬 Feature Engineering (Business Translation)
We created new logical features to answer specific clinical questions:

* **Primary Condition (ICD-9 Grouping)**: 
    * *Diabetes*: ICD-9 250.xx
    * *Heart/Circulatory*: 390–459, 785
    * *Respiratory*: 460–519, 786
    * *Other*: Digestive, Injury/Trauma, etc.
* **Clinical Indicators (Binary)**:
    * `Readmitted_Binary`: 1 if readmitted <30 days, 0 otherwise.
    * `A1C_None`: 1 if the A1C test was not performed (Process Failure).
    * `A1C_High`: 1 if result was >7 or >8 (Uncontrolled Diabetes).
    * `MaxGlu_High`: 1 if result >200 or >300.

