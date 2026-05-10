# Phase 6 — Capstone Integration + MLOps in Production

→ [System Architecture Diagram + API Contract](architecture.md)

**Duration:** Month 7 (6 weeks) | **Output:** Unified AIOps platform, deployed and documented

## Week 1–2: Integration

### Unified Data Pipeline

All four modules share a common event schema. Standardize now:

```python
# aiops-platform/shared/event.py
from dataclasses import dataclass
from datetime import datetime

@dataclass
class AIOpsEvent:
    event_id:     str
    source:       str        # "anomaly_detector" | "log_intelligence" | "rca_engine" | "capacity_planner"
    metric:       str
    value:        float
    severity:     float      # 0.0–1.0
    event_type:   str        # "anomaly" | "log_rare" | "rca" | "proactive"
    timestamp:    datetime
    metadata:     dict       # source-specific extras
```

### FastAPI Service

```
aiops-platform/api/
├── main.py          # FastAPI app
├── routes/
│   ├── alerts.py    # GET /alerts, GET /alerts/active
│   ├── incidents.py # GET /incidents, GET /incidents/{id}
│   └── forecast.py  # GET /forecast/{metric}
└── models.py        # Pydantic response models
```

Run all modules as background threads, serve results via the API.

### Grafana Dashboard

Create panels for:
1. Active anomaly count (from `alerts.jsonl`, filter `is_anomaly=true`)
2. Alert severity distribution (histogram)
3. Recent incidents with RCA candidates (table panel)
4. Capacity forecast for CPU + memory (time series with forecast line)

## Week 3–4: MLOps

### MLflow Model Tracking

```bash
pip install mlflow
mlflow ui  # runs at http://localhost:5000
```

```python
import mlflow

with mlflow.start_run(run_name="isolation_forest_v1"):
    mlflow.log_param("contamination", 0.01)
    mlflow.log_param("training_window", 1440)
    mlflow.log_metric("precision", precision)
    mlflow.log_metric("recall", recall)
    mlflow.log_metric("f1", f1)
    mlflow.sklearn.log_model(clf, "isolation_forest")
```

### Drift Detection with Alibi-Detect

```python
from alibi_detect.cd import KSDrift

# Train on 7 days of baseline data
detector = KSDrift(reference, p_val=0.05)

# Daily: test current window against baseline
result = detector.predict(current_window)
if result["data"]["is_drift"]:
    print("Drift detected — schedule retraining")
    # trigger retraining pipeline
```

## Week 5–6: Hardening

### Docker Compose

Create `aiops-platform/docker-compose.yml` with services:
- `anomaly-detector` — runs `modules/anomaly_detector/main.py` on 60s interval
- `log-intelligence` — runs `modules/log_intelligence/main.py` on 5m interval
- `rca-engine` — runs `modules/rca_engine/main.py` on 5m interval
- `capacity-planner` — runs `modules/capacity_planner/main.py` on 6h interval
- `api` — FastAPI service on port 8000

### Load Test

```bash
# Verify the API handles load before claiming production-ready
pip install locust
locust -f tests/locustfile.py --headless -u 50 -r 5 --run-time 60s
```

### Operational Runbook

Write `aiops-platform/RUNBOOK.md` covering:
1. How to retrain any module's model manually
2. How to tune the `contamination` parameter for anomaly detection
3. How to add a new Prometheus metric to the anomaly detector
4. How to restart a stuck module
5. How to interpret an RCA report

## Capstone Completion Checklist

- [ ] All 4 modules running against live infrastructure
- [ ] Unified FastAPI service running on port 8000
- [ ] Grafana dashboard with 4 panels
- [ ] MLflow tracking server with at least one registered model
- [ ] Drift detection running daily
- [ ] docker-compose brings up all services cleanly
- [ ] Load test passes (API handles 50 concurrent users)
- [ ] RUNBOOK.md written
- [ ] Lessons learned document written

## Final Commit

```bash
cd aiops-platform
git add .
git commit -m "feat: unified AIOps platform — all modules integrated with API, MLOps, and docker-compose"
git tag v1.0.0
```
