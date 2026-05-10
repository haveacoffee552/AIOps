# Module 2 — Log Intelligence Pipeline

**Capstone file:** `aiops-platform/modules/log_intelligence/`

## What You're Building

A pipeline that reads log files, parses them with Drain3, clusters templates, detects novel/rare patterns, and correlates with Module 1 alerts.

## File Structure

```
aiops-platform/modules/log_intelligence/
├── parser.py          # Drain3 log parsing
├── clusterer.py       # TF-IDF + DBSCAN on templates
├── correlator.py      # Match log anomalies to metric alerts
└── main.py
```

## Step 1: Install Drain3

```bash
pip install drain3 scikit-learn
```

## Step 2: parser.py

```python
# aiops-platform/modules/log_intelligence/parser.py
from drain3 import TemplateMiner
from drain3.template_miner_config import TemplateMinerConfig
import json
from pathlib import Path

def build_parser() -> TemplateMiner:
    config = TemplateMinerConfig()
    config.load(str(Path(__file__).parent / "drain3.ini"))
    return TemplateMiner(config=config)

def parse_log_file(log_path: str) -> list[dict]:
    """Parse each line, return list of {raw, template, params, cluster_id}."""
    parser = build_parser()
    results = []
    with open(log_path) as f:
        for line in f:
            line = line.strip()
            if not line:
                continue
            result = parser.add_log_message(line)
            results.append({
                "raw":        line,
                "template":   result["template_mined"],
                "cluster_id": result["cluster_id"],
                "change_type": result["change_type"],
            })
    return results
```

Create `drain3.ini` in the same directory:
```ini
[DRAIN]
sim_th = 0.4
depth = 4
max_children = 100
max_clusters = 1024

[SNAPSHOT]
snapshot_interval_minutes = 60
compress_state = True
```

## Step 3: clusterer.py

```python
# aiops-platform/modules/log_intelligence/clusterer.py
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.cluster import DBSCAN
import numpy as np

def find_rare_patterns(parsed_logs: list[dict], eps: float = 0.5) -> list[dict]:
    """
    Cluster log templates with DBSCAN. Return logs assigned to noise (-1)
    — these are rare/novel patterns worth surfacing.
    """
    templates = [log["template"] for log in parsed_logs]
    if len(templates) < 5:
        return []

    vectorizer = TfidfVectorizer(analyzer='word', token_pattern=r'\b[a-zA-Z]+\b')
    X = vectorizer.fit_transform(templates).toarray()

    db = DBSCAN(eps=eps, min_samples=3, metric='cosine')
    labels = db.fit_predict(X)

    rare = []
    for log, label in zip(parsed_logs, labels):
        if label == -1:
            rare.append({**log, "cluster_label": -1, "reason": "novel_template"})
    return rare
```

## Step 4: correlator.py

```python
# aiops-platform/modules/log_intelligence/correlator.py
import json
from datetime import datetime, timedelta
from pathlib import Path

ALERTS_FILE = Path("aiops-platform/data/alerts.jsonl")
CORRELATION_WINDOW_SECONDS = 300  # 5-minute window

def load_metric_alerts(since_minutes: int = 60) -> list[dict]:
    if not ALERTS_FILE.exists():
        return []
    cutoff = datetime.utcnow() - timedelta(minutes=since_minutes)
    alerts = []
    with open(ALERTS_FILE) as f:
        for line in f:
            alert = json.loads(line)
            ts = datetime.fromisoformat(alert["timestamp"])
            if ts >= cutoff:
                alerts.append(alert)
    return alerts

def correlate(log_anomalies: list[dict], log_timestamps: list[datetime]) -> list[dict]:
    """
    For each log anomaly, check if a metric alert occurred within CORRELATION_WINDOW_SECONDS.
    Return correlated events.
    """
    metric_alerts = load_metric_alerts()
    correlated = []
    for log_anom, log_ts in zip(log_anomalies, log_timestamps):
        for alert in metric_alerts:
            alert_ts = datetime.fromisoformat(alert["timestamp"])
            delta = abs((log_ts - alert_ts).total_seconds())
            if delta <= CORRELATION_WINDOW_SECONDS:
                correlated.append({
                    "log_template":    log_anom["template"],
                    "log_timestamp":   log_ts.isoformat(),
                    "correlated_metric": alert["metric"],
                    "metric_severity": alert["severity"],
                    "time_delta_sec":  delta,
                })
    return correlated
```

## Step 5: main.py

```python
# aiops-platform/modules/log_intelligence/main.py
import json
from pathlib import Path
from datetime import datetime
from parser import parse_log_file
from clusterer import find_rare_patterns

LOGS_PATH   = "/var/log/app/application.log"   # adjust to your log path
OUTPUT_FILE = Path("aiops-platform/data/log_anomalies.jsonl")

def run():
    parsed = parse_log_file(LOGS_PATH)
    rare   = find_rare_patterns(parsed)
    OUTPUT_FILE.parent.mkdir(parents=True, exist_ok=True)
    with open(OUTPUT_FILE, "a") as f:
        for r in rare:
            r["detected_at"] = datetime.utcnow().isoformat()
            f.write(json.dumps(r) + "\n")
    print(f"Found {len(rare)} rare log patterns from {len(parsed)} lines")

if __name__ == "__main__":
    run()
```

## Step 6: Commit to capstone repo

```bash
cd aiops-platform
git add modules/log_intelligence/ data/
git commit -m "feat(module-2): log intelligence pipeline with Drain3 and DBSCAN clustering"
```

## Done When

- [ ] `main.py` runs against your real application logs without errors
- [ ] At least some rare patterns appear in `log_anomalies.jsonl`
- [ ] You can explain what `eps=0.5` controls in DBSCAN and how you'd tune it
