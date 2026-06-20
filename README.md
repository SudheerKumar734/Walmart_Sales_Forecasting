# 🛒 Walmart Weekly Sales Forecasting

A time series forecasting project that analyzes historical Walmart sales data to uncover key business drivers and predict future weekly sales at the individual store level using SARIMAX.

![Python](https://img.shields.io/badge/Python-3.10-blue)
![Status](https://img.shields.io/badge/Status-Completed-success)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## 📌 Overview

Walmart operates 45 stores, each shaped differently by seasonality, holidays, and macroeconomic conditions like unemployment and inflation. This project:

- Performs exploratory data analysis (EDA) to uncover the key drivers of weekly sales
- Builds a parallelized SARIMAX forecasting pipeline to predict the next 12 weeks of sales per store
- Exports forecast results to a multi-sheet Excel report for stakeholder use

---

## 📊 Dataset

| Attribute | Details |
|---|---|
| Records | 6,435 weekly observations |
| Stores | 45 |
| Time span | 2010 – 2012 |
| Features | Store, Date, Weekly_Sales, Holiday_Flag, Temperature, Fuel_Price, CPI, Unemployment |
| Missing values | None |

---

## 🔍 Key EDA Insights

- **Seasonality:** Sales spike sharply in **November–December**, driven by Thanksgiving, Christmas, and New Year shopping.
- **Unemployment impact:** Stores 38 (-0.785) and 44 (-0.780) show the strongest negative correlation between sales and local unemployment.
- **CPI impact:** Store 36 shows a striking -0.915 correlation with CPI — sales fall sharply as cost of goods rises.
- **Temperature:** Virtually no effect on sales (correlation: -0.064).
- **Store performance gap:** Best store (Store 20: $2.1M/week avg) outsells the worst (Store 33: $260K/week avg) by ~88%.

---

## 🧠 Methodology

1. **Preprocessing** — Parsed dates, set time-series index, resampled to weekly totals per store.
2. **EDA** — Correlation analysis, seasonal decomposition, holiday vs. non-holiday comparison.
3. **Modeling** — `SARIMAX(0,1,1)x(0,1,1,52)` to capture annual seasonality in weekly sales.
4. **Validation** — Last 12 weeks held out as test set; evaluated using RMSE and MAPE.
5. **Forecasting** — Refit on full series to generate a 12-week-ahead forecast per store.
6. **Parallelization** — Used `joblib` (loky backend) to fit multiple store models concurrently.
7. **Reporting** — Exported actual-vs-forecast and future forecasts to Excel via `XlsxWriter`.

---

## 📈 Forecast Results (12-Week Test Period)

| Store | RMSE | MAPE | Accuracy |
|---|---|---|---|
| 33 | 9,140.62 | 2.97% | High |
| 44 | 13,192.63 | 3.13% | High |
| 5 | 12,240.85 | 2.61% | High |
| 36 | 27,825.47 | 8.38% | Moderate |
| 38 | 22,128.21 | 3.65% | High |

> 4 of 5 stores achieved MAPE under 4%, indicating strong forecast reliability.

---

## 🛠️ Tech Stack

- **Language:** Python
- **Data Handling:** Pandas, NumPy
- **Visualization:** Matplotlib, Seaborn
- **Time Series Modeling:** Statsmodels (SARIMAX, seasonal_decompose)
- **Evaluation:** Scikit-learn
- **Parallel Processing:** Joblib
- **Reporting:** XlsxWriter
- **Environment:** Jupyter Notebook / Google Colab

---

## 📂 Project Structure

Walmart_Sales_Forecasting/

│

├── Walmart.csv              # Raw dataset

├── Wallmart_Sales_Forecasting.ipynb            # Main notebook (EDA + forecasting)

├── sales_forecast_report.xlsx       # Generated forecast report

├── Wallmart_Sales_Forecasting_PP.pdf      #Power Point Presentation (PDF)

├── Wallmart_Sales_Forecasting_Project_Report.docx

└── README.md

---

## 🚀 How to Run

```bash
git clone https://github.com/<your-username>/walmart-sales-forecasting.git
cd walmart-sales-forecasting
pip install pandas numpy matplotlib seaborn statsmodels scikit-learn joblib xlsxwriter
jupyter notebook final_projectWM.ipynb
```

---

## 💡 Future Improvements

- Extend forecasting to all 45 stores instead of a 5-store sample
- Automate rolling monthly re-forecasting
- Add a Power BI/Streamlit dashboard for interactive forecast exploration
- Incorporate additional exogenous regressors (e.g., regional promotions)

---

## 👤 Author

**Sudheer Kumar**
Data Analyst / Data Scientist | [LinkedIn](https://linkedin.com/in/sudheer-kumar-b202871a4) | [GitHub](https://github.com/SudheerKumar734)
