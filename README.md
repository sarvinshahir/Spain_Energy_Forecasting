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


# ⚡ Spain Energy Demand Forecasting (2015–2018)

**Author:** Sarvin Shahir  
**Program:** M.S. in Data Analytics Engineering, Northeastern University (Vancouver)

---

## 🧩 Overview
This project forecasts **Spain’s hourly electricity demand** using four years of generation, weather, and market data.  
The work compares **traditional statistical models** with **deep learning architectures** to understand which methods best capture short-term load behavior.

Accurate demand forecasting plays a key role in grid stability, renewable energy integration, and efficient system planning.

---

## 🎯 Objectives
- Build models to forecast **hourly total electrical load**.  
- Compare multiple forecasting approaches:
  - Linear Regression  
  - ARIMA  
  - SARIMAX  
  - Simple RNN  
  - LSTM  
  - GRU  
- Evaluate models using standard forecasting metrics.  
- Analyze insights and limitations for real-world forecasting scenarios.

---

## 📊 Dataset

### **Sources**
- **ENTSOE Transparency Platform** — generation + load  
- **Red Eléctrica de España (REE)** — pricing + forecasts  
- **OpenWeather API** — weather profiles for Madrid, Barcelona, Valencia, Seville, Bilbao  

### **Final Dataset Description**
- **35,064 hourly rows**  
- **26 numerical features + datetime**  
- **Target:** `total load actual` (MW)  
- Strong daily, weekly, and seasonal patterns  

### **Features Include**
- Renewable & fossil fuel generation  
- Nuclear and hydro generation  
- Weather: temperature, humidity, wind speed, pressure, rainfall  
- Day-ahead load and price forecasts  

---

## 🛠️ Methodology

### 1️⃣ **Data Preparation**
- Converted timestamps and aligned all datasets  
- Dropped missing values and all-zero generation columns  
- Forward-filled small gaps  
- Merged energy + weather data by timestamp  
- Normalized features with `MinMaxScaler`  
- Created **24-hour lookback sequences** for deep learning models  
- Used an **80/20 sequential split** to preserve time order  

---

### 2️⃣ **Model Development**

#### **Traditional Models**
- **Linear Regression**  
- **ARIMA (2,1,2)**  
- **SARIMAX (1,1,1)(1,0,1,7)** with full exogenous feature set  

#### **Deep Learning Models**
All models use:
- 24-hour window  
- 64 hidden units  
- `Dense(32, relu)` + `Dense(1)` output  
- Adam optimizer, 20–50 epochs  

Models implemented:
- **Simple RNN**  
- **LSTM**  
- **GRU**  

Early stopping applied in selected experiments.

---

## 📏 Evaluation Metrics
- **MAE — Mean Absolute Error**  
- **RMSE — Root Mean Squared Error**  
- **MAPE — Mean Absolute Percentage Error**  
- **R² — Coefficient of Determination**  

---

## 📈 Results Summary

| Model | MAE | RMSE | MAPE | R² | Notes |
|-------|------:|------:|------:|------:|------|
| **Linear Regression** | 1178.7 | 1485.6 | 4.22% | 0.892 | Good baseline |
| **ARIMA** | 2421.3 | 3127.3 | 9.02% | -0.423 | Fits poorly; over-smoothing |
| **SARIMAX** | 2139.1 | 2558.8 | 7.59% | 0.047 | Limited improvement |
| **Simple RNN** | ~340 | ~510 | ~1.20% | 0.987 | Very strong performance |
| **LSTM** | ~1109 | ~1402 | ~3.93% | 0.904 | Stable & robust |
| **GRU** | ~1130 | ~1430 | ~3.97% | 0.900 | Similar to LSTM; faster |

---

## ✅ Key Insights
- Deep learning models consistently outperform ARIMA-based models.  
- Simple RNN produced the **best accuracy**, likely because:
  - The dataset has strong daily structure  
  - The 24-hour window matches natural cycles  
  - The model is smaller → less overfitting  
- LSTM and GRU offered **better stability** but not necessarily lower error.  
- ARIMA and SARIMAX struggled with:
  - Strong nonlinear dependencies  
  - Multiple correlated exogenous variables  
  - Long seasonal cycles beyond their specification  

---

## 🚀 Future Work
- Implement a **Transformer-based** model to capture long-range dependencies  
- Add engineered calendar features (hour, weekday, holidays)  
- Try **feature selection or dimensionality reduction**  
- Build a **Streamlit forecasting dashboard**  
- Explore **multi-step (24-hour ahead)** forecasting  
- Forecast additional variables (renewables, pricing, net load)

---

## 📂 Repository Structure
📁 data/ → CSV files or download instructions
📁 notebooks/ → Model development notebooks
📄 README.md → Project overview
📄 requirements.txt → Python dependencies


