# AIOps Learning Route Map — Design Spec

**Date:** 2026-05-10
**Author:** nhannn278@gmail.com
**Approach:** Foundations-First, then Domain Specialization
**Timeline:** ~7 months at 5–10 hours/week

---

## Learner Profile

- **Background:** DevOps/SRE engineer — strong in infrastructure, monitoring, incident response
- **ML knowledge:** None (this is the primary gap)
- **Goal:** Build AIOps tools for own team/org
- **Pain points to solve:** Anomaly detection, log intelligence, root cause analysis, capacity planning
- **Learning style:** Single end-to-end capstone project, with open-source references introduced per domain

---

## Overall Structure

| Phase | Focus | Duration |
|---|---|---|
| 0 | AIOps Orientation | Week 1–2 |
| 1 | ML Foundations for Ops Engineers | Month 1–2 |
| 2 | Domain: Anomaly Detection & Alerting | Month 3 |
| 3 | Domain: Log Intelligence | Month 4 |
| 4 | Domain: Root Cause Analysis & Incident Correlation | Month 5 |
| 5 | Domain: Capacity Planning & Predictive Scaling | Month 6 |
| 6 | Capstone Integration + MLOps in Production | Month 7 |

**Capstone thread:** Phases 2–6 each add one module to a single unified AIOps platform. The capstone is not a separate project — it grows alongside learning.

**DevOps skip markers:** Sections on Docker, Prometheus, Grafana setup, and incident workflows are marked `[SKIP — you know this]` throughout.

---

## Phase 0 — AIOps Orientation (Week 1–2)

**Goal:** Understand the landscape before touching any code.

### Theory
- What is AIOps? Key concepts: event correlation, anomaly detection, observability pipeline
- The AIOps stack: data sources (metrics, logs, traces) → ML layer → action layer
- Survey commercial solutions: Moogsoft, Dynatrace, Datadog AIOps — what problems do they solve and how?

### Reading
- Gartner's AIOps Market Guide (definition and landscape)
- CNCF TAG Observability whitepaper

### Setup
- Python 3.11+, Jupyter, VS Code, Docker `[SKIP if already set up]`
- Create project GitHub repo: `aiops-platform`

---

## Phase 1 — ML Foundations for Ops Engineers (Month 1–2)

**Goal:** Learn only the ML needed for AIOps — not all of machine learning.

### Block A — Python for Data (Week 1–2)
**Theory:**
- NumPy, Pandas, Matplotlib/Seaborn
- Working with time series data structures
- Resampling, rolling windows, lag features

**Practice:**
- Load a Prometheus metrics export (CSV or JSON)
- Plot CPU, memory, request rate over time
- Visually identify outliers — no ML yet, just exploration

### Block B — Core ML Concepts (Week 3–5)
**Theory:**
- Supervised vs unsupervised learning (AIOps uses mostly unsupervised)
- Key algorithms:
  - Isolation Forest (anomaly detection)
  - k-means, DBSCAN (clustering)
  - Linear Regression (trend modeling)
  - LSTM basics (sequence modeling)
- Overfitting, train/validation splits
- Evaluation metrics: precision, recall, F1-score, AUC

**Practice:**
- Generate synthetic CPU metric data with injected anomalies
- Train an Isolation Forest, evaluate precision/recall
- Experiment with contamination parameter

### Block C — Time Series Analysis (Week 6–8)
**Theory:**
- Stationarity, seasonality, trend (STL decomposition)
- SARIMA: when and why to use it
- Facebook Prophet: business-friendly forecasting with seasonality
- Anomaly detection approaches: statistical (z-score, IQR) vs ML (Isolation Forest, Autoencoder)

**Practice:**
- Download the Numenta Anomaly Benchmark (NAB) dataset
- Apply STL decomposition, visualize components
- Detect anomalies using both z-score and Isolation Forest
- Compare results — where does each approach fail?

**Key resource:** *Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow* (Géron) — Chapters 1–4, 8–9, 15 only.

---

## Phase 2 — Anomaly Detection & Alerting (Month 3)

### Theory
- Statistical methods: z-score, rolling mean/std, Bollinger Bands, Holt-Winters
- ML methods: Isolation Forest, Autoencoders, LSTM-based detectors
- The alert fatigue problem: why static thresholds fail at scale
- Dynamic thresholding strategies

### Practice — Capstone Module 1
- Connect to real Prometheus/Grafana stack via HTTP API
- Build a dynamic anomaly detector on live infrastructure metrics
- Output: alerts with severity scores (not binary on/off flags)
- Store alerts in a time series DB or structured log for later correlation

