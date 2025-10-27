# Hospital Readmission and Recovery Trends Dashboard

A Power BI dashboard analyzing hospital patient data. This project focuses on readmission rates, recovery trends, patient satisfaction, average length of stay (ALOS), and key financial KPIs. Interactive visuals track performance by procedure, condition, and department.

## Dashboard Preview
![Dashboard Preview](Hospital%20Data-%20Analysis.png)

---

## Project Overview
This project visualizes hospital data to provide insights into patient readmission, recovery trends, financial revenue, and quality of care metrics. The dashboard allows for interactive filtering by gender, condition, and procedure to help hospital administrators identify problem areas and opportunities for improvement.

## Key Visuals & KPIs
* **KPI Cards:** Total Patients, Total Revenue, Total Readmission %, Average Length of Stay (ALOS), and Average Satisfaction Score.
* **Line Chart:** A trend analysis of `Total Patients by Month`.
* **Bar Charts:**
    * `Top 5 Procedures by Average Length of Stay` (using a Top N filter).
    * `Average Satisfaction by Department`.
* **Donut Chart:** A breakdown of `Patients by Age Category`.
* **Slicers:** Interactive slicers for `Gender`, `Condition`, and `Procedure`.

---

## Key DAX Measures
Several DAX measures were created to power the KPIs and visuals. The core formulas are consolidated below:

*(Note: Table name is based on your file `hospital_patient_cleaned.xlsx - Sheet1.csv`)*

```dax
Total Patients = 
DISTINCTCOUNT('hospital_patient_cleaned'[Patient ID])

Total Revenue = 
SUM('hospital_patient_cleaned'[Revenue])

Average Length of Stay = 
AVERAGE('hospital_patient_cleaned'[Length of Stay])

Total Readmissions = 
CALCULATE(
    COUNTROWS('hospital_patient_cleaned'),
    'hospital_patient_cleaned'[Readmission] = "Yes"
)

Total Readmission % = 
DIVIDE( [Total Readmissions], [Total Patients], 0 )

Average Satisfaction = 
AVERAGE('hospital_patient_cleaned'[Satisfaction])

Satisfaction with Scale = 
FORMAT( [Average Satisfaction], "0.0" ) & " / 5.0"
