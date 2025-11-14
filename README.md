# 🔍 Scaler — Learner Profiling & Clustering Project (K-Means & Manual Clusters)

## 🚀 Project Overview
This project profiles Scaler learners to identify meaningful clusters of employees based on **company**, **job position**, **CTC**, and **experience**. The aim is to produce groupings (manual + unsupervised) that reveal high/low performers, tiers across companies, and role-specific insights to drive hiring, placement, and learning recommendations.

---

## ⭐ Key Highlights
- Performed **data cleaning & regex normalization** on company names and job titles.  
- Created **manual clusters** (Designation / Class / Tier) using business rules derived from company-level CTC summaries.  
- Applied **unsupervised clustering** (Elbow + K-Means, Hierarchical) to validate and refine manual segments.  
- Generated actionable lists: Top/Bottom employees per company & role, Top companies by CTC, and Role rankings.  
- Produced business recommendations for talent engagement, upskilling, and placement prioritization.

---

## 🧠 Techniques & Concepts Used
- **Data Cleaning & Preparation**
  - Regex to remove special characters from company/job names.
  - Duplicate detection & removal, missing-value imputation (KNN / mean).
  - Feature creation: `Years_of_Experience` = (current_year − orgyear), `CTC_updated_year` handling.

- **Manual Clustering**
  - Aggregation per `(Company, Job_position, Years_of_Experience)` to compute CTC statistics (mean, median, count, min, max).
  - Flags:
    - `Designation` — relative to peers in same (Company, Job_position, YOE) → values `[1,2,3]` (1 = above avg).
    - `Class` — role-level flag within company → values `[1,2,3]`.
    - `Tier` — company-level flag based on overall CTC distribution → values `[1,2,3]`.

- **Unsupervised Clustering**
  - Encoding: Label / One-hot encoding for categorical vars.
  - Standardization (StandardScaler / RobustScaler).
  - Clustering Tendency → Elbow method & silhouette analysis.
  - K-Means clustering & Hierarchical clustering for cross-validation of groups.

---

## 🛠 Workflow Methodology
1. **Import & Initial EDA**  
   - Inspect shape, dtypes, missing values, unique email hashes and frequencies.

2. **Cleaning & Feature Engineering**  
   - Regex cleanup of `Company_hash` labels (where applicable), compute `Years_of_Experience`, convert categorical dtypes.
   - Handle missing values via KNN or mean imputation depending on variable.

3. **Manual Clustering & Flags**  
   - Aggregate CTC by `(Company, Job_position, Years_of_Experience)` → compute 5-point summary.
   - Create `Designation`, `Class`, `Tier` flags based on relative CTC comparisons.

4. **Unsupervised Clustering Preparation**  
   - Encode categorical features, scale numeric features, check clustering tendency.

5. **Clustering & Validation**  
   - Use Elbow method + silhouette score to pick k. Run K-Means, and Hierarchical clustering (sample if large).
   - Compare clusters against manual flags (confusion/overlap) and interpret.
   
---

## 🧰 Tech Stack
- **Pandas, NumPy** — data cleaning & manipulation  
- **scikit-learn** — KNN imputation, StandardScaler, KMeans, hierarchical clustering, metrics  
- **SciPy / statsmodels** — optional stats & hierarchical linkage  
- **Matplotlib, Seaborn** — EDA & visualization  

---

## 🎯 Outcomes
- Cleaned dataset with added `Years_of_Experience`, `Designation`, `Class`, `Tier` flags.  
- Ranked lists:
  - Top 10 Tier-1 employees (company-wide top earners).
  - Top/Bottom 10 Data Science positions per company (Class 1 / Class 3).
  - Top companies by average CTC and top 2 positions per company.
- Validated unsupervised clusters that align (or highlight differences) with manual segmentation.
- Actionable recommendations for Scaler (targeted upskilling, placement focus, employer partnerships).


