# Block A — Python for Data

**Duration:** Week 1–2 | **Focus:** NumPy, Pandas, Matplotlib with time series data

## Why This Matters for AIOps

Your metrics are time series. Your logs are sequences of strings. Before any ML, you need to load, reshape, and visualize this data fluently. Pandas is the lingua franca for this work.

## NumPy Essentials

The only NumPy you need for AIOps:

```python
import numpy as np

# Arrays
arr = np.array([1.0, 2.0, 3.0])
arr.mean()       # 2.0
arr.std()        # standard deviation
arr.min(), arr.max()

# Operations used constantly in anomaly detection
z_scores = (arr - arr.mean()) / arr.std()

# Rolling window (manual, before you learn Pandas)
window = 5
rolling_mean = np.convolve(arr, np.ones(window)/window, mode='valid')
```

## Pandas for Time Series

```python
import pandas as pd

# Load a CSV Prometheus export
# Typical format: timestamp, metric_name, value, labels
df = pd.read_csv('prometheus_export.csv', parse_dates=['timestamp'])
df = df.set_index('timestamp').sort_index()

# Resample to 1-minute intervals
df_1m = df['cpu_usage'].resample('1min').mean()

# Rolling statistics — the foundation of many AIOps baselines
rolling_mean = df_1m.rolling(window=60).mean()    # 1-hour rolling mean
rolling_std  = df_1m.rolling(window=60).std()

# Lag features — used in time series ML
df['lag_1']  = df['cpu_usage'].shift(1)
df['lag_60'] = df['cpu_usage'].shift(60)

# Boolean indexing — find spikes
spikes = df[df['cpu_usage'] > (rolling_mean + 3 * rolling_std)]
```

## Matplotlib for Ops Visualization

```python
import matplotlib.pyplot as plt

fig, axes = plt.subplots(2, 1, figsize=(14, 6), sharex=True)

# Top: raw metric with rolling mean
axes[0].plot(df.index, df['cpu_usage'], alpha=0.5, label='CPU %')
axes[0].plot(df.index, rolling_mean, color='red', label='60-min mean')
axes[0].fill_between(df.index,
    rolling_mean - 3*rolling_std,
    rolling_mean + 3*rolling_std,
    alpha=0.2, label='3σ band')
axes[0].legend()
axes[0].set_title('CPU Usage with Dynamic Threshold')

# Bottom: z-score
z = (df['cpu_usage'] - rolling_mean) / rolling_std
axes[1].plot(df.index, z, color='orange')
axes[1].axhline(3, color='red', linestyle='--', label='3σ threshold')
axes[1].set_title('Z-Score')
axes[1].legend()

plt.tight_layout()
plt.savefig('cpu_analysis.png', dpi=150)
```

## Practice Exercise

**Goal:** Load real Prometheus data, plot it, identify outliers visually.

1. Export 7 days of CPU, memory, and request rate data from your Prometheus via:
   ```
   http://localhost:9090/api/v1/query_range?query=node_cpu_seconds_total&start=...&end=...&step=60
   ```
   Save as CSV.

2. Load into Pandas, resample to 1-minute intervals, plot all three metrics.

3. Compute 1-hour rolling mean and 3σ bands for CPU. Mark where CPU exceeded the band.

4. Answer these questions by looking at the chart:
   - Is the CPU pattern seasonal (daily/weekly cycle)?
   - Are outliers correlated with request rate spikes?
   - What does "normal" look like for your service?

**Done when:** You have a saved `cpu_analysis.png` and can answer the 3 questions above.
