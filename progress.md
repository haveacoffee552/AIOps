# Learning Progress Tracker

Check off each item as you complete it. Commit this file after each session.

## Phase 0 — Orientation (Week 1–2)
- [ ] Read Gartner AIOps Market Guide
- [ ] Read CNCF TAG Observability whitepaper
- [ ] Survey Moogsoft, Dynatrace, Datadog AIOps features
- [ ] Set up Python 3.11+, Jupyter, VS Code, Docker
- [ ] Create `aiops-platform` GitHub repo

## Phase 1 — ML Foundations (Month 1–2)

### Block A — Python for Data (Week 1–2)
- [ ] Complete NumPy basics exercises
- [ ] Complete Pandas time series exercises
- [ ] Complete Matplotlib/Seaborn visualization exercises
- [ ] Practice: load Prometheus export, plot CPU/memory/request rate

### Block B — Core ML Concepts (Week 3–5)
- [ ] Understand supervised vs unsupervised learning
- [ ] Implement Isolation Forest on synthetic data
- [ ] Implement k-means clustering
- [ ] Implement DBSCAN clustering
- [ ] Understand overfitting, train/validation split
- [ ] Practice: train Isolation Forest on synthetic CPU metrics, measure F1

### Block C — Time Series Analysis (Week 6–8)
- [ ] Understand stationarity and seasonality
- [ ] Apply STL decomposition to a dataset
- [ ] Run SARIMA on a time series
- [ ] Run Facebook Prophet on a time series
- [ ] Practice: NAB dataset — compare z-score vs Isolation Forest anomaly detection

## Phase 2 — Anomaly Detection (Month 3)
- [ ] Read: statistical methods (z-score, Bollinger Bands, Holt-Winters)
- [ ] Read: ML methods (Isolation Forest, Autoencoders, LSTM detectors)
- [ ] Study Luminol codebase
- [ ] Study Alibi-Detect quickstart
- [ ] Study Prometheus Anomaly Detector README
- [ ] Build Module 1: connect to Prometheus API
- [ ] Build Module 1: dynamic anomaly detector on live metrics
- [ ] Build Module 1: severity-scored alert output

## Phase 3 — Log Intelligence (Month 4)
- [ ] Read: Drain algorithm (ICWS 2017 paper)
- [ ] Read: log clustering with DBSCAN
- [ ] Read: DeepLog paper (CCS 2017)
- [ ] Set up Drain3 on real application logs
- [ ] Build Module 2: log template clustering
- [ ] Build Module 2: rare pattern detection
- [ ] Build Module 2: correlate log anomalies with Module 1 metric alerts

## Phase 4 — Root Cause Analysis (Month 5)
- [ ] Read: temporal and topological event correlation
- [ ] Read: causality vs correlation in distributed systems
- [ ] Study CIRCA codebase
- [ ] Build Module 3: service dependency graph from traces
- [ ] Build Module 3: time-window event correlator
- [ ] Build Module 3: graph-traversal RCA scorer
- [ ] Build Module 3: incident report generator

## Phase 5 — Capacity Planning (Month 6)
- [ ] Read: workload characterization patterns
- [ ] Study Prophet documentation and examples
- [ ] Study NeuralForecast quickstart
- [ ] Study Karpenter scaling logic
- [ ] Build Module 4: 90-day historical data pipeline
- [ ] Build Module 4: saturation forecaster (24–72 hour horizon)
- [ ] Build Module 4: proactive alert integration with Module 1
- [ ] Verify: at least one proactive alert appears in data/alerts.jsonl (or document why saturation is not predicted)

## Phase 6 — Capstone Integration + MLOps (Month 7)

### Week 1–2: Integration
- [ ] Unified data pipeline (OTel collector → shared JSONL event files → module inputs)
- [ ] Standardized alert/event schema
- [ ] FastAPI layer serving all 4 modules
- [ ] Grafana dashboard

### Week 3–4: MLOps
- [ ] MLflow model versioning set up
- [ ] Drift detection with Alibi-Detect
- [ ] Automated retraining trigger
- [ ] Model prediction logging

### Week 5–6: Hardening
- [ ] All modules containerized with Docker
- [ ] docker-compose wiring complete
- [ ] Operational runbook written
- [ ] Load test passed
- [ ] Lessons learned written
