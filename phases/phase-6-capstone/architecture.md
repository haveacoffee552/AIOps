# Capstone System Architecture

## Component Diagram

```
┌─────────────────────────────────────────────────────────────────────┐
│                        DATA SOURCES                                  │
│  Prometheus (metrics) │ Log files │ Jaeger/OTel (traces)            │
└────────────┬──────────┴─────┬─────┴──────────┬──────────────────────┘
             │                │                 │
             ▼                ▼                 ▼
┌─────────────────────────────────────────────────────────────────────┐
│                        MODULE LAYER                                  │
│                                                                      │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐  │
│  │ Anomaly Detector │  │ Log Intelligence │  │   RCA Engine     │  │
│  │ (Isolation Forest│  │ (Drain3 + DBSCAN)│  │ (Graph traversal)│  │
│  │  + Bollinger)    │  │                  │  │                  │  │
│  └────────┬─────────┘  └────────┬─────────┘  └────────┬─────────┘  │
│           │                     │                      │            │
│           └─────────────────────┼──────────────────────┘            │
│                                 ▼                                    │
│                    ┌──────────────────────┐                         │
│                    │  Capacity Planner    │                         │
│                    │  (Prophet forecast)  │                         │
│                    └──────────────────────┘                         │
└─────────────────────────────────┬───────────────────────────────────┘
                                  │ shared: data/alerts.jsonl
                                  │         data/incidents.jsonl
                                  ▼
┌─────────────────────────────────────────────────────────────────────┐
│                        API LAYER                                     │
│                    FastAPI on port 8000                              │
│  GET /alerts         GET /incidents        GET /forecast/{metric}   │
└─────────────────────────────────┬───────────────────────────────────┘
                                  │
             ┌────────────────────┼────────────────────┐
             ▼                    ▼                     ▼
     ┌──────────────┐   ┌──────────────────┐   ┌──────────────┐
     │   Grafana    │   │     MLflow       │   │  Alibi-Detect│
     │  Dashboard   │   │  Model Registry  │   │    Drift     │
     └──────────────┘   └──────────────────┘   └──────────────┘
```

## API Contract

### GET /alerts
Returns recent alerts from all modules.
```json
{
  "alerts": [
    {
      "event_id": "uuid",
      "source": "anomaly_detector",
      "metric": "cpu_usage",
      "value": 94.2,
      "severity": 0.87,
      "event_type": "anomaly",
      "timestamp": "2026-05-10T14:32:01Z",
      "metadata": {}
    }
  ],
  "total": 1
}
```

### GET /incidents
Returns recent incidents with RCA candidates.
```json
{
  "incidents": [
    {
      "incident_id": "INC-1715350321",
      "started_at": "2026-05-10T14:30:00Z",
      "alert_count": 3,
      "max_severity": 0.9,
      "rca_candidates": [
        {"service": "payment-service", "rca_score": 2},
        {"service": "database", "rca_score": 1}
      ]
    }
  ]
}
```

### GET /forecast/{metric}
Returns 72-hour forecast for the given metric.
```json
{
  "metric": "cpu_usage",
  "forecast": [
    {"timestamp": "2026-05-10T15:00:00Z", "yhat": 52.3, "yhat_lower": 48.1, "yhat_upper": 56.5}
  ],
  "saturation_eta_hours": null
}
```

## Data Flow

1. Modules write events to `data/alerts.jsonl` (append-only JSONL)
2. FastAPI reads and serves from those files
3. Grafana queries FastAPI via HTTP
4. MLflow tracks model metadata separately (SQLite backend by default)
5. Alibi-Detect drift detector runs as a daily cron job, writes drift events to `data/drift.jsonl`
