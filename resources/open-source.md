# Open-Source Projects

## Anomaly Detection

### Luminol (LinkedIn)
**Repo:** https://github.com/linkedin/luminol
**What it does:** Time series anomaly detection and correlation. Two algorithms: bitmap (pattern-based) and derivative (rate-of-change).
**When to use:** When you want a battle-tested lightweight library without sklearn dependency.
**Setup:**
```bash
pip install luminol
```
```python
from luminol.anomaly_detector import AnomalyDetector
ts = {timestamp: value, ...}   # dict of unix_timestamp → float
detector = AnomalyDetector(ts)
anomalies = detector.get_anomalies()
```

### Alibi-Detect
**Repo:** https://github.com/SeldonIO/alibi-detect
**What it does:** Anomaly detection, outlier detection, and drift detection. Production-ready wrappers around isolation forest, VAE, and statistical tests.
**When to use:** Phase 6 MLOps — drift detection after your model is in production.
**Setup:**
```bash
pip install alibi-detect
```

### Prometheus Anomaly Detector (Red Hat)
**Repo:** https://github.com/AICoE/prometheus-anomaly-detector
**What it does:** Queries Prometheus, runs Fourier and Prophet models, outputs anomaly metrics back to Prometheus.
**When to use:** Reference architecture for how to wire Prometheus → ML → Prometheus.

---

## Log Intelligence

### Drain3
**Repo:** https://github.com/logpai/Drain3
**What it does:** Streaming log parser using the Drain algorithm. Maintains state between log batches.
**Setup:**
```bash
pip install drain3
```
See [Module 2 practice guide](../phases/phase-3-log-intelligence/practice/module-2-log-parser.md) for usage.

### Logparser
**Repo:** https://github.com/logpai/logparser
**What it does:** Benchmark suite with 13 log parsing algorithms (Drain, Spell, AEL, IPLoM, etc.) and the Loghub datasets.
**When to use:** If you want to benchmark Drain against alternatives on your log format.

### DeepLog
**Repo:** https://github.com/wuyifan18/DeepLog
**What it does:** LSTM trained on sequences of log event keys. Detects anomalous log sequences.
**When to use:** After Drain3 + DBSCAN, if you still miss sequential anomalies.

---

## Root Cause Analysis

### Causal-learn (py-why)
**Repo:** https://github.com/py-why/causal-learn
**What it does:** Causal discovery algorithms: PC (constraint-based), GES (score-based), LiNGAM (non-Gaussian).
**Setup:**
```bash
pip install causal-learn
```

### CIRCA (NetManAIOps)
**Repo:** https://github.com/NetManAIOps/CIRCA
**What it does:** Full RCA pipeline from NeurIPS 2022. Includes dataset, evaluation, and three RCA algorithms.
**When to use:** Study the codebase to understand how production RCA is evaluated. The `circa/alg/` directory is the core.

### MicroTosca (University of Pisa)
**Repo:** https://github.com/di-unipi-socc/microTosca
**What it does:** Topology-aware modeling for microservice architectures. Identifies architectural smells that cause operational problems.
**When to use:** Reference for understanding how topology shapes RCA — study alongside `graph_builder.py` in Module 3.

---

## Capacity Planning

### Prophet (Meta)
**Repo:** https://github.com/facebook/prophet
**What it does:** Time series forecasting with automatic seasonality detection and holiday effects.
**Setup:**
```bash
pip install prophet
```
See [Module 4 practice guide](../phases/phase-5-capacity-planning/practice/module-4-forecasting.md) for usage.

### NeuralForecast (Nixtla)
**Repo:** https://github.com/Nixtla/neuralforecast
**What it does:** Deep learning forecasting — NHITS, NBEATS, TFT. When Prophet accuracy is insufficient.
**Setup:**
```bash
pip install neuralforecast
```

### Karpenter (AWS)
**Repo:** https://github.com/aws/karpenter
**What it does:** Kubernetes node autoscaler. Study `pkg/controllers/provisioning/` to understand how production scaling decisions are made from metrics.
**When to use:** Reference for production-grade scaling logic, not a library to import.
