# ⚽ FootLens AI — Executive Sports Telemetry & Biomechanics Dashboard

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://your-app-name.streamlit.app)
![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.2%2B-150458?logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-1.26%2B-013243?logo=numpy&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-5.22%2B-3F4F75?logo=plotly&logoColor=white)
![Status](https://img.shields.io/badge/Status-Production%20Ready-success)

> **Course:** Mathematics for AI-II (Summative Assessment)  
> **CRS:** Artificial Intelligence  
> **Scenario:** Scenario 1 — FootLens Analytics (Player Injuries and Team Performance Dashboard)  
> **Live Web App:** [🚀 Launch FootLens AI Dashboard](https://your-app-name.streamlit.app) *(Replace with your deployed Streamlit Cloud URL)*

---

## 📑 Table of Contents
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

## 📌 1. Executive Summary & Problem Statement
In elite professional football, player injuries are not merely medical setbacks—they are **tactical, statistical, and financial liabilities**. A single soft-tissue injury to a starting midfielder or striker can derail a club's league campaign, cost millions in unproductive wages, and trigger a cascade of secondary injuries due to squad overexertion.

**FootLens AI** is an end-to-end, interactive sports telemetry and biomechanics decision-support platform built with **Python, Pandas, NumPy, Plotly, and Streamlit**. Designed for technical directors, sports scientists, and club medical departments, the dashboard ingests raw match and biometric telemetry, automates data cleaning and position-stratified imputation, quantifies team performance degradation during player absences, and runs real-time **Monte Carlo simulations** to forecast league points at risk.

---

## 🎯 2. Research Questions & Domain Objectives
The exploratory data analysis (EDA) and interactive visualizations are engineered to answer **six core analytical questions**:

1. **Injury Impact Ranking:** Which specific injury pathologies (e.g., ACL Tear, Hamstring Strain, Ankle Sprain) cause the steepest drop in overall team performance and longest rehabilitation windows?
2. **Team Resilience & Standings Shift:** How does a club's Win / Draw / Loss distribution shift when key squad members are sidelined?
3. **Post-Rehabilitation Recovery:** How do individual player match ratings compare before injury versus after returning to play, and which athletes demonstrate the strongest comeback trajectories?
4. **Temporal & Organizational Clustering:** Are specific calendar months (e.g., winter fixture congestion) or specific clubs experiencing disproportionate injury clusters?
5. **Age vs. Degradation Correlation:** How does player age correlate with both team performance drop and rehabilitation duration?
6. **Biomechanical & Cryotherapy Efficacy:** How do Acute:Chronic Workload Ratio (ACWR), sleep quality, and post-match Cold Water Immersion (cryotherapy) compliance affect Creatine Kinase (CK) biomarkers and soft-tissue relapse probability?

---

## 🏗️ 3. System Architecture & Data Flow

```text
┌───────────────────────────┐
│   Raw Match & Biometric   │
│     Telemetry (raw_df)    │
└─────────────┬─────────────┘
              │
              ▼
┌───────────────────────────────────────────────────────────┐
│  ETL Engine: initialize_telemetry_engine() [@st.cache_data]│
│  1. Deduplication (.drop_duplicates)                      │
│  2. Schema Standardization (28 Telemetry Codes -> Labels) │
│  3. Temporal Parsing (datetime64[ns])                     │
│  4. Position-Stratified Median Imputation (NaN Handling)  │
│  5. Vectorized Feature Engineering (KPIs & Biomarkers)    │
└─────────────┬─────────────────────────────────────────────┘
              │
              ▼
┌───────────────────────────────────────────────────────────┐
│        Global Reactive Sidebar Filter Matrix              │
│  (Club | Position | Severity | Pathology | Mechanism |    │
│   Age Bracket | Cryotherapy Compliance)                   │
└─────────────┬─────────────────────────────────────────────┘


              │
              ▼
┌───────────────────────────────────────────────────────────
