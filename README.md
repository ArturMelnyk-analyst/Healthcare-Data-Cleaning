🩺 Healthcare Provider Fraud Detection – Data Cleaning Project
Author: Artur Melnyk
Dataset: Kaggle - Medicare Provider Fraud Detection
________________________________________
📌 Project Overview
This project focuses on building a clean and structurally sound foundation for detecting fraud in Medicare healthcare claims. The work includes:
•	Cleaning and standardizing eight interrelated raw datasets
•	Ensuring referential integrity across claims and beneficiary records
•	Implementing outlier handling that preserves training data size
•	Performing type conversion, imputation, and feature engineering
•	Preparing data for downstream modeling or exploratory analysis
________________________________________
📁 Datasets Used
The following raw CSV datasets were processed:
•	Train and Test main tables
•	Train_Beneficiary and Test_Beneficiary
•	Train_Inpatient and Test_Inpatient
•	Train_Outpatient and Test_Outpatient
________________________________________
🔧 Key Cleaning Operations
✅ Missing Value Handling
•	Dates parsed as datetime with coercion
•	Numerical fields imputed using the median
•	Categorical fields imputed using the mode
•	Sparse but relevant columns preserved for schema alignment
✅ Outlier Handling
Initial IQR filtering led to significant row loss. This was corrected using winsorization, which caps extreme values while maintaining the full dataset size.
python
CopyEdit
def winsorize_column(series):
    Q1 = series.quantile(0.25)
    Q3 = series.quantile(0.75)
    IQR = Q3 - Q1
    return series.clip(Q1 - 1.5 * IQR, Q3 + 1.5 * IQR)
✅ Data Type Conversion
•	Dates: pd.to_datetime(..., errors='coerce')
•	Categories: .astype('category') for memory efficiency
✅ Feature Engineering
•	AgeAtDeathOrLastClaim: Derived from DOB and DOD fields
________________________________________
🔍 Data Integrity & Structure Checks
•	Confirmed BeneID alignment across all claim and beneficiary files
•	Verified train/test schema consistency (except for PotentialFraud target)
•	Performed .info() and .isnull().sum() for structural validation
📈 A relationship diagram illustrates how datasets are connected through BeneID.
________________________________________
⚠️ Challenges Faced
•	Over-aggressive row deletion during initial outlier filtering
•	Retention of extremely sparse fields (e.g. ClmProcedureCode_6) for schema stability
•	Preserving row counts while cleaning for realistic model training
________________________________________
✅ Final Output
•	Cleaned, validated, and aligned dataset with 0 mismatched BeneIDs
•	Ready for modeling, visualization, and statistical analysis
________________________________________
📌 Recommendations for Next Steps
•	Apply label or one-hot encoding for categorical variables
•	Analyze and potentially drop very sparse columns
•	Engineer provider-level aggregates (e.g. claim counts)
•	Explore class imbalance handling for PotentialFraud

