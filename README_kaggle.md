# Swat River & KPK Flood Prediction Dataset

This synthetic dataset is engineered based on historical reports, WAPDA discharge boundaries, and Pakistan Meteorological Department (PMD) trends for the Swat River basin. It is designed to train Machine Learning models (like Random Forests, XGBoost, or LSTMs) for flood forecasting.

## Files Included:
1. `historical_floods.csv`: Annual extreme events framework (2010-2026) capturing major peak flows like the 2010 and 2022 super-floods.
2. `daily_hydro_met.csv`: Continuous daily time-series matrix (2024-2026) containing dynamic triggers (Rainfall, Temperature, Discharge, Water Level).
3. `basin_geospatial_features.csv`: Static spatial parameters capturing vulnerability metrics across upper, middle, and lower sub-basins.

## Features Guide for Models:
- Use `Daily_Rainfall_mm` and `Avg_Temperature_C` as predictive features.
- Target variables: `River_Discharge_Cusecs` (Regression) or `Flood_Label` (Classification).
