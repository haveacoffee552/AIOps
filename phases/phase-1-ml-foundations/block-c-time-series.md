# Block C — Time Series Analysis

**Duration:** Week 6–8 | **Focus:** STL, SARIMA, Prophet, anomaly on time series

## Why Time Series Is Different

Standard ML assumes samples are i.i.d. (independent and identically distributed). Time series data is neither — each point depends on its neighbors, and there are seasonal patterns (daily, weekly) that must be modeled, not treated as noise.

## Key Concepts

**Stationarity:** A time series is stationary when its mean and variance don't change over time. Most ML models assume stationarity. You must check for it and transform if needed.

```python
from statsmodels.tsa.stattools import adfuller

result = adfuller(df['cpu_usage'].dropna())
print(f"ADF Statistic: {result[0]:.4f}")
print(f"p-value: {result[1]:.4f}")
# p < 0.05 = stationary (good). p > 0.05 = non-stationary, apply differencing.
```

## STL Decomposition

Separates a time series into Trend + Seasonal + Residual components. The residual is what you run anomaly detection on — after removing expected patterns.

```python
from statsmodels.tsa.seasonal import STL

stl = STL(df['cpu_usage'], period=1440)  # 1440 = minutes per day for 1-min data
result = stl.fit()

trend    = result.trend
seasonal = result.seasonal
residual = result.resid

# Anomaly detection on the residual (actual surprise, not seasonal spike)
from sklearn.ensemble import IsolationForest
iso = IsolationForest(contamination=0.01, random_state=42)
anomalies = iso.fit_predict(residual.values.reshape(-1,1))
```

## SARIMA (Seasonal ARIMA)

Use SARIMA when you have stationary data (or near-stationary after differencing) and need short-horizon forecasts (<24h). It is more interpretable than Prophet for data without strong weekly seasonality.

```python
from statsmodels.tsa.statespace.sarimax import SARIMAX

# SARIMA(p,d,q)(P,D,Q,s) where s = seasonal period
# For 1-minute data with hourly seasonality: s=60
model = SARIMAX(series,
    order=(1, 1, 1),         # (AR, differencing, MA)
    seasonal_order=(1, 1, 1, 60),  # seasonal (AR, diff, MA, period)
    enforce_stationarity=False,
    enforce_invertibility=False
)
result = model.fit(disp=False)

# Forecast 60 minutes ahead
forecast = result.get_forecast(steps=60)
forecast_mean = forecast.predicted_mean
confidence_intervals = forecast.conf_int()

# Values outside the 95% CI are anomalies
print(f"Forecast: {forecast_mean.iloc[-1]:.2f}")
```

**When to prefer SARIMA over Prophet:**
- Your data has no weekly pattern (intra-day only)
- You need a forecast horizon under 6 hours
- You want explicit model order control (interpretability)

**Limitation:** SARIMA is sensitive to parameter selection (p, d, q). Use `auto_arima` from the `pmdarima` library to search for optimal parameters:
```bash
pip install pmdarima
```
```python
from pmdarima import auto_arima
model = auto_arima(series, seasonal=True, m=60, stepwise=True, suppress_warnings=True)
```

## Facebook Prophet

Business-friendly forecasting. Handles daily/weekly/yearly seasonality automatically. Returns a forecast with uncertainty intervals — use the interval to flag anomalies.

```python
from prophet import Prophet
import pandas as pd

# Prophet requires columns named 'ds' (datetime) and 'y' (value)
df_prophet = df[['cpu_usage']].reset_index()
df_prophet.columns = ['ds', 'y']

m = Prophet(
    changepoint_prior_scale=0.05,   # sensitivity to trend changes
    seasonality_mode='multiplicative'
)
m.fit(df_prophet)

future = m.make_future_dataframe(periods=60, freq='min')  # forecast 1 hour ahead
forecast = m.predict(future)

# Flag actuals outside the 95% uncertainty interval as anomalies
merged = df_prophet.merge(forecast[['ds','yhat','yhat_lower','yhat_upper']], on='ds')
merged['anomaly'] = (merged['y'] < merged['yhat_lower']) | (merged['y'] > merged['yhat_upper'])
```

## Comparing Anomaly Detection Approaches

| Method | Best For | Weakness |
|---|---|---|
| Z-score | Fast baseline, stationary data | Fails with seasonality |
| IQR | Robust to outliers in baseline | Same seasonality problem |
| STL + Isolation Forest | Seasonal data (metrics) | Needs enough history for STL |
| Prophet | Forecasting + anomaly | Slow to train, needs weeks of data |
| LSTM Autoencoder | Complex multivariate patterns | High complexity, slow |

## Practice Exercise — Numenta Anomaly Benchmark (NAB)

1. Download NAB: `git clone https://github.com/numenta/NAB`
2. Load `realKnownCause/machine_temperature_system_failure.csv`
3. Apply STL decomposition, plot the three components
4. Run z-score on the residual → compute F1 against NAB's ground truth labels
5. Run Isolation Forest on the residual → compare F1
6. Run Prophet on the full series → compare F1

**Done when:** You have a comparison table showing F1 for each method, and you can explain *why* one method outperforms the others on this specific dataset.
