Smoking and Health Analysis Dashboard

Domain: Healthcare Analytics | Tool: Microsoft Power BI (DAX) | Organization: Sapphire IQ

An interactive-dashboard project built on patient-level data (10,000 patients, 15 fields). It tracks key patient KPIs, smoking patterns, health conditions by organ, and trends across age groups, gender and region.

Disclaimer: This project is for educational and exploratory analysis only. It does not establish medical diagnoses or prove that smoking causes any health condition.

Dataset

Smoking_Health_Analysis.csv has 10,000 rows and 15 columns, with no missing values and no duplicate patient IDs.

Column	Description
Patient_ID	Unique patient identifier
Age, Gender, Region	Demographics
Diagnosis_Date	Date of diagnosis (2021-01-01 to 2026-09-30)
Smoking_Status	Current Smoker, Former Smoker, Never Smoked
Cigarettes_Per_Day, Years_Smoking	Smoking intensity and duration
Diagnosed_Organ, Health_Condition	Recorded organ category and condition
Total_Cholesterol_mg_dL	Total cholesterol
Systolic_BP_mmHg, Diastolic_BP_mmHg	Blood pressure
BMI, Resting_Heart_Rate_bpm	Other indicators
Project objectives
KPIs: total patients, current smokers, patients with a recorded organ category, patients with a recorded health condition.
DAX calculated columns: Age Group and BP Risk Category (plus Smoking Exposure Level for Objective 4.2).
Smoking patterns and health indicators: average cigarettes/day by status, organ-wise condition distribution, smoking status distribution, average cholesterol by BP risk category.
Demographics and health patterns: current smokers by age group, recorded conditions by smoking exposure level.
Repository structure
.
├── data/
│   ├── Smoking_Health_Analysis.csv              # original data
│   └── 02_Smoking_Health_Enriched_Dataset.csv   # original + Age Group, BP Risk, Exposure Level
├── dax/
│   ├── 01_Objective1_KPI_Measures.dax
│   ├── 02_Objective2_Calculated_Columns.dax
│   ├── 03_Objective3_Analysis_Measures.dax
│   └── 04_Objective4_Analysis_Measures.dax
├── results/                                     # result tables (CSV), one per analysis
│   ├── 01_Objective1_KPIs.csv
│   ├── 03a_Avg_Cigarettes_by_Smoking_Status.csv
│   ├── 03b_Organ_vs_Health_Condition_Counts.csv
│   ├── 03b_Organ_Condition_Distribution_Long.csv
│   ├── 03c_Smoking_Status_Distribution.csv
│   ├── 03d_Avg_Cholesterol_by_BP_Risk.csv
│   ├── 04a_Current_Smokers_by_Age_Group.csv
│   ├── 04b_Exposure_Level_Summary.csv
│   └── 04b_Exposure_Level_vs_Health_Condition_Counts.csv
├── charts/                                      # chart previews (PNG)
│   ├── 03a_chart_avg_cigarettes.png
│   ├── 03b_chart_organ_condition.png
│   ├── 03c_chart_smoking_status_donut.png
│   ├── 03d_chart_cholesterol_by_bp.png
│   ├── 04a_chart_smokers_by_age.png
│   └── 04b_chart_exposure_conditions.png
└── README.md
How to use in Power BI Desktop
Get Data > Text/CSV, load Smoking_Health_Analysis.csv (table name Smoking_Health_Analysis) and set Diagnosis_Date to Date.
Add the calculated columns from dax/02_Objective2_Calculated_Columns.dax (Table tools > New column). Set each text column's Sort by column to its matching _Sort column. (Or load the enriched CSV, which already contains them.)
Add the measures from the other .dax files (Modeling > New measure).
Build the visuals and add slicers for Gender, Region, Age Group and Smoking_Status:
Visual	Type	Fields
KPI cards (x4)	Card	Total Patients, Total Current Smokers, Patients With Recorded Organ Category, Patients With Recorded Health Condition
Avg cigarettes/day	Clustered column	Smoking_Status, Avg Cigarettes Per Day
Organ vs condition	100% stacked bar	Diagnosed_Organ, Health_Condition, Patient Count
Smoking status	Donut	Smoking_Status, Patient Count
Cholesterol vs BP	Clustered column	BP Risk Category, Avg Cholesterol
Smokers by age	Clustered column	Age Group, Total Current Smokers
Conditions by exposure	Stacked column	Smoking Exposure Level, Health_Condition, Recorded Condition Count
Definitions
Age Group: 18-29, 30-44, 45-59, 60+
BP Risk Category: High if systolic >= 140 or diastolic >= 90; Elevated if systolic 120-139 or diastolic 80-89; Lower Range otherwise. These are simplified screening buckets, not clinical diagnoses.
Smoking Exposure Level: based on years smoked: No Exposure (0), Low (1-10), Moderate (11-25), High (26+). Pack-years is not used because former smokers are recorded as 0 cigarettes/day.
Key results
KPI	Value
Total patients	10,000
Current smokers	3,015 (30.2%)
Recorded organ category	7,227 (72.3%)
Recorded health condition	5,772 (57.7%)
Smoking status: Never 42.6%, Current 30.2%, Former 27.2%.
Cigarettes/day: current smokers average 17.1; former and never smokers are recorded as 0.
Cholesterol vs BP risk: 195.4 (Lower Range), 197.2 (Elevated), 197.9 (High) mg/dL, a very small spread.
Current smokers by age group: 508 / 668 / 715 / 1,124. The share of each age group that smokes is similar (28.6%-31.4%).
Recorded condition by exposure: 58.4% (No Exposure), 58.3% (Low), 57.7% (Moderate), 54.8% (High).
Notes and limitations
Results are associations within one dataset, not causal findings. Patterns are weak and should not be used to draw health conclusions.
1,237 patients have a recorded condition but no recorded organ (for example hypertension or diabetes), and 2,692 have an organ recorded but no diagnosed condition, so the organ and condition KPIs are not interchangeable.
The DAX logic was verified against an equivalent pandas calculation but should be confirmed against the card values in Power BI.
