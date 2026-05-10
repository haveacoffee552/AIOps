# Module 3 — Incident Correlator + RCA Engine

**Capstone file:** `aiops-platform/modules/rca_engine/`

## What You're Building

A service that reads active alerts (from Module 1), groups them by time window, builds a service dependency graph, and scores each service as a root cause candidate.

## File Structure

```
aiops-platform/modules/rca_engine/
├── graph_builder.py    # Build service dependency graph from traces
├── correlator.py       # Group alerts into incidents by time window
├── rca_scorer.py       # Score root cause candidates via graph traversal
├── reporter.py         # Generate incident report
└── main.py
```

## Step 0: Install dependencies

```bash
pip install networkx requests
```

## Step 1: graph_builder.py

```python
# aiops-platform/modules/rca_engine/graph_builder.py
# Builds a directed graph from Jaeger traces via its HTTP API.
import requests
import networkx as nx
from datetime import datetime, timedelta

JAEGER_URL = "http://localhost:16686"

def build_dependency_graph(lookback_minutes: int = 60) -> nx.DiGraph:
    """Query Jaeger for recent traces and extract service call graph."""
    G = nx.DiGraph()
    end_us   = int(datetime.utcnow().timestamp() * 1_000_000)
    start_us = end_us - lookback_minutes * 60 * 1_000_000

    resp = requests.get(f"{JAEGER_URL}/api/traces", params={
        "limit": 500,
        "start": start_us,
        "end":   end_us,
    })
    resp.raise_for_status()
    traces = resp.json().get("data", [])

    for trace in traces:
        processes = trace.get("processes", {})
        spans = {s["spanID"]: s for s in trace["spans"]}
        for span in trace["spans"]:
            svc_name = processes.get(span["processID"], {}).get("serviceName", span["processID"])
            if span.get("references"):
                parent_id = span["references"][0]["spanID"]
                if parent_id in spans:
                    parent_svc = processes.get(spans[parent_id]["processID"], {}).get("serviceName", spans[parent_id]["processID"])
                    G.add_edge(parent_svc, svc_name)
    return G
```

## Step 2: correlator.py

```python
# aiops-platform/modules/rca_engine/correlator.py
import json
from datetime import datetime, timedelta
from pathlib import Path

ALERTS_FILE = Path("aiops-platform/data/alerts.jsonl")

def load_recent_alerts(window_minutes: int = 10) -> list[dict]:
    if not ALERTS_FILE.exists():
        return []
    cutoff = datetime.utcnow() - timedelta(minutes=window_minutes)
    alerts = []
    with open(ALERTS_FILE) as f:
        for line in f:
            a = json.loads(line)
            if datetime.fromisoformat(a["timestamp"]) >= cutoff:
                alerts.append(a)
    return alerts

def group_into_incident(alerts: list[dict]) -> dict:
    """Group all alerts in the window into a single incident."""
    if not alerts:
        return {}
    return {
        "incident_id":    f"INC-{int(datetime.utcnow().timestamp())}",
        "started_at":     min(a["timestamp"] for a in alerts),
        "alert_count":    len(alerts),
        "affected_metrics": list({a["metric"] for a in alerts}),
        "max_severity":   max(a["severity"] for a in alerts),
        "alerts":         alerts,
    }
```

## Step 3: rca_scorer.py

```python
# aiops-platform/modules/rca_engine/rca_scorer.py
import networkx as nx

def score_root_causes(graph: nx.DiGraph, affected_services: list[str]) -> list[dict]:
    """
    Score each node in the graph by how many affected services it can reach downstream.
    Higher score = more likely root cause.
    """
    scores = {}
    affected_set = set(affected_services)

    for node in graph.nodes():
        descendants = nx.descendants(graph, node)
        hit = descendants & affected_set
        scores[node] = len(hit)

    ranked = sorted(scores.items(), key=lambda x: x[1], reverse=True)
    return [{"service": svc, "rca_score": score} for svc, score in ranked if score > 0]
```

## Step 4: reporter.py

```python
# aiops-platform/modules/rca_engine/reporter.py
import json
from pathlib import Path
from datetime import datetime

REPORTS_FILE = Path("aiops-platform/data/incidents.jsonl")

def write_report(incident: dict, rca_candidates: list[dict]) -> None:
    report = {
        **incident,
        "rca_candidates": rca_candidates[:3],   # top 3 candidates
        "generated_at":   datetime.utcnow().isoformat(),
    }
    REPORTS_FILE.parent.mkdir(parents=True, exist_ok=True)
    with open(REPORTS_FILE, "a") as f:
        f.write(json.dumps(report) + "\n")
    print(f"Incident {report['incident_id']}: top cause = {rca_candidates[0]['service'] if rca_candidates else 'unknown'}")
```

## Step 5: main.py

```python
# aiops-platform/modules/rca_engine/main.py
from graph_builder import build_dependency_graph
from correlator    import load_recent_alerts, group_into_incident
from rca_scorer    import score_root_causes
from reporter      import write_report

# Map metric names to the service that owns them. Update this for your stack.
METRIC_TO_SERVICE = {
    "cpu_idle":       "node-exporter",
    "mem_available":  "node-exporter",
    "http_requests":  "api-server",
}

def run():
    alerts = load_recent_alerts(window_minutes=10)
    if not alerts:
        print("No recent alerts — no incident to analyze")
        return
    incident = group_into_incident(alerts)
    graph    = build_dependency_graph(lookback_minutes=60)
    affected_services = list({
        METRIC_TO_SERVICE.get(m, m) for m in incident["affected_metrics"]
    })
    candidates = score_root_causes(graph, affected_services)
    write_report(incident, candidates)

if __name__ == "__main__":
    run()
```

## Step 6: Commit to capstone repo

```bash
cd aiops-platform
git add modules/rca_engine/ data/
git commit -m "feat(module-3): RCA engine with dependency graph and incident correlator"
```

## Done When

- [ ] `main.py` runs and writes a report to `incidents.jsonl`
- [ ] Report contains ranked RCA candidates when multiple services are alerting
- [ ] You can explain what `nx.descendants()` returns and why it approximates root cause likelihood
