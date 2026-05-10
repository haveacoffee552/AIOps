# Module 4 — Saturation Forecaster

**Capstone file:** `aiops-platform/modules/capacity_planner/`

## What You're Building

A pipeline that fetches 90 days of Prometheus history, trains a Prophet model per metric, forecasts 72 hours ahead, detects when any resource will hit saturation, and writes a proactive alert.

## File Structure

```
aiops-platform/modules/capacity_planner/
├── history_fetcher.py    # Fetch 90 days from Prometheus
├── forecaster.py         # Prophet model training + forecasting
├── saturation.py         # Detect when forecast crosses threshold
└── main.py
```

## Step 1: history_fetcher.py

```python
# aiops-platform/modules/capacity_planner/history_fetcher.py
import requests
import pandas as pd
from datetime import datetime, timedelta

PROMETHEUS_URL = "http://localhost:9090"

def fetch_history(query: str, days: int = 90) -> pd.DataFrame:
    """Fetch metric history. Returns DataFrame with columns: ds (datetime), y (float)."""
    end   = datetime.utcnow()
    start = end - timedelta(days=days)
    resp  = requests.get(f"{PROMETHEUS_URL}/api/v1/query_range", params={
        "query": query,
        "start": start.isoformat() + "Z",
        "end":   end.isoformat() + "Z",
        "step":  "3600",    # 1-hour resolution for 90 days
    })
    resp.raise_for_status()
    result = resp.json()["data"]["result"]
    if not result:
        return pd.DataFrame(columns=["ds", "y"])
    values = result[0]["values"]
    return pd.DataFrame({
        "ds": [datetime.utcfromtimestamp(float(t)) for t, _ in values],
        "y":  [float(v) for _, v in values],
    })
```

## Step 2: forecaster.py

```python
# aiops-platform/modules/capacity_planner/forecaster.py
import pandas as pd
from prophet import Prophet

def train_and_forecast(df: pd.DataFrame, horizon_hours: int = 72) -> pd.DataFrame:
    """
    Train Prophet on historical data. Return forecast DataFrame with
    columns: ds, yhat, yhat_lower, yhat_upper.
    """
    if df.empty or len(df) < 48:    # need at least 48 hours of hourly data
        return pd.DataFrame()

    m = Prophet(
        changepoint_prior_scale=0.05,
        seasonality_mode='multiplicative',
        daily_seasonality=True,
        weekly_seasonality=True,
    )
    m.fit(df)

    future   = m.make_future_dataframe(periods=horizon_hours, freq='h')
    forecast = m.predict(future)
    return forecast[["ds", "yhat", "yhat_lower", "yhat_upper"]]
```

## Step 3: saturation.py

```python
# aiops-platform/modules/capacity_planner/saturation.py
import pandas as pd
import json
from pathlib import Path
from datetime import datetime

ALERTS_FILE = Path("aiops-platform/data/alerts.jsonl")

THRESHOLDS = {
    "cpu_usage":        80.0,   # percent
    "mem_used_percent": 85.0,   # percent
    "disk_used_percent": 90.0,  # percent
}

def check_saturation(metric_name: str, forecast: pd.DataFrame) -> list[dict]:
    """Return list of proactive alerts for forecast points crossing threshold."""
    threshold = THRESHOLDS.get(metric_name)
    if threshold is None or forecast.empty:
        return []

    future_only = forecast[forecast["ds"] > datetime.utcnow()]
    crossing    = future_only[future_only["yhat"] >= threshold]
    if crossing.empty:
        return []

    first_crossing = crossing.iloc[0]
    hours_away = (first_crossing["ds"] - datetime.utcnow()).total_seconds() / 3600

    return [{
        "type":            "proactive",
        "metric":          metric_name,
        "predicted_value": float(first_crossing["yhat"]),
        "threshold":       threshold,
        "eta_hours":       round(hours_away, 1),
        "timestamp":       first_crossing["ds"].isoformat(),
        "severity":        1.0 if hours_away < 6 else 0.6,
        "detected_at":     datetime.utcnow().isoformat(),
    }]

def write_proactive_alerts(alerts: list[dict]) -> None:
    ALERTS_FILE.parent.mkdir(parents=True, exist_ok=True)
    with open(ALERTS_FILE, "a") as f:
        for a in alerts:
            f.write(json.dumps(a) + "\n")
```

## Step 4: main.py

```python
# aiops-platform/modules/capacity_planner/main.py
from history_fetcher import fetch_history
from forecaster      import train_and_forecast
from saturation      import check_saturation, write_proactive_alerts

METRICS = [
    ("100 - (avg(rate(node_cpu_seconds_total{mode='idle'}[5m])) * 100)", "cpu_usage"),
    ("100 * (1 - node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)",  "mem_used_percent"),
]

def run():
    for query, name in METRICS:
        print(f"Fetching 90 days of {name}...")
        df       = fetch_history(query, days=90)
        forecast = train_and_forecast(df, horizon_hours=72)
        alerts   = check_saturation(name, forecast)
        if alerts:
            write_proactive_alerts(alerts)
            for a in alerts:
                print(f"PROACTIVE: {name} will hit {a['threshold']}% in {a['eta_hours']}h")
        else:
            print(f"{name}: no saturation predicted in 72h")

if __name__ == "__main__":
    run()
```

## Step 5: Commit to capstone repo

```bash
cd aiops-platform
pip install prophet
git add modules/capacity_planner/ data/
git commit -m "feat(module-4): saturation forecaster with Prophet and proactive alerting"
```

## Done When

- [ ] `main.py` runs against 90 days of Prometheus history
- [ ] Forecast plot (Prophet's `plot()`) shows a plausible trend for your infrastructure
- [ ] At least one proactive alert is generated (or you can explain why saturation is not predicted)
- [ ] You can explain the difference between `yhat` and `yhat_upper` and when to use each for alerting
