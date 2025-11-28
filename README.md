# 🏥 Health Insurance Claims Analysis  
A complete data analytics pipeline using **Python**, **SQL Server**, and **Power BI**.  
This project transforms raw health insurance claim data into a clean, structured star-schema model and delivers actionable business insights through interactive dashboards.

---

## 📂 Project Overview
Insurance companies rely on accurate claim analysis to reduce fraud, understand provider patterns, and assess financial performance.  
This project simulates a real-world BI workflow:

✔️ **Python** → Exploratory Data Analysis and data cleaning  
✔️ **SQL Server** → Data modeling (Star Schema), surrogate keys, fact/dimension tables  
✔️ **Power BI** → Interactive dashboards and DAX measures  

---

# 🧪 1. Exploratory Data Analysis (Python)

### 🔍 EDA Steps
- Summary statistics  
- Missing value analysis  
- Duplicates detection  
- Outlier detection  
- Claim amount distributions  
- Categorical distributions (Gender, Specialty, Status…)  
- Correlation heatmaps  
- Trend analysis over dates  

### 🧼 Data Cleaning Performed
- Dropping exact duplicate claim records  
- Fixing inconsistent formatting (cities, genders, submission methods)  
- Converting dates to datetime format  
- Casting numeric columns  
- Handling nulls depending on business logic  
- Exporting cleaned dataset → `clean_health_insurance.csv`

### 🐍 Tech Stack
- pandas  
- numpy  
- matplotlib / seaborn (if used)  
- jupyter notebook  

All code is included in the `python/` directory.

---

# 🗄️ 2. SQL Data Modeling

### ▶️ Steps in SQL Server
1. Imported cleaned CSV using SSMS Import Wizard  
2. Created **Dim tables** (Patient, Provider, ClaimType, SubmissionMethod, Date)  
3. Built **FactClaim** with surrogate keys  
4. Loaded data using SQL insert scripts  
5. Applied primary & foreign key constraints  
6. Removed duplicates and validated referential integrity  

### ✔ Sample SQL Included
- Table creation scripts  
- Mapping logic  
- Deduplication script  
- Date dimension generation  
- Fact population with joins  

---

# ⭐ Star Schema Architecture

       DimPatient
           |
       DimProvider
           |
        DimDate
           |
       FactClaim
           |
      DimClaimType
           |
  DimSubmissionMethod

  
### **FactClaim**
- ClaimID  
- PatientID  
- ProviderID  
- ClaimAmount  
- ClaimStatus  
- ClaimTypeID  
- SubmissionMethodID  
- DateKey  
- DiagnosisCode *(DD)*  
- ProcedureCode *(DD)*  

(*DD = Degenerate Dimension*)

---

# 📊 3. Power BI Dashboards

3 professional dashboards built:

---

## **📌 Dashboard 1 — Executive Overview**
- Total Claims  
- Total Claim Amount  
- Avg Claim per Patient  
- Approval Rate  
- Claims by City (Filled Map)  
- Top 5 Providers  
- Claims by Status  
- Claims by Submission Method  

---

## **📌 Dashboard 2 — Provider & Specialty Insights**
- Claims by Provider  
- Claims by Provider Specialty  
- Claims Trend by Month  
- Distinct Providers  
- Distinct Specialties  
- Top Performing Cities  

---

## **📌 Dashboard 3 — Financial Performance**
- Claim Amount by Type  
- High-value vs Low-value claims  
- Submission channel financial analysis  
- Year-over-year trends (YoY)  
- Monthly Claim Amount Trend  

---

# 🔢 Key DAX Measures

```DAX
Total Claims = COUNT(FactClaim[ClaimID])

Total Claim Amount = SUM(FactClaim[ClaimAmount])

Total Providers = DISTINCTCOUNT(DimProvider[ProviderID])

Total Specialties = DISTINCTCOUNT(DimProvider[ProviderSpecialty])

Total Locations = DISTINCTCOUNT(DimProvider[ProviderLocation])

Approval Rate = 
    DIVIDE(
        CALCULATE(COUNT(FactClaim[ClaimID]), FactClaim[ClaimStatus] = "Approved"),
        COUNT(FactClaim[ClaimID])
    )

Avg Claim per Patient =
    DIVIDE(
        SUM(FactClaim[ClaimAmount]),
        DISTINCTCOUNT(FactClaim[PatientID])
    )

├── python/
│   ├── EDA.ipynb
│   ├── cleaning.py
│   └── Health_Insurance_dataset.csv
│
├── sql/
│   ├── 01_create_dimensions.sql
│   ├── 02_create_factclaim.sql
│   ├── 03_insert_dimensions.sql
│   ├── 04_insert_factclaim.sql
│   └── 05_remove_duplicates.sql
│
├── powerbi/
│   ├── Health_Insurance.pbix
│   └── dashboards_screenshots/
│
└── README.md
