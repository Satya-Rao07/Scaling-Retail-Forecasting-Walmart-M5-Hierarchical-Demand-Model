# 📊 M5 Hierarchical Demand Forecasting

## 🔍 Overview
This project implements a scalable hierarchical demand forecasting pipeline on the Walmart M5 dataset using XGBoost. It focuses on improving forecast accuracy at the granular item-store level by leveraging more stable patterns at higher aggregation levels.

The approach mirrors real-world retail planning systems, where forecasts must remain **coherent across hierarchies** while still being actionable at the SKU level.

---

## 🎯 Problem Statement
Retail demand forecasting operates across multiple hierarchical levels:
- Item → Department → Category  
- Store → State  

Forecasting directly at the lowest level is often noisy and unstable, leading to:
- Stockouts and lost sales  
- Excess inventory and higher holding costs  

The goal of this project is to:
> Improve item-level forecast accuracy by combining aggregated forecasting with intelligent disaggregation, while maintaining hierarchical consistency.

---

## 🧠 Approach

### 1. Hierarchical Forecasting Strategy
- Forecast demand at an aggregated level (dept × store)
- Distribute forecasts down to item level using learned proportions  
- Ensure coherence using **largest remainder rounding**

---

### 2. Dual Model Architecture
- **Model 1 (Aggregate Model):**
  - Predicts demand at dept-store level  
  - Captures stable demand signals  

- **Model 2 (Disaggregation Model):**
  - Learns proportional contribution of items within each group  
  - Allocates aggregate forecasts to item level  

---

### 3. Feature Engineering
- Lag features (e.g., 28-day, 35-day)
- Rolling statistics and demand signals  
- Calendar features:
  - Weekday/weekend indicators  
  - Seasonal encodings  
- Price-based features:
  - Price momentum  
- Event and SNAP indicators  

---

### 4. Training Enhancements
- **Stockout-aware training** to reduce demand distortion  
- **Time-weighted samples** using exponential decay to prioritize recent trends  

---

### 5. Evaluation Metrics
- **Aggregate wMAPE:** Measures accuracy at higher levels (business-relevant)  
- **Item-level RMSE:** Measures granular prediction accuracy  

---

## 📈 Results
- **Aggregate wMAPE:** 8.89% (dept-store level)  
- **Item-level RMSE:** 2.24 units  
- **Performance Gain:** 21.1% improvement over lag-28 seasonal naive baseline  

These results highlight the effectiveness of combining hierarchical aggregation with machine learning models.

---

## 💡 Key Insights
- Aggregated forecasts provide significantly more stable signals than item-level models  
- Hierarchical disaggregation improves granular accuracy without sacrificing consistency  
- Handling stockouts is critical to avoid biased demand learning  
- Feature engineering contributes more to performance than model complexity  

---

## 🏗️ Project Structure

    ├── notebooks/           # Data exploration and model development
    ├── data/                # Input datasets (not included)
    ├── outputs/             # Predictions and evaluation results
    └── README.md            # Project documentation

---

## ▶️ How to Run

1. Download the dataset from Kaggle:  
   https://www.kaggle.com/competitions/m5-forecasting-accuracy/data  

2. Update the data path:

       DATA_DIR = "path_to_your_data"

3. Run the notebook:

       notebooks/m5_forecasting.ipynb

---

## 🚀 Future Improvements
- Implement formal hierarchical reconciliation methods (e.g., MinT)  
- Extend to probabilistic forecasting  
- Incorporate external drivers (weather, promotions depth)  
- Deploy as an API or integrate into a planning dashboard  

---

## 👤 Author
Satya Rao — Supply Chain Professional (CSCP) focused on data-driven demand planning, forecasting, and decision analytics

---

## ⭐ Final Note
This project demonstrates how combining **machine learning with hierarchical supply chain thinking** can significantly improve forecasting performance, making models more aligned with real-world retail planning systems.
