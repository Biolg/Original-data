# README — NHANES 2011–2016 dataset for “Blood Heavy Metal Mixtures and Colorectal Cancer”

## 1) Repository overview

This repository contains the de-identified analytic dataset and metadata used to examine associations between whole-blood metals and prevalent colorectal cancer (CRC) in U.S. adults using NHANES 2011–2016. The project integrates survey-weighted regression and mixture methods (WQS, qgcomp, BKMR).

**Primary data file:** `Original_data.csv`
 **Population:** NHANES participants ≥20 years with valid blood metal measurements and covariates, pooled across 2011–2012, 2013–2014, and 2015–2016 cycles.

> **Note:** The first column `X` is an export artifact and should be dropped.

------

## 2) Data provenance, cohort selection, and ethics

- **Source:** National Health and Nutrition Examination Survey (NHANES), CDC/NCHS (publicly available, de-identified).
- **Cycles pooled:** 2011–2012, 2013–2014, 2015–2016.
- **CRC ascertainment:** Self-reported physician diagnosis from the Medical Conditions Questionnaire:
  - **MCQ240g** (“Age when first told you had colon cancer”)
  - **MCQ240v** (“Age when first told you had rectal cancer”)
     Participants answering “yes” to either were classified as **CRC = 1**; others **CRC = 0**.
- **Ethics:** NHANES protocols were approved by the NCHS Ethics Review Board; this secondary analysis uses public, de-identified data and does not involve identifiable information.

------

## 3) File list

- `Original_data.csv` — analysis-ready dataset (one row per participant).
- `codebook.csv` *(optional)* — extended coding/labels for categorical variables.
- `README.md` — this file.

------

## 4) Data dictionary (column order matches the CSV)

> Units, types, and brief definitions are listed below. Detailed operational definitions (e.g., category cut-points) should match your Supplementary Table 2.

- `X` — export index (**ignore / drop**).
- `seqn` — NHANES respondent ID (numeric; unique).
- `Year` — NHANES cycle (factor; “2011–2012”, “2013–2014”, “2015–2016”).
- `sdmvpsu` — masked primary sampling unit (integer).
- `sdmvstra` — masked sampling strata (integer).
- `wtmec2yr` — 2-year MEC exam weight (numeric); use **6-year weight = `wtmec2yr / 3`** for pooled analyses.
- `Age` — years (numeric).
- `Sex` — sex (categorical; NHANES coding; see codebook).
- `Race` — race/ethnicity (categorical; original or collapsed; see codebook).
- `Marital` — marital status (categorical).
- `Poverty` — poverty-to-income ratio (PIR; numeric or categorized).
- `Education` — education level (categorical).
- `alcohol.user` — legacy alcohol indicator (derivation variable).
- `Drinking` — analytic alcohol category (e.g., none/former/current).
- `smoke` — legacy smoking indicator (derivation variable).
- `Smoking` — analytic smoking category (e.g., never/former/current).
- `CKD` — chronic kidney disease (binary; definition per Supplementary Table 2).
- `DM` — diabetes mellitus (binary; definition per Supplementary Table 2).
- `Hypertension` — hypertension (binary; definition per Supplementary Table 2).
- `BMI` — body mass index, kg/m² (numeric).
- `WC` — waist circumference, cm (numeric).
- `ALB` — serum albumin, g/dL (numeric).
- `CRE` — serum creatinine, mg/dL (numeric).
- `TC` — total cholesterol, mg/dL (numeric).
- `LDL` — LDL cholesterol, mg/dL (numeric).
- `Cd` — whole-blood cadmium, **** (numeric).
- `Pb` — whole-blood lead, **** (numeric).
- `Hg` — whole-blood total mercury, **** (numeric).
- `Mn` — whole-blood manganese, **** (numeric).
- `Se` — whole-blood selenium, **** (numeric).
- `Outcome` — prevalent CRC (binary; 1 = yes (colon or rectal), 0 = no).

**Handling below LOD:** For metals, values <LOD were imputed as **LOD/√2** (see Supplementary Table 1 for LODs and <LOD proportions).

------

## 5) Missing data

- Missing values are encoded as blank/`NA`.
- Any additional imputation or exclusions should be described in the manuscript or a separate analysis note (this CSV reflects the variables as analyzed).

------

## 6) Survey design and weights (critical for replication)

To obtain nationally representative estimates and valid variances in pooled analyses:

- **Strata:** `sdmvstra`
- **PSU:** `sdmvpsu`
- **Weight:** combined **6-year MEC weight = `wtmec2yr / 3`**
- Apply NHANES analytic guidelines for combined cycles; specify strata/PSU/weights in all descriptive and regression analyses.