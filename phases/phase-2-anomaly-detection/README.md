# Phase 2 — Anomaly Detection & Alerting

**Duration:** Month 3 | **Capstone output:** Module 1 — live anomaly detector on Prometheus

## Theory

### Why Static Thresholds Fail

Static thresholds (`alert if CPU > 80%`) cause alert fatigue because:
- Normal peaks (deployments, batch jobs, traffic spikes) trigger false positives
- Gradual degradation below threshold goes undetected
- Every service has different "normal" — one threshold doesn't fit all

### Dynamic Thresholding Methods

**Bollinger Bands:** Rolling mean ± k×rolling_std. Simple and effective for stable services.
```python
window = 60  # 60-minute rolling window
mean = series.rolling(window).mean()
std  = series.rolling(window).std()
upper_band = mean + 3 * std
lower_band = mean - 3 * std
anomaly = (series > upper_band) | (series < lower_band)
```

**Holt-Winters (Exponential Smoothing):** Handles trend and seasonality with exponential weights. Better than Bollinger Bands when your metric has a clear daily cycle.
```python
from statsmodels.tsa.holtwinters import ExponentialSmoothing
model = ExponentialSmoothing(series, trend='add', seasonal='add', seasonal_periods=1440)
fit = model.fit()
forecast = fit.fittedvalues
residuals = series - forecast
anomaly = residuals.abs() > (3 * residuals.std())
```

**Isolation Forest:** Learns what "normal" looks like from a training window. No need to specify thresholds. Best when you have multiple correlated metrics as features.

**LSTM Autoencoder:** Learns to reconstruct normal sequences. High reconstruction error = anomaly. Use when simpler methods miss anomalies in complex multi-variate patterns. Only reach for this if Isolation Forest is insufficient.

### Severity Scoring

Don't output binary anomaly/not-anomaly. Score each anomaly:
```python
# Normalize isolation score to 0–1 severity
raw_score = clf.score_samples(X)           # more negative = more anomalous
severity  = 1 - (raw_score - raw_score.min()) / (raw_score.max() - raw_score.min())
```

## Open-Source Projects to Study

| Project | What to look at |
|---|---|
| [Luminol](https://github.com/linkedin/luminol) | `luminol/algorithms/` — how LinkedIn implements bitmap and derivative algorithms |
| [Alibi-Detect](https://github.com/SeldonIO/alibi-detect) | `alibi_detect/od/iforest.py` — production Isolation Forest wrapper |
| [Prometheus Anomaly Detector](https://github.com/AICoE/prometheus-anomaly-detector) | `app.py` — how to query Prometheus API and feed results to ML |

Spend 1–2 hours reading each codebase before starting Module 1.

## Proceed to Practice

→ [Module 1: Build the Live Anomaly Detector](practice/module-1-anomaly-detector.md)
