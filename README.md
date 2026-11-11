# ⛺ Demographic & Humanitarian Population Camps Analysis

[![Live Demo](https://img.shields.io/badge/Live_Dashboard-ORION_Analytics-6C5CE7?style=for-the-badge&logo=googlechrome&logoColor=white)](https://ayagomaa-cmd.github.io/population-camps-demographic-analysis/)
[![Python](https://img.shields.io/badge/Python-3.9+-blue?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data_Analysis-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Status](https://img.shields.io/badge/Cohort-9%2C917_Inspections-2ED573?style=for-the-badge)](#project-overview)

An end-to-end exploratory data analysis (EDA), statistical anomaly audit, and feature engineering pipeline examining demographic shifts, gender balances, household crowding, and shelter allocations across refugee and civilian camps in **Yemen, Syria, Iraq, and Libya** (2017–2018).

---

## 🔗 Quick Links
- 🌐 **Interactive Web Dashboard:** [Launch Live ORION Dashboard](https://ayagomaa-cmd.github.io/population-camps-demographic-analysis/)
- 📓 **Jupyter Analysis Notebook:** [View Notebook](population_camp_data_analysis.ipynb)

---

## 📌 Project Overview
- **Dataset Scale:** 9,917 observational survey records across 19 major cities and gathering sites in 4 conflict-impacted countries.
- **Screened Population:** $59,006,538$ cumulative residents and $1,187,621$ housing units tracked across a 23-month survey timeline.
- **Core Objectives:**
  * Quantify temporal migration patterns and population changes between 2017 and 2018.
  * Audit gender ratios, vulnerability indicators, and household density metrics.
  * Evaluate shelter modalities (**Flats, Rooms, Houses, Tents**) to inform humanitarian aid logistics and shelter capacity planning.

---

## 💡 Key Analytical Findings

| Metric / Dimension | Statistical Value | Humanitarian Takeaway |
| :--- | :--- | :--- |
| **Highest Shelter Burden** | **Yemen** ($478,256$ houses / $23.88\text{M}$ members) | Accounts for over $40\%$ of all surveyed camp populations, led by Aden (*السليمانيات*). |
| **Secondary Population Hub** | **Syria** ($389,439$ houses / $19.43\text{M}$ members) | High shelter concentration in northern border gathering clusters (Atma, Jarablus). |
| **Gender Distribution** | **$56.7\%$ Female** vs. **$43.3\%$ Male** | Female displacement majority observed across $74\%$ of surveyed camp clusters. |
| **Household Density** | **$\approx 49.7$ people / dwelling** | High crowding pressure; severe overcrowding ($>70$ people/unit) observed in emergency clusters. |
| **Shelter Modality Split** | **$76.5\%$ Structural** vs. **$23.5\%$ Tent** | $7,588$ urban inspections (Flats, Rooms, Houses) vs. $2,329$ dedicated emergency Tent camps ($279\text{K}+$ tents). |
| **Housing Linear Fit** | **$r = 0.30$** ($p < 0.001$) | Moderate positive correlation between dwelling units and total members; bounded by maximum shelter capacity. |

---

## 🔬 Methodology & Engineering Pipeline

### 1. Data Cleaning & Integrity Screening
- **Temporal Parsing:** Extracted longitudinal features (`Check_Year`, `Check_Month`, `Check_Day`) from datetime timestamps spanning Jan 2017 to Nov 2018.
- **Structural Missing Value Imputation:**
  * Resolved the initial $14,575$ missing entries.
  * The `Tent` feature was null in $7,588$ urban records and imputed to $0$.
  * Conversely, `Room`, `Flat`, and `House` were systematically absent in pure tent camps ($2,329 \times 3 = 6,987$ valid structural nulls).
- **String Normalization:** Applied `.astype(str).str.strip()` to eliminate irregular whitespace anomalies across regional and Arabic site names.
- **Parametric Outlier Screening:** Evaluated standardized $Z$-scores (`Members_Z_Score`). Confirmed zero catastrophic measurement anomalies ($|Z| > 3$), with populations naturally distributed between $5$ and $15,933$ per site.

### 2. Feature Engineering
- **Gender Proportions:** Derived `Male_Percentage` and `Female_Percentage` with vectorized `np.where()` guards against division-by-zero errors.
- **Household Crowding Index:** Engineered `Avg_People_Per_House = Members / Houses` to benchmark human density per shelter unit.
- **Dominant Shelter Categorization:** Mapped dwelling volumes via `.idxmax(axis=1)` to classify prevailing shelter infrastructure (`Flat`, `House`, `Room`, `Tent`).
- **Feature Normalization:** Applied `MinMaxScaler` across continuous dimensions (`Houses`, `Members`, `Avg_People_Per_House`) into $[0, 1]$ ranges for comparative profiling.

### 3. Statistical Analysis & Visualizations
- **Temporal Multi-Line Tracking:** Longitudinal trends mapping population allocations by country and year.
- **Crosstabulation Pivot Matrix:** Country $\times$ Year matrix validating house distributions:
  * **Iraq:** $83,818$ (2017) $\rightarrow$ $80,103$ (2018) | **Total:** $163,921$
  * **Libya:** $80,731$ (2017) $\rightarrow$ $75,274$ (2018) | **Total:** $156,005$
  * **Syria:** $197,814$ (2017) $\rightarrow$ $191,625$ (2018) | **Total:** $389,439$
  * **Yemen:** $243,963$ (2017) $\rightarrow$ $234,293$ (2018) | **Total:** $478,256$
  * **Grand Total:** $1,187,621$ housing units.
- **Kernel Density Estimation (KDE):** Overlaid dual-distribution curves comparing female skewness vs. male density across all camps.
- **Pearson Correlation Heatmap ($8 \times 8$):** Mapped inter-metric dependencies, confirming strong collinearity between structural housing types ($r = 1.00$) and high gender-to-population correlations ($r = 0.91$ for Female, $r = 0.87$ for Male).

---

## 🗂️ Repository Structure

```text
├── index.html                           # Standalone live interactive ORION dashboard
├── population_camp_data_analysis.ipynb  # Comprehensive Python Jupyter Notebook (EDA & Modeling)
└── README.md                            # Project documentation and analytical synthesis
```

---

## 🛠️ Tech Stack & Libraries
- **Language:** Python
- **Data Manipulation:** Pandas, NumPy
- **Feature Preprocessing:** Scikit-Learn (`StandardScaler`, `MinMaxScaler`)
- **Visual Analytics:** Matplotlib, Seaborn
- **Interactive Web Dashboard:** HTML5, CSS3 Grid/Flexbox, Vanilla ES6+ JavaScript, SVG Data Visualisation (ORION Design System)

---

## 🚀 How to Run Locally

1. **Clone the repository:**
   ```bash
   git clone https://github.com/ayagomaa-cmd/population-camps-demographic-analysis.git
   cd population-camps-demographic-analysis
   ```

2. **Launch the Jupyter Notebook:**
   ```bash
   jupyter notebook population_camp_data_analysis.ipynb
   ```

3. **Open the Live Dashboard:**
   Simply open `index.html` in any modern web browser or launch via local server:
   ```bash
   python -m http.server 8000
   ```
   Navigate to `http://localhost:8000` to interact with the dashboard.
