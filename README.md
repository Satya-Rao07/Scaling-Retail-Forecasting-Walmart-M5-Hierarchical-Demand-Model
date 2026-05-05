# M5 Hierarchical Demand Forecasting

Hierarchical forecasting approach for the Walmart M5 dataset using XGBoost, 
achieving a 21.1% improvement over a seasonal naive baseline.

## Key Features
- Hierarchical aggregation (dept+store → item level forecasting)
- XGBoost regression model, with Tweedie loss for zero-inflated sales data
- Stockout-aware training data cleaning
- Sample weighting to emphasize recent observations
- Price momentum and lag-based demand features

## Results
- **Aggregate wMAPE:** 8.89% (dept+store level)
- **Item-level RMSE:** 2.24 units
- **Improvement:** 21.1% better than lag-28 naive baseline

## How to Run
1. Download M5 dataset from Kaggle
2. Update `DATA_DIR` path in the notebook/script
3. Run all cells sequentially

## Key Insights
- Hierarchical aggregation significantly improves stability of item-level forecasts
- Lag and date features capture strong seasonality
- Cleaning stockouts reduces artificial demand distortion
- Model performance is strongest at aggregated levels

## Author
Satya Rao — Supply Chain Professional (CSCP) focused on data-driven demand planning, forecasting, and decision analytics
