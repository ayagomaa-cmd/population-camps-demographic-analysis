# ⛺ Demographic & Humanitarian Population Camps Analysis

An in-depth exploratory data analysis (EDA), anomaly audit, and feature engineering pipeline examining demographic shifts, gender ratios, household crowding, and shelter distribution across refugee and civilian gathering sites in Iraq, Syria, Libya, and Yemen (2017–2018).

📓 **Interactive Notebook:** [View Notebook](population_camp_data_analysis.ipynb)

---

## 📌 Project Overview
* **Dataset Scale:** 9,900+ observational survey records spanning 19 major cities/regions across 4 conflict-impacted countries.
* **Core Objectives:**
  * Evaluate population influx and migration dynamics between 2017 and 2018[cite: 16].
  * Quantify gender distributions and household density metrics[cite: 16].
  * Identify dominant shelter typologies (Flats, Houses, Rooms, Tents) to support humanitarian logistics[cite: 16].

---

## 🔬 Methodology & Key Stages

### 1. Data Cleaning & Integrity Screening
* **Temporal Slicing:** Parsed `Date` into structured `Year`, `Month`, and `Day` components for longitudinal trend evaluation[cite: 16].
* **Missing Value Imputation:** Handled missing data across shelter categories; imputed missing values in the `Tent` classification to zero where structured dwellings were present[cite: 16].
* **Statistical Anomaly Auditing:** Applied parametric $Z$-score filtering on population sizes (`Members`) to confirm sample boundaries and verify absence of catastrophic measurement outliers ($|Z| > 3$)[cite: 16].

### 2. Feature Engineering
* `Male_Percentage` & `Female_Percentage`: Derived normalized gender distributions with zero-division exception handling[cite: 16].
* `Avg_People_Per_House`: Created a crowding metric measuring household occupancy load per dwelling unit[cite: 16].
* `Dominant_Housing`: Evaluated dwelling volumes (`Flat`, `House`, `Room`, `Tent`) across each site to categorize the prevailing shelter typology[cite: 16].
* **Feature Scaling:** Applied `MinMaxScaler` across continuous features (`Houses`, `Members`, `Avg_People_Per_House`) to normalize distributions for comparative modeling[cite: 16].

### 3. Exploratory Data Visualization
* **Macro Distributions:** Aggregated cumulative population numbers across host nations[cite: 16].
* **Temporal Tracking:** Time-series multi-line trend plots tracking population movements across years per country[cite: 16].
* **KDE Density Profile:** Kernel Density Estimate (KDE) plot mapping the distribution spread of female vs. male percentages across all surveyed camps[cite: 16].

---

## 🛠️ Tech Stack
* **Language:** Python
* **Data Manipulation:** Pandas, NumPy
* **Preprocessing:** Scikit-learn (`StandardScaler`, `MinMaxScaler`)
* **Visualization:** Matplotlib, Seaborn