### Open-Source References
| Project | Purpose |
|---|---|
| [Luminol](https://github.com/linkedin/luminol) | Lightweight time series anomaly detection (LinkedIn) |
| [Alibi-Detect](https://github.com/SeldonIO/alibi-detect) | Production-grade anomaly & drift detection |
| [Prometheus Anomaly Detector](https://github.com/AICoE/prometheus-anomaly-detector) | k-NN on Prometheus metrics (Red Hat) |

---

## Phase 3 — Log Intelligence (Month 4)

### Theory
- Log parsing: the Drain algorithm — fast, streaming, production-proven
- Log clustering: grouping similar templates with DBSCAN
- Log anomaly detection: DeepLog (LSTM on log sequences), LogBERT
- NLP basics for logs: TF-IDF, sentence embeddings (no full NLP course needed)

### Practice — Capstone Module 2
- Run Drain3 on real application logs from your stack
- Cluster log templates, surface rare/novel patterns automatically
- Integrate with Module 1: correlate metric anomalies with log anomalies
- Output: enriched alerts with supporting log evidence

### Open-Source References
| Project | Purpose |
|---|---|
| [Drain3](https://github.com/logpai/Drain3) | Production-ready streaming log parser |
| [Logparser](https://github.com/logpai/logparser) | Benchmark toolkit with 13 parsing algorithms |
| [DeepLog](https://github.com/wuyifan18/DeepLog) | LSTM-based log anomaly detection |

---

## Phase 4 — Root Cause Analysis & Incident Correlation (Month 5)

### Theory
- Event correlation: temporal (time-window grouping) and topological (service-dependency aware)
- Causality vs correlation: why correlation alone fails in distributed systems
- Graph-based RCA: service dependency graphs, Bayesian networks
- Microservice RCA patterns: trace-based, metric-based, log-based triangulation

### Practice — Capstone Module 3
- Build a service dependency graph from OpenTelemetry or Jaeger traces
- Implement event correlator: group alerts within a time window by affected service
- Score root cause candidates using graph traversal (which upstream service triggered cascade?)
- Output: incident report draft with ranked root cause candidates

### Open-Source References
| Project | Purpose |
|---|---|
| [Causal-learn](https://github.com/py-why/causal-learn) | Causal discovery algorithms (PC, GES, LiNGAM) |
| [MicroTosca](https://github.com/di-unipi-socc/microTosca) | Microservice topology-aware RCA |
| [CIRCA](https://github.com/NetManAIOps/CIRCA) | Cloud RCA (NeurIPS 2022) |

---

## Phase 5 — Capacity Planning & Predictive Scaling (Month 6)

### Theory
- Workload characterization: diurnal patterns, weekly cycles, growth trends
- Forecasting methods: Prophet (business-friendly), SARIMA, LSTM for multivariate
- Resource utilization modeling: CPU/memory headroom, saturation points
- Cost-aware scaling: predict need before saturation, not after

### Practice — Capstone Module 4
- Build a forecasting pipeline on 90 days of historical Prometheus data
- Predict resource saturation 24–72 hours ahead
- Generate capacity report + recommended scaling actions
- Integrate with Module 1: proactive alert before anomaly rather than reactive response

### Open-Source References
| Project | Purpose |
|---|---|
| [Prophet](https://github.com/facebook/prophet) | Battle-tested forecasting with seasonality (Meta) |
| [NeuralForecast](https://github.com/Nixtla/neuralforecast) | Modern deep learning forecasting (Nixtla) |
| [Karpenter](https://github.com/aws/karpenter) | Study its scaling logic as a production reference |

---

## Phase 6 — Capstone Integration + MLOps in Production (Month 7)

### Week 1–2: Integration
- Unify 4 modules behind a shared data pipeline: OpenTelemetry collector → feature store → model layer
- Standardize alert/event schema across all modules
- Build a single API layer (FastAPI) serving all four modules
- Single Grafana dashboard fed by the AIOps API

### Week 3–4: MLOps — Keeping Models Alive in Production
- Model versioning with MLflow: track experiments, register models
- Drift detection with Alibi-Detect: know when your anomaly model degrades
- Automated retraining trigger: drift detected → retrain → promote new model
- Model monitoring: log predictions, measure alert precision/recall over time

### Week 5–6: Hardening & Documentation
- Containerize all modules with Docker, wire together with docker-compose
- Write an operational runbook: how to retrain, tune thresholds, add a new data source
- Load test: verify the pipeline handles actual metrics/log volume
- Write lessons learned document

### Capstone Deliverable

A GitHub repo (`aiops-platform`) containing:

- [ ] Anomaly detector on live Prometheus metrics
- [ ] Log intelligence pipeline (Drain3-based)
- [ ] Incident correlator with RCA scoring
- [ ] Capacity forecasting with proactive alerts
- [ ] MLOps layer: drift detection + automated retraining
- [ ] Docker-compose deployment
- [ ] Grafana dashboard
- [ ] FastAPI service with API docs
- [ ] Operational runbook

---

## Supporting Resources

### Datasets
| Dataset | Use |
|---|---|
| [Numenta Anomaly Benchmark (NAB)](https://github.com/numenta/NAB) | Phase 1 time series practice |
| [AIOPS Challenge Datasets (2018–2022)](https://competition.aiops-challenge.com) | Phases 2–5 domain practice |
| [Loghub](https://github.com/logpai/loghub) | Phase 3 log intelligence |

### Papers Worth Reading
- *AIOps: Real-World Challenges and Research Innovations* — IBM Research
- *Drain: An Online Log Parsing Approach with Fixed Depth Tree* — ICWS 2017
- *DeepLog: Anomaly Detection and Diagnosis from System Logs* — CCS 2017
- *CIRCA: Causal Inference for Root Cause Analysis* — NeurIPS 2022

### Community
- CNCF TAG Observability Slack (`#observability` channel)
- arXiv: `cs.LG` + `cs.SE` tags for AIOps papers
- Papers With Code: search "AIOps", "log anomaly detection", "root cause analysis"

---

## Success Criteria

By the end of Month 7, you should be able to:

1. Explain the ML techniques behind each AIOps domain and when to use which
2. Run a working anomaly detector, log parser, RCA engine, and capacity forecaster against your real infrastructure
3. Detect concept drift and retrain models without manual intervention
4. Present the platform to your team and hand over operational runbooks
