# AIOps Learning Route Map

## Timeline

| Phase | Focus | Duration | Key Output |
|---|---|---|---|
| [0 — Orientation](phases/phase-0-orientation/README.md) | AIOps landscape + dev setup | Week 1–2 | Environment ready, landscape understood |
| [1 — ML Foundations](phases/phase-1-ml-foundations/README.md) | Python for data, core ML, time series | Month 1–2 | Can train and evaluate anomaly detection models |
| [2 — Anomaly Detection](phases/phase-2-anomaly-detection/README.md) | Dynamic alerting on live metrics | Month 3 | Capstone Module 1: live anomaly detector |
| [3 — Log Intelligence](phases/phase-3-log-intelligence/README.md) | Log parsing, clustering, anomaly detection | Month 4 | Capstone Module 2: log intelligence pipeline |
| [4 — Root Cause Analysis](phases/phase-4-root-cause-analysis/README.md) | Event correlation, graph RCA | Month 5 | Capstone Module 3: incident correlator + RCA scorer |
| [5 — Capacity Planning](phases/phase-5-capacity-planning/README.md) | Forecasting, proactive scaling | Month 6 | Capstone Module 4: resource saturation forecaster |
| [6 — Capstone + MLOps](phases/phase-6-capstone/README.md) | Integration, drift detection, hardening | Month 7 | Unified AIOps platform, deployed, documented |

## Approach

**Foundations-first:** Build a shared ML base (Phase 1) before tackling AIOps domains. Your DevOps knowledge means the infrastructure layer is already handled — the ML gap is the focus.

**Single capstone thread:** Don't build 4 separate projects. Each domain phase extends the same `aiops-platform/` repo. Integration is Phase 6's focus, not an afterthought.

## Open-Source Ecosystem

| Domain | Key Projects |
|---|---|
| Anomaly Detection | Luminol, Alibi-Detect, Prometheus Anomaly Detector |
| Log Intelligence | Drain3, Logparser, DeepLog |
| Root Cause Analysis | Causal-learn, MicroTosca, CIRCA |
| Capacity Planning | Prophet, NeuralForecast, Karpenter |

Full details: [resources/open-source.md](resources/open-source.md)
