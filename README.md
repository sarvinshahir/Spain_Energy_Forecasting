# ⚡ Spain Energy Demand Forecasting (2015–2018)

**Author:** Sarvin Shahir  
**Program:** M.S. in Data Analytics Engineering, Northeastern University (Vancouver)  

---

## 🧩 Overview
This project forecasts **Spain’s hourly electricity demand** using energy generation, weather, and market data.  
It evaluates the performance of **traditional statistical models** and **deep learning architectures** to improve forecasting accuracy and support renewable energy integration.

Forecasting energy demand accurately helps utilities and policymakers enhance grid stability, optimize renewable generation, and reduce operational costs.

---

## 🎯 Objectives
- Forecast hourly total electrical demand using historical weather and generation data.  
- Compare traditional and deep learning models:
  - Linear Regression  
  - ARIMA / SARIMAX  
  - Recurrent Neural Network (RNN)  
  - Long Short-Term Memory (LSTM)
- Evaluate and interpret model performance using standard forecasting metrics.  

---

## 📊 Dataset
Data covers **2015–2018**, combining multiple open sources:
- **ENTSOE Transparency Platform** — energy generation and consumption data.  
- **Red Eléctrica de España (REE)** — day-ahead pricing and load forecasts.  
- **OpenWeather API** — hourly weather data for Spain’s five largest cities (Madrid, Barcelona, Valencia, Seville, Bilbao).  

Each record represents **hourly data** with 26 numerical variables and one datetime index.  
Key variables include:
- Energy generation by source (fossil, renewable, nuclear)
- Weather (temperature, humidity, wind speed, pressure, rainfall)
- Total load and day-ahead forecasts

---

## 🧮 Methodology
1. **Data Preparation**
   - Converted timestamps and aligned across all data sources.
   - Cleaned missing or invalid values and removed all-zero columns.
   - Merged weather and energy data on hourly timestamps.
   - Normalized numeric features for model training.

2. **Model Development**
   - Trained multiple forecasting models to predict hourly total load.  
   - Benchmarked traditional (ARIMA, Linear Regression) vs. deep learning (RNN, LSTM).  
   - Used an 80/20 train-test split with sequential ordering to preserve time dependencies.

3. **Evaluation Metrics**
   - MAE — Mean Absolute Error  
   - RMSE — Root Mean Squared Error  
   - MAPE — Mean Absolute Percentage Error  
   - R² — Coefficient of Determination  

---

## 📈 Results Summary

| Model | MAE | RMSE | MAPE | R² | Notes |
|:------|-----:|-----:|-----:|----:|:------|
| **Linear Regression** | 1,178.7 | 1,485.6 | 4.22% | 0.892 | Strong baseline |
| **ARIMA (hourly)** | 2,421.3 | 3,127.3 | 9.02% | -0.423 | Poor fit; over-smoothed |
| **SARIMAX (daily)** | 2,139.1 | 2,558.8 | 7.59% | 0.047 | Weak improvement |
| **RNN** | 324.1 | 500.8 | 1.14% | 0.988 | Excellent accuracy; minor overfit |
| **LSTM** | **475.2** | **643.5** | **1.67%** | **0.980** | Best overall generalization |

✅ **Key Takeaway:**  
Deep learning architectures (especially LSTM) outperform classical methods by effectively learning nonlinear temporal relationships between load, weather, and generation.



