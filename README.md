# Predicting_Ion_Battery_Life

## Project Overview
This project focuses on predicting the Remaining Useful Life (RUL) of lithium-ion batteries using advanced feature engineering and machine learning models. The workflow covers data preprocessing, feature engineering, model training, evaluation, and visualization.

---

## Dataset
- ~7,565 CSV files with alternating measurement types:
  - Voltage, Current, Temperature, Load, Time
  - Sense Current, Battery Current, Current Ratio, Battery Impedance, Rectified Impedance
- Metadata CSV with columns:
  - `Cycle`, `Capacity`, `Re`, `Rct`, `RUL`, `Type`, `Start_time`, `Ambient_temperature`, `Battery_id`, `Test_id`, `UID`, `Filename`

---

## Data Preprocessing
- Load raw discharge metadata from CSV
- Compute Remaining Useful Life (RUL)
- Filter valid discharge cycles
- Create target labels for ML models

---

## Feature Engineering

### Basic Features
- **Time-Domain:** Voltage/Current/Temperature mean, cycle duration, normalized capacity ratio
- **Impedance-Domain:** Mean, std, max, min impedance per cycle, rate of change in impedance

### Advanced Features
- **Degradation Trends:** Capacity/current trends, moving averages, normalized rates
- **Lag Features:** Lag values for voltage, impedance, capacity, etc.
- **Smoothed & Delta Features:** Rolling mean/std/min/max, EMA, cycle-to-cycle deltas, trend direction
- **Power & Efficiency:** Instantaneous power, energy per cycle, cumulative energy, efficiency metrics
- **Interaction Features:** Health index, cross-domain ratios (e.g., capacity/impedance, voltage/impedance)

---

## Model Training & Evaluation

### Models Used
- **Linear Regression:** Baseline model for RUL prediction.
- **Random Forest Regressor:** Ensemble model, robust to feature interactions and non-linearities.
- **Gradient Boosting Regressor:** Sequential ensemble model for improved accuracy.
- **XGBoost Regressor:** Optimized gradient boosting, handles large datasets efficiently.
- **LightGBM Regressor:** Fast, efficient gradient boosting for large-scale data.

### Training Workflow
- Split data into train, validation, and test sets
- Scale features using StandardScaler
- Train each model on the training set
- Evaluate on validation set using Mean Squared Error (MSE) and Mean Absolute Error (MAE)
- Select best model based on validation metrics

### Final Evaluation
- Test best model on the test set
- Save predictions to `rul_predictions.csv`
- Visualize results in a dedicated notebook

---

## Visualization

- **Actual vs Predicted RUL:** Scatter plot to compare model predictions with ground truth.
- **Residuals Histogram:** Distribution of prediction errors.
- **Residuals vs Actual RUL:** Error trends across RUL range.

---

## Results

- **Best Model:** Random Forest achieved near-perfect R² and very low MAE/MSE.
- **Feature Importance:** Only a few features (e.g., `RUL_x`, `capacity_per_cycle_impedance`) were highly predictive.
- **Visualizations:** Plots show accurate predictions and small, unbiased residuals.

---

## Goal
Predict battery Remaining Useful Life (RUL) before the capacity falls below 80% of initial capacity.

---

## How to Run

1. Clone the repository.
2. Install dependencies:
   ```
   pip install -r requirements.txt
   ```
3. Run notebooks in order:
   - Data preprocessing
   - Feature engineering
   - Model training
   - Model evaluation
   - Visualization

---

## Requirements

- Python 3.8+
- pandas, numpy, scikit-learn, matplotlib, seaborn, xgboost, lightgbm

---

## Credits

- NASA Prognostics Data Repository
- Scikit-learn, XGBoost, LightGBM

---

## License

MIT License

---

## Reference

Dataset: [Kaggle - NASA Battery Dataset](https://www.kaggle.com/datasets/patrickfleith/nasa-battery-dataset)