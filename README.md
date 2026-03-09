# 🌿 AI-Driven Smart Irrigation System for Water-Efficient Farming in Ireland

> **MSc Data Analytics Thesis Project** — Technological University of the Shannon (TUS), Limerick  
> **Author:** Vignesh Gunnala | **Supervisor:** Eric McNamara | **Submitted:** August 2025

---

## 📌 Overview

Irish agriculture is increasingly exposed to climate variability — irregular rainfall, short droughts, and rising summer temperatures are making traditional irrigation scheduling unreliable. This project develops a **sensor-free, AI-driven irrigation decision system** tailored specifically to Ireland's temperate maritime climate.

Rather than relying on expensive IoT hardware, the system uses **publicly available weather data** from Met Éireann, standard agronomic formulas (FAO-56), and machine learning to answer one critical question for Irish farmers:

> **"Should I irrigate today — or skip?"**

---

## 🎯 Key Features

-  **No IoT sensors required** — fully data-driven using public weather data
-  **15-year historical dataset** (2010–2024) across multiple Irish counties
-  **Rain-aware skip logic** — optimised for Ireland's high-rainfall, high-variability climate
-  **Three ML models compared** — Random Forest, XGBoost, and LSTM
-  **Explainable recommendations** — SHAP-based feature importance
-  **County-level granularity** — accounts for regional climate differences across Ireland

---

## 🧠 How It Works

```
Met Éireann Weather Data (2010–2024)
        ↓
Data Cleaning & Feature Engineering
(rolling rainfall, ET₀, days-since-last-rain, season flags)
        ↓
FAO-56 Agronomic Pipeline
ET₀ → ETc (with crop coefficients Kc) → Effective Rainfall (Pe)
        ↓
Net Irrigation Requirement (NIR) = max(0, ETc − Pe)
        ↓
ML Model Training (RF / XGBoost / LSTM)
        ↓
Daily County-Level Irrigation Recommendation
("Irrigate" or "Skip" with explanation)
```

---

## 📂 Project Structure

```
smart-irrigation-ireland/
│
├── data/
│   ├── raw/                  # Raw Met Éireann weather data
│   ├── processed/            # Cleaned & feature-engineered datasets
│   └── soil/                 # Static soil attributes (AWC, drainage class)
│
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_EDA.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_model_training.ipynb
│   └── 05_model_evaluation.ipynb
│
├── models/
│   ├── random_forest_model.pkl
│   ├── xgboost_model.pkl
│   └── lstm_model.h5
│
├── outputs/
│   ├── figures/              # EDA charts, anomaly plots, seasonal graphs
│   └── results/              # Model evaluation metrics
│
├── requirements.txt
└── README.md
```

---

## 📊 Dataset

| Variable | Description | Source |
|---|---|---|
| Temperature (°C) | Daily min/max/mean | Met Éireann |
| Rainfall (mm) | Daily precipitation | Met Éireann |
| Relative Humidity (%) | Daily average | Met Éireann |
| Wind Speed (m/s) | Daily average | Met Éireann |
| Solar Radiation | Daily estimate | Met Éireann / Copernicus |
| Soil AWC / Drainage | Static soil attributes | ESDAC |
| Crop Coefficients (Kc) | Barley, wheat, potatoes, grass | FAO-56 |

- **Coverage:** 2010–2024 (daily resolution)
- **Scope:** Multiple Irish counties
- **Size:** 5,000+ daily observations

---

##  Models

| Model | Strength | Best For |
|---|---|---|
| **Random Forest** | Robust, interpretable, handles noise | Stable baseline, feature importance |
| **XGBoost** | Tabular data, non-linear interactions, fast | County-level daily predictions |
| **LSTM** | Sequential memory, temporal patterns | Transitional seasons, carry-over rainfall effects |

### Evaluation Metrics
- **MAE** (Mean Absolute Error) on Net Irrigation Requirement
- **Precision & Recall** of skip/irrigate decisions
- **Water saved (mm/ha)** from correct skip decisions
- Time-series cross-validation: Train 2010–2018 → Validate 2019–2021 → Test 2022–2024

---

## 📈 Key Findings

-  Average summer temperatures in Ireland rose by **~0.5–0.8°C** between 2010 and 2024
-  The **2018 drought** saw rainfall drop below 50% of average in eastern counties
-  Summer rainfall declining while winter rainfall increasing — creating a critical water gap during crop growth stages
-  Extreme rainfall days increased from **5/year (2010–2014)** to **9/year (2020–2024)**
-  Western counties (Galway, Mayo) average **~1,400 mm/year** vs eastern counties (Dublin) at **~850 mm/year**

---

## 🚀 Getting Started

### Prerequisites
```bash
pip install -r requirements.txt
```

### Main dependencies
```
pandas
numpy
scikit-learn
xgboost
tensorflow / keras
matplotlib
seaborn
shap
jupyter
```

### Run the Pipeline
```bash
# Step 1 — Data cleaning
jupyter notebook notebooks/01_data_cleaning.ipynb

# Step 2 — Exploratory Data Analysis
jupyter notebook notebooks/02_EDA.ipynb

# Step 3 — Feature engineering
jupyter notebook notebooks/03_feature_engineering.ipynb

# Step 4 — Model training
jupyter notebook notebooks/04_model_training.ipynb

# Step 5 — Evaluation & results
jupyter notebook notebooks/05_model_evaluation.ipynb
```

---

## 🔍 Sample Output

```
County: Kildare | Date: 2024-07-14
─────────────────────────────────────────
ET₀:          4.2 mm/day
ETc (Barley): 3.8 mm/day
Effective Rainfall (Pe): 1.1 mm
NIR:          2.7 mm

Recommendation: 💧 IRRIGATE
Reason: Crop demand exceeds effective rainfall by 2.7 mm.
        No significant rain forecast in next 48 hours.
```

---

## 📚 Academic Context

This project was submitted as an **MSc thesis** in partial fulfilment of the Degree of Master of Science in Data Analytics at TUS Limerick. It contributes to the literature by:

1. Applying AI-driven irrigation to a **temperate, high-rainfall European context** rarely covered in existing research
2. Formalising a **sensor-free NIR label** for supervised learning using FAO-56 agronomy
3. Delivering a **reproducible, county-level pipeline** that prioritises explainability and farmer usability over black-box complexity

---

## 📄 Keywords

`Smart Irrigation` · `Ireland` · `Machine Learning` · `Evapotranspiration` · `FAO-56` · `Sensor-Free` · `Decision Support` · `Precision Agriculture` · `Random Forest` · `XGBoost` · `LSTM` · `Time Series`

---

## 👤 Author

**Vignesh Gunnala**  
MSc Data Analytics — TUS Limerick, Ireland  
📧 vigneshgunnala440@gmail.com  
🔗 [LinkedIn](https://www.linkedin.com/in/vignesh-gunnala-5547711b4/)

---

## 📜 License

This project is for academic and educational purposes. Data sourced from Met Éireann and ESDAC is subject to their respective licensing terms.
