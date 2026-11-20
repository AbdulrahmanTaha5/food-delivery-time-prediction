# Food Delivery Time Prediction

## Problem & Goal
Delivery durations vary across trips due to distance, preparation time, traffic, weather, time of day, vehicle type, and courier experience.
This project predicts `Delivery_Time_min` (in minutes) to help operations teams estimate arrival windows and plan dispatch, while keeping final operational decisions with human staff.

## Dataset & How to Run
- Dataset: `Food_Delivery_Times.csv` (1,000 delivery records with trip, weather, traffic, and courier attributes).
- How to run:
  1. Open `delivery_time_prediction.ipynb` in Jupyter or Google Colab with `Food_Delivery_Times.csv` available in the working directory.
  2. Run all cells sequentially and save the notebook with outputs kept.

## Approach & Results
- Removed `Order_ID` and split the data into training (80%) and test (20%) sets prior to preprocessing so test data never leaks into imputation, scaling, or encoding.
- Compared a median baseline (`DummyRegressor`), `Ridge Regression`, and `Random Forest` using 5-fold cross-validation on training data, measured by **Mean Absolute Error (MAE)** in minutes.
- Selected `Ridge Regression` based on validation performance:
  - 5-fold CV MAE: ~6.77 min (vs. ~17.88 min baseline)
  - Test MAE: ~6.06 min (vs. ~17.46 min baseline), Test RMSE: ~8.95 min

## Limitations & Risks
- Missing values occur in `Weather`, `Traffic_Level`, `Time_of_Day`, and `Courier_Experience_yrs` (30 rows each) and are imputed from training data; missingness patterns could shift over time.
- Model estimates can have larger errors on unusual or peak/adverse cases and should support rather than replace human judgment.
