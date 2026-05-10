# Module 1 — Live Anomaly Detector on Prometheus

**Capstone file:** `aiops-platform/modules/anomaly_detector/`

## What You're Building

A service that queries Prometheus every minute, detects anomalies using a rolling Isolation Forest, and outputs severity-scored alerts to a JSON file (later: to a database).

## File Structure

```
aiops-platform/modules/anomaly_detector/
├── collector.py      # Query Prometheus API, return DataFrame
├── detector.py       # Isolation Forest with rolling training window
├── scorer.py         # Normalize raw scores to 0–1 severity
├── alerter.py        # Format and write alerts to JSON
└── main.py           # Orchestrate: collect → detect → score → alert
```

## Step 0: Install dependencies

```bash
pip install requests scikit-learn pandas
```

## Step 1: collector.py

```python
# aiops-platform/modules/anomaly_detector/collector.py
import requests
import pandas as pd
from datetime import datetime, timedelta

PROMETHEUS_URL = "http://localhost:9090"

def fetch_metric(query: str, minutes: int = 60) -> pd.Series:
    """Fetch the last `minutes` of a Prometheus metric. Returns a float Series indexed by datetime."""
    end = datetime.utcnow()
    start = end - timedelta(minutes=minutes)
    resp = requests.get(f"{PROMETHEUS_URL}/api/v1/query_range", params={
        "query": query,
        "start": start.isoformat() + "Z",
        "end": end.isoformat() + "Z",
        "step": "60",
    })
    resp.raise_for_status()
    result = resp.json()["data"]["result"]
    if not result:
        return pd.Series(dtype=float)
    values = result[0]["values"]
    index = [datetime.utcfromtimestamp(float(t)) for t, _ in values]
    data  = [float(v) for _, v in values]
    return pd.Series(data, index=index)
```

## Step 2: detector.py

```python
# aiops-platform/modules/anomaly_detector/detector.py
import numpy as np
import pandas as pd
from sklearn.ensemble import IsolationForest

TRAINING_WINDOW = 1440  # 24 hours of 1-minute data points

def detect(series: pd.Series, contamination: float = 0.01) -> pd.DataFrame:
    """
    Train Isolation Forest on last TRAINING_WINDOW points.
    Return DataFrame with columns: timestamp, value, is_anomaly, raw_score.
    """
    if len(series) < 10:
        return pd.DataFrame()

    X = series.values.reshape(-1, 1)
    train_X = X[-TRAINING_WINDOW:] if len(X) > TRAINING_WINDOW else X

    clf = IsolationForest(contamination=contamination, random_state=42)
    clf.fit(train_X)

    predictions = clf.predict(X)
    raw_scores  = clf.score_samples(X)

    return pd.DataFrame({
        "timestamp": series.index,
        "value":     series.values,
        "is_anomaly": predictions == -1,
        "raw_score":  raw_scores,
    })
```

## Step 3: scorer.py

```python
# aiops-platform/modules/anomaly_detector/scorer.py
import pandas as pd
import numpy as np

def add_severity(df: pd.DataFrame) -> pd.DataFrame:
    """Add a 0–1 severity column. Only meaningful for anomaly rows."""
    if df.empty or "raw_score" not in df.columns:
        return df
    min_s, max_s = df["raw_score"].min(), df["raw_score"].max()
    if max_s == min_s:
        df["severity"] = 0.0
    else:
        df["severity"] = 1 - (df["raw_score"] - min_s) / (max_s - min_s)
    return df
```

## Step 4: alerter.py

```python
# aiops-platform/modules/anomaly_detector/alerter.py
import json
from pathlib import Path
from datetime import datetime
import pandas as pd

ALERTS_FILE = Path("aiops-platform/data/alerts.jsonl")

def write_alerts(df: pd.DataFrame, metric_name: str) -> None:
    """Append anomaly rows to a JSONL alerts file."""
    anomalies = df[df["is_anomaly"]]
    if anomalies.empty:
        return
    ALERTS_FILE.parent.mkdir(parents=True, exist_ok=True)
    with open(ALERTS_FILE, "a") as f:
        for _, row in anomalies.iterrows():
            alert = {
                "timestamp": row["timestamp"].isoformat(),
                "metric":    metric_name,
                "value":     float(row["value"]),
                "severity":  float(row["severity"]),
                "detected_at": datetime.utcnow().isoformat(),
            }
            f.write(json.dumps(alert) + "\n")
```

## Step 5: main.py

```python
# aiops-platform/modules/anomaly_detector/main.py
import time
from collector import fetch_metric
from detector  import detect
from scorer    import add_severity
from alerter   import write_alerts

METRICS = [
    ("rate(node_cpu_seconds_total{mode='idle'}[5m])", "cpu_idle"),
    ("node_memory_MemAvailable_bytes",                 "mem_available"),
    ("rate(http_requests_total[5m])",                  "http_requests"),
]

def run_once():
    for query, name in METRICS:
        series = fetch_metric(query, minutes=1500)  # 25 hours for training window
        if series.empty:
            print(f"No data for {name}")
            continue
        df = detect(series)
        df = add_severity(df)
        write_alerts(df, name)
        n = df["is_anomaly"].sum()
        print(f"{name}: {n} anomalies detected")

if __name__ == "__main__":
    while True:
        run_once()
        time.sleep(60)
```

## Step 6: Test it manually

```bash
cd aiops-platform
python modules/anomaly_detector/main.py
# Expected output:
# cpu_idle: 0 anomalies detected
# mem_available: 0 anomalies detected
# http_requests: 0 anomalies detected
```

Check `data/alerts.jsonl` after a few minutes. Inject a synthetic spike to verify detection:
```bash
# Simulate a CPU spike by stressing the system for 2 minutes, then check alerts.jsonl
stress-ng --cpu 4 --timeout 120s
```

## Step 7: Commit to capstone repo

```bash
cd aiops-platform
git add modules/anomaly_detector/ data/
git commit -m "feat(module-1): live anomaly detector on Prometheus metrics"
```

## Done When

- [ ] `main.py` runs without errors against your Prometheus
- [ ] At least one real anomaly (or injected spike) appears in `alerts.jsonl` with a severity score
- [ ] You can explain to a colleague what `contamination=0.01` means and when you'd raise or lower it
