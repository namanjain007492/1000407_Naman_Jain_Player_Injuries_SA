# FootLens AI — Executive Sports Telemetry & Biomechanics Dashboard

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://your-app-name.streamlit.app)
![Python](https://img.shields.io/badge/Python-3.11%2B-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.2%2B-150458?logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-1.26%2B-013243?logo=numpy&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-5.22%2B-3F4F75?logo=plotly&logoColor=white)
![Status](https://img.shields.io/badge/Status-Production%20Ready-success)

**Course:** Mathematics for AI-II (Summative Assessment)  
**CRS:** Artificial Intelligence  
**Scenario:** Scenario 1 — FootLens Analytics (Player Injuries and Team Performance Dashboard)  
**Live Web App:** [Launch FootLens AI(https://1000407namanjainplayerinjuries.streamlit.app/)

---

## Table of Contents
1. [Executive Summary & Problem Statement](#-1-executive-summary--problem-statement)
2. [Research Questions & Domain Objectives](#-2-research-questions--domain-objectives)
3. [System Architecture & Data Flow](#-3-system-architecture--data-flow)
4. [Data Engineering & ETL Pipeline](#-4-data-engineering--etl-pipeline)
5. [Data Dictionary & Feature Engineering Formulas](#-5-data-dictionary--feature-engineering-formulas)
6. [Dashboard Modules & Analytical Deep Dive](#-6-dashboard-modules--analytical-deep-dive)
7. [Mathematical & Statistical Modeling](#-7-mathematical--statistical-modeling)
8. [Tech Stack & Performance Optimization](#-8-tech-stack--performance-optimization)
9. [Repository Structure](#-9-repository-structure)
10. [Installation & Cloud Deployment Guide](#-10-installation--cloud-deployment-guide)
11. [Dashboard Screenshots](#-11-dashboard-screenshots)
12. [Future Roadmap](#-12-future-roadmap)
13. [Author & Submission Details](#-13-author--submission-details)

---

##  1. Executive Summary & Problem Statement
In elite professional football, player injuries are not merely medical setbacks—they are **tactical, statistical, and financial liabilities**. A single soft-tissue injury to a starting midfielder or striker can derail a club's league campaign, cost millions in unproductive wages, and trigger a cascade of secondary injuries due to squad overexertion.

**FootLens AI** is an end-to-end, interactive sports telemetry and biomechanics decision-support platform built with **Python, Pandas, NumPy, Plotly, and Streamlit**. Designed for technical directors, sports scientists, and club medical departments, the dashboard ingests raw match and biometric telemetry, automates data cleaning and position-stratified imputation, quantifies team performance degradation during player absences, and runs real-time **Monte Carlo simulations** to forecast league points at risk.

---

##  2. Research Questions & Domain Objectives
The exploratory data analysis (EDA) and interactive visualizations are engineered to answer **six core analytical questions**:

1. **Injury Impact Ranking:** Which specific injury pathologies (e.g., ACL Tear, Hamstring Strain, Ankle Sprain) cause the steepest drop in overall team performance and longest rehabilitation windows?
2. **Team Resilience & Standings Shift:** How does a club's Win / Draw / Loss distribution shift when key squad members are sidelined?
3. **Post-Rehabilitation Recovery:** How do individual player match ratings compare before injury versus after returning to play, and which athletes demonstrate the strongest comeback trajectories?
4. **Temporal & Organizational Clustering:** Are specific calendar months (e.g., winter fixture congestion) or specific clubs experiencing disproportionate injury clusters?
5. **Age vs. Degradation Correlation:** How does player age correlate with both team performance drop and rehabilitation duration?
6. **Biomechanical & Cryotherapy Efficacy:** How do Acute:Chronic Workload Ratio (ACWR), sleep quality, and post-match Cold Water Immersion (cryotherapy) compliance affect Creatine Kinase (CK) biomarkers and soft-tissue relapse probability?

---

##  3. System Architecture & Data Flow

1. **Data Ingestion:** Raw match and biometric telemetry (**raw_df**) is loaded into the application.
2. **Cached ETL Engine:** **initialize_telemetry_engine()** (decorated with **@st.cache_data**) executes deduplication, schema standardization across 28 telemetry codes, temporal casting to **datetime64[ns]**, position-stratified median imputation, and vectorized feature engineering.
3. **Global Reactive Filter Matrix:** A persistent sidebar dynamically slices the dataset across **Club, Position, Severity Tier, Pathology, Trauma Mechanism, Age Bracket, and Cryotherapy Compliance**.
4. **7 Interactive Analytics & AI Modules:** Filtered dataframes flow in real time into the Trauma Feed & ETL Audit, Cryotherapy Protocols, Core EDA & Club Analytics, 105×68m Pitch & 3D Lab, Athlete Bio-Passport, AI Injury Predictor & Monte Carlo Simulator, and Tactical Squad Rotation & CSV Export.

---

##  4. Data Engineering & ETL Pipeline
All raw telemetry passes through a deterministic, memory-cached **Pandas & NumPy ETL pipeline** inside **initialize_telemetry_engine()** to guarantee zero data leakage, fast re-renders, and full auditability:

| Pipeline Stage | Technical Implementation | Purpose & Impact |
| :--- | :--- | :--- |
| **1. Deduplication** | **df.drop_duplicates()** | Eliminates redundant sensor packet transmissions from pitchside wearables. |
| **2. Schema Standardization** | Column dictionary mapping | Converts 28 abbreviated raw telemetry codes (e.g., **plyr_nm**, **acwr_ratio**, **rtg_before**) into readable executive labels. |
| **3. Temporal Casting** | **pd.to_datetime()** | Converts string timestamps into **datetime64[ns]** objects to compute exact calendar-month clusters and recovery durations. |
| **4. Stratified Imputation** | **groupby('Position').transform('median')** | Fills missing **NaN** values in **Pre-Injury Rating** and **Post-Injury Rating** using tactical position medians (**Forward**, **Midfielder**, **Defender**, **Goalkeeper**) rather than global averages, preserving positional rating distributions. |
| **5. Vectorized Feature Engineering** | NumPy & Pandas array operations | Computes derived biomechanical, tactical, and financial metrics in O(n) vectorized time without Python loops. |

---

##  5. Data Dictionary & Feature Engineering Formulas

### Core Engineered Metrics
* **Recovery Days:** Exact duration between injury onset and medical clearance.
* **Games Missed:** Estimated competitive fixtures missed based on recovery window and match cadence.
* **Rating Improvement:** Net individual form recovery post-rehabilitation (**Post-Injury Rating minus Pre-Injury Rating**).
* **Performance Drop Index (PDI):** Composite metric weighting injury severity, league points dropped during absence, and the sidelined player's baseline match rating.
* **Sprint Speed Loss (km/h):** Quantifies post-injury peak velocity degradation from GPS tracking data.
* **Relapse Probability (%):** Biomechanical risk score driven by ACWR overload, poor sleep quality, elevated Creatine Kinase (CK), and cryotherapy non-compliance.
* **Financial Wage Impact ($K):** Estimated unproductive club payroll expenditure incurred while the athlete is unavailable for selection.

---

## 6. Dashboard Modules & Analytical Deep Dive
A **global sidebar filter matrix** dynamically slices the dataset across 7 dimensions (**Club, Position, Severity Tier, Pathology, Trauma Mechanism, Age Bracket, and Cryotherapy Compliance**) and updates all KPIs and charts in real time across **7 specialized tabs**:

### 1.  Trauma Feed & Data Engineering Pipeline
* **Pitchside Video Integration:** Embedded match trauma video feed for qualitative biomechanics review.
* **ETL Transparency:** Side-by-side raw vs. cleaned dataframe inspection tables.
* **Imputation Audit Chart:** Before vs. After **NaN** count bar chart proving zero missing values remain in critical rating columns.

### 2.  Cryotherapy & Sports Medicine Protocols
* **Clinical Reference Guide:** Evidence-based protocols for Cold Water Immersion (10°C–12°C), Contrast Water Therapy, and medical contraindications.
* **Rehab Duration Comparison:** Bar chart contrasting average recovery days across cryotherapy compliance tiers.
* **Biomarker Distribution:** Box plot of **Creatine Kinase (U/L)** levels demonstrating reduced muscle damage markers in compliant athletes.

### 3. 📊 Club Performance & Recovery Analytics (Core EDA)
* **Top Injuries by Team Impact (Horizontal Bar Chart):** Ranks pathologies by average **Performance Drop Index**.
* **Absence Match Outcomes (Stacked Bar Chart):** Compares club Win / Draw / Loss records during key player absences.
* **Injury Cluster Heatmap (pd.pivot_table):** Cross-tabulates Clubs vs. Calendar Months to expose seasonal injury spikes.
* **Age vs. Impact Analysis (Scatter Plot + OLS Trendline):** Plots Player Age against Performance Drop Index, bubble-sized by **Recovery Days**, with a fitted NumPy Ordinary Least Squares regression line.
* **Comeback Leaderboard & Position Pivot Table:** Highlights top-recovering athletes and aggregates recovery metrics by tactical role.

### 4. 🏟️ Spatial Pitch Map & 3D Multivariate Lab
* **105m × 68m Pitch Trauma Density Map:** Interactive football pitch plotting exact **(X, Y)** coordinates of injury events color-coded by severity tier.
* **3D Multivariate Biometric Lab:** Interactive 3D scatter plot mapping **ACWR (X)**, **Sleep Quality (Y)**, and **Relapse Probability (Z)** to uncover non-linear fatigue thresholds.

### 5. 🏃 Athlete Bio-Passport & Head-to-Head
* **Longitudinal Form Tracker:** Dual-series line chart tracking an individual player's Pre-Injury vs. Post-Recovery match ratings over time.
* **Clinical History Dossier:** Complete tabular record of an athlete's injuries, recovery timelines, and biomarker readings.

### 6. 🤖 AI Injury Predictor & Monte Carlo Simulator
* **Interactive Biometric Sliders:** Adjust ACWR, sleep hours, fatigue index, and cryotherapy adherence to compute live soft-tissue relapse probability.
* **1,000-Iteration Monte Carlo Engine:** Simulates upcoming fixture blocks using binomial probability sampling to project expected league points lost and worst-case risk tails.

### 7. ♟️ Tactical Squad Rotation & Telemetry Export
* **High-Risk Rotation Alerts:** Automated triage table flagging players exceeding the critical **Relapse Probability ≥ 55%** threshold for immediate squad rotation.
* **One-Click Data Export:** Download the cleaned, dynamically filtered dataset as a **.csv** file for external reporting.

---

## 🧮 7. Mathematical & Statistical Modeling
* **Ordinary Least Squares (OLS) Regression:** Implemented via **np.polyfit(x, y, 1)** to model the linear trend between player age and team performance degradation without heavy external ML dependencies.
* **Monte Carlo Fixture Simulation:** Executes 1,000 stochastic trials using **np.random.binomial** to model the probability distribution of points dropped over congested match schedules given a player's live relapse risk.
* **Stratified Imputation:** Uses conditional medians grouped by tactical position to minimize variance distortion compared to global mean imputation.

---

## 🛠️ 8. Tech Stack & Performance Optimization
* **Frontend & App Framework:** Streamlit (custom Cyber-UI CSS injection, wide layout, reactive state management, **@st.cache_data**)
* **Data Engineering:** Pandas (**groupby**, **agg**, **pivot_table**, vectorized column transforms)
* **Numerical Computing:** NumPy (OLS polyfit, binomial Monte Carlo sampling, array math)
* **Interactive Visualization:** Plotly Express & Plotly Graph Objects (hover tooltips, zoom/pan, 3D WebGL scatter plots)

### Required Packages (requirements.txt)
* **streamlit>=1.35.0**
* **pandas>=2.2.0**
* **numpy>=1.26.0**
* **plotly>=5.22.0**

---

## 📁 9. Repository Structure
* **app.py** — Main Streamlit application, Cyber-UI CSS & ETL engine
* **requirements.txt** — Python package dependencies for local & cloud deployment
* **README.md** — Comprehensive project documentation
* **Screen_Recording_2026-11-05_140813.mp4** — Pitchside trauma video asset (optional)
* **screenshots/hero_and_etl.png** — Executive KPIs & ETL Imputation Audit
* **screenshots/eda_visualizations.png** — Core EDA, Heatmap & OLS Scatter
* **screenshots/spatial_and_simulator.png** — 105×68m Pitch Map, 3D Lab & Monte Carlo Simulator

---

##  10. Installation & Cloud Deployment Guide

### Option A: Run Locally
1. **Clone the repository:** Run **git clone https://github.com/YourUsername/YourRepository.git** and navigate into the folder with **cd YourRepository**.
2. **Create a virtual environment:** Run **python -m venv venv** and activate it (**source venv/bin/activate** on macOS/Linux or **venv\Scripts\activate** on Windows).
3. **Install dependencies:** Run **pip install -r requirements.txt**.
4. **Launch the application:** Run **streamlit run app.py**. The dashboard will open automatically at **http://localhost:8501**.

### Option B: Deploy on Streamlit Community Cloud
1. Push **app.py**, **requirements.txt**, and **README.md** to a public GitHub repository.
2. Navigate to [share.streamlit.io](https://share.streamlit.io) and sign in with GitHub.
3. Click **New app**, then select your repository, branch (**main**), and entry file (**app.py**).
4. Click **Deploy!** and update the live URL at the top of this **README.md**.

---

##  11. Dashboard Screenshots

| Executive Command Center & ETL Audit | Core EDA & Performance Drop Visuals |
| :---: | :---: |
| ![ETL Audit](screenshots/hero_and_etl.png) | ![EDA Charts](screenshots/eda_visualizations.png) |

| Spatial Pitch Map & Monte Carlo Simulator |
| :---: |
| ![Spatial & Simulator](screenshots/spatial_and_simulator.png) |

---

##  12. Future Roadmap
* **Live Wearable API Integration:** Connect real-time GPS vest telemetry (Catapult / STATSports) via REST webhooks.
* **Machine Learning Upgrade:** Replace heuristic relapse scoring with a trained XGBoost / Random Forest classifier with SHAP explainability plots.
* **Automated PDF Medical Reports:** Add one-click generation of executive medical briefings for coaching staff.

---

##  13. Author & Submission Details
* **Student Name:** Naman Jain
* **Candidate Registration Number:** 1000407
* **School / Institution:** Jain Vidyalaya
* **Course:** Mathematics for AI-II (Artificial Intelligence)

## 


