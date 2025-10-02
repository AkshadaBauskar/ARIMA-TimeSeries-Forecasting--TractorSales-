# ARIMA Time Series Forecasting – Tractor Sales & Marketing Impact Analysis  

## Problem statemnet  

This project began with a real-world business problem: PowerHorse, a tractor and farm equipment manufacturer, wanted to better understand and forecast its sales. While the company had experienced steady growth over the years, unpredictable fluctuations in sales were creating challenges in production planning, inventory management, and cost control.  
On top of that, management wanted to evaluate whether their marketing spend was actually driving sales or simply adding to costs without measurable returns.  

My goal was to create a solution that could:  
- Reliably forecast tractor sales for the next three years.  
- Quantify the true impact of marketing expenditure on sales.  
- Translate the results into actionable business insights.  

## Data and Preparation  

I was provided with 12 years of monthly tractor sales data from PowerHorse’s MIS team, along with 4 years of marketing expenditure data.  

To prepare the data for modeling, I:  
- Converted the records into a **time-indexed dataset**.  
- Extracted relevant date features (month, year).  
- Handled missing values and applied **log transformations** to stabilize variance.  
- Performed **differencing** to achieve stationarity, which is crucial for ARIMA models.  
This preprocessing ensured that the time series was suitable for advanced statistical modeling.  


## Exploratory Analysis  

Visual exploration immediately revealed two important patterns:  
- Trend: Tractor sales showed a strong upward trajectory over time.  
- Seasonality: Annual cycles emerged clearly, with peaks in consistent months year after year.  

By decomposing the series into **trend, seasonality, and residuals**, I validated these patterns and confirmed that ARIMA (with seasonal extensions) was a strong candidate for forecasting.  

## Building the Forecasting Model  

I followed a step-by-step process to develop the ARIMA model:  

1. **Stationarity testing** (ADF test, rolling statistics).  
2. **ACF and PACF analysis** to identify potential AR and MA terms.  
3. **Grid search of parameters (p,d,q)(P,D,Q)[s]** using the SARIMAX implementation from `statsmodels`.  
4. **Model selection based on AIC/BIC criteria**.  
The best performing model turned out to be **ARIMA(0,1,1)(1,0,1)[12]**, which successfully captured both the trend and seasonal structure of the data.  
Residual diagnostics confirmed that the model errors resembled white noise, meaning the model had captured most of the structure in the data.  

## Forecasting Results  

With the chosen ARIMA model, I generated forecasts for the next **36 months (3 years)**.  

- The forecasts followed the seasonal and upward trend seen historically.  
- **Confidence intervals (95% and 99%)** were added to quantify uncertainty.  
- The results demonstrated that while **short-term forecasts were very reliable**, longer horizons carried more uncertainty — highlighting the need for **periodic model retraining**.  

For PowerHorse, this meant they could plan production and inventory with greater confidence, especially in the short to medium term.  

## Marketing Impact Analysis  

An additional layer of analysis involved assessing the effectiveness of marketing expenditure on tractor sales.  

At first glance, sales and marketing spend showed a high correlation (>0.8). However, after adjusting for growth trends, the correlation dropped to around 0.41 — and when lag effects (1–3 months) were tested, the relationship weakened further.  

To quantify this formally, I extended the ARIMA model to an ARIMAX model, incorporating marketing expenditure as an exogenous regressor. The results were surprising:  

- Models without marketing spend performed better (lower AIC) than those including it.  
- This suggested that marketing spend did not have a significant effect on sales in this dataset.  

From a business standpoint, this meant that PowerHorse’s management should re-evaluate their marketing strategies, as current spending was not translating into measurable sales increases.  

---

## Key Insights  

- ✅ **Reliable Forecasts** – The ARIMA(0,1,1)(1,0,1)[12] model provided accurate forecasts and will support better inventory and production planning.  
- ✅ **Marketing Reassessment** – Marketing spend showed little predictive value in driving sales. This insight could save PowerHorse from unnecessary expenditure.  
- ✅ **Business Value** – Forecasting is not just a technical exercise. When aligned with business needs, it can deliver tangible savings, operational efficiency, and strategic clarity.  

---

## 🛠 Tools and Technologies  

- **Python**: Pandas, NumPy, Matplotlib, Seaborn  
- **Statsmodels**: ARIMA, SARIMAX implementation  
- **pmdarima**: Automated parameter tuning  
- **Scikit-learn**: Model evaluation and metrics  
- **Jupyter Notebook**: Development environment for analysis  

---

## 🚀 How to Run the Project  

Clone this repository:  
```bash
git clone https://github.com/AkshadaBauskar/ARIMA-TimeSeries-Forecasting--TractorSales-.git
cd ARIMA-TimeSeries-Forecasting--TractorSales-
