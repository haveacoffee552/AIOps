# AIOps Learning Roadmap — Content Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build out the full AIOps learning route map as a structured set of Markdown files the learner will navigate phase by phase.

**Architecture:** One Markdown file per learning unit, organized in phase directories under `phases/`. A top-level `ROADMAP.md` provides navigation. A `resources/` directory centralizes datasets, papers, and open-source refs. A `progress.md` tracks completion.

**Tech Stack:** Markdown, Git (frequent commits per task)

---

## File Map

| File | Responsibility |
|---|---|
| `README.md` | Project intro, quick-start, link to ROADMAP |
| `ROADMAP.md` | 7-phase timeline table, phase summaries, navigation links |
| `progress.md` | Full checkbox tracker — one entry per learning unit |
| `phases/phase-0-orientation/README.md` | AIOps landscape, setup, first readings |
| `phases/phase-1-ml-foundations/README.md` | Phase overview + links to blocks |
| `phases/phase-1-ml-foundations/block-a-python-for-data.md` | NumPy/Pandas/Matplotlib for ops data |
| `phases/phase-1-ml-foundations/block-b-core-ml-concepts.md` | Isolation Forest, DBSCAN, k-means, LSTM basics |
| `phases/phase-1-ml-foundations/block-c-time-series.md` | STL, SARIMA, Prophet, anomaly methods |
| `phases/phase-2-anomaly-detection/README.md` | Theory: z-score, Bollinger Bands, Autoencoders, alert fatigue |
| `phases/phase-2-anomaly-detection/practice/module-1-anomaly-detector.md` | Step-by-step capstone module 1 build guide |
| `phases/phase-3-log-intelligence/README.md` | Theory: Drain, DBSCAN on logs, DeepLog, NLP basics |
| `phases/phase-3-log-intelligence/practice/module-2-log-parser.md` | Step-by-step capstone module 2 build guide |
| `phases/phase-4-root-cause-analysis/README.md` | Theory: event correlation, causality, graph RCA |
| `phases/phase-4-root-cause-analysis/practice/module-3-rca-engine.md` | Step-by-step capstone module 3 build guide |
| `phases/phase-5-capacity-planning/README.md` | Theory: workload characterization, Prophet, LSTM forecasting |
| `phases/phase-5-capacity-planning/practice/module-4-forecasting.md` | Step-by-step capstone module 4 build guide |
| `phases/phase-6-capstone/README.md` | Integration week-by-week guide, MLOps, hardening |
| `phases/phase-6-capstone/architecture.md` | Full capstone system architecture diagram (ASCII) + API contract |
| `resources/datasets.md` | NAB, AIOPS Challenge, Loghub — download links + usage notes |
| `resources/papers.md` | Annotated reading list with why each paper matters |
| `resources/open-source.md` | All open-source projects consolidated with setup instructions |

---

## Task 1: README and ROADMAP scaffolding

**Files:**
- Create: `README.md`
- Create: `ROADMAP.md`

- [ ] **Step 1: Create README.md**

```markdown
# AIOps Learning Platform

A 7-month self-paced route map for DevOps/SRE engineers learning to build AIOps tools from zero.

## Who This Is For

- DevOps/SRE engineers with infrastructure experience but no ML background
- Goal: build AIOps tools for your own team (anomaly detection, log intelligence, RCA, capacity planning)

## How to Use This Repo

1. Start at [ROADMAP.md](ROADMAP.md) — get the full picture
2. Work through `phases/` in order — each phase links to the next
3. Track your progress in [progress.md](progress.md)
4. All datasets, papers, and open-source tools are in [resources/](resources/)

## Capstone Project

Phases 2–6 each add one module to a single unified AIOps platform (`aiops-platform/`). By the end you have a working system running against your real infrastructure.

## Time Commitment

5–10 hours/week over ~7 months.
```

- [ ] **Step 2: Create ROADMAP.md**

```markdown
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
```

- [ ] **Step 3: Commit**

```bash
git add README.md ROADMAP.md
git commit -m "feat: add README and ROADMAP scaffolding"
```

---

## Task 2: Progress tracker

**Files:**
- Create: `progress.md`

- [ ] **Step 1: Create progress.md**

```markdown
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

## Phase 6 — Capstone Integration + MLOps (Month 7)

### Week 1–2: Integration
- [ ] Unified data pipeline (OTel → feature store → model layer)
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
```

- [ ] **Step 2: Commit**

```bash
git add progress.md
git commit -m "feat: add progress tracker with full phase checklist"
```

---

## Task 3: Phase 0 — Orientation guide

**Files:**
- Create: `phases/phase-0-orientation/README.md`

- [ ] **Step 1: Create the directory and file**

```markdown
# Phase 0 — AIOps Orientation

**Duration:** Week 1–2 | **Hours:** 5–10 hrs total

## Goal

Understand what AIOps is, what problems it solves, and how the commercial and open-source ecosystems are structured — before writing a single line of code.

## What Is AIOps?

AIOps (Artificial Intelligence for IT Operations) applies ML to the three pillars of observability — **metrics, logs, and traces** — to automate detection, correlation, and remediation of operational problems.

The core value proposition: your infrastructure generates more signal than humans can process manually. AIOps filters noise, correlates events across systems, and surfaces actionable insights.

**The AIOps stack (simplified):**
```
Data Sources          ML Layer               Action Layer
─────────────         ────────               ────────────
Metrics (Prometheus)  Anomaly Detection  →   Alert with severity score
Logs (Loki/ELK)   →  Log Intelligence   →   Incident correlation
Traces (Jaeger)       Root Cause Analysis→   RCA report
                      Capacity Forecasting→  Proactive scaling
```

## Reading List (do in order)

1. **CNCF TAG Observability Whitepaper** — establishes the vocabulary you'll use throughout this roadmap (metrics, logs, traces, events, profiles). Free PDF at cncf.io.
2. **Gartner Market Guide for AIOps Platforms** — understand what vendors claim vs what they actually do. Focus on the "Market Definition" and "Representative Vendors" sections.
3. **"AIOps: Real-World Challenges and Research Innovations"** (IBM Research, 2017) — a practitioner's view of what's hard. Skim for context, not depth.

## Commercial Survey (1 hour, no sign-up required)

For each product, read the product page and one customer case study. Answer: *what problem does this solve, and how do they describe the ML doing it?*

- **Datadog AIOps / Watchdog** — anomaly detection + incident correlation
- **Dynatrace Davis AI** — deterministic AI for RCA
- **Moogsoft** — event correlation and noise reduction

## Dev Environment Setup

> **[SKIP if already set up]** — If you have Python 3.11+, Jupyter, VS Code, and Docker running, move on.

```bash
# Verify Python version
python --version  # Should be 3.11+

# Install core data science packages
pip install numpy pandas matplotlib seaborn scikit-learn jupyter

# Verify Docker
docker run hello-world
```

Create your capstone repo now — you'll add to it every phase:
```bash
mkdir aiops-platform && cd aiops-platform
git init
echo "# AIOps Platform" > README.md
git add README.md && git commit -m "init: aiops-platform capstone repo"
```

## Done When

- [ ] You can explain what AIOps is to a colleague in 2 minutes
- [ ] You know what Drain, Isolation Forest, and Prophet are (at a concept level — not implementation)
- [ ] Your dev environment is working
- [ ] `aiops-platform` repo exists with initial commit
```

- [ ] **Step 2: Commit**

```bash
git add phases/phase-0-orientation/README.md
git commit -m "feat: add Phase 0 orientation guide"
```

---

## Task 4: Phase 1 — ML Foundations (overview + Block A)

**Files:**
- Create: `phases/phase-1-ml-foundations/README.md`
- Create: `phases/phase-1-ml-foundations/block-a-python-for-data.md`

- [ ] **Step 1: Create phases/phase-1-ml-foundations/README.md**

```markdown
# Phase 1 — ML Foundations for Ops Engineers

**Duration:** Month 1–2 (8 weeks) | **Hours:** ~40–80 hrs total

## Goal

Learn the slice of ML that AIOps actually uses. Not all of ML — just the techniques you'll reach for in Phases 2–5.

## Three Blocks

| Block | Focus | Duration |
|---|---|---|
| [A — Python for Data](block-a-python-for-data.md) | NumPy, Pandas, Matplotlib with time series data | Week 1–2 |
| [B — Core ML Concepts](block-b-core-ml-concepts.md) | Isolation Forest, DBSCAN, k-means, LSTM | Week 3–5 |
| [C — Time Series Analysis](block-c-time-series.md) | STL, SARIMA, Prophet, anomaly methods | Week 6–8 |

## Key Resource

*Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow* — Aurélien Géron (O'Reilly, 3rd ed.)

Read **only these chapters** (skip the rest):
- Ch 1–4: ML landscape, end-to-end project, classification, training models
- Ch 8–9: Dimensionality reduction, unsupervised learning
- Ch 15: Processing sequences (LSTM basics)

## What You Already Know (Skip List)

As a DevOps/SRE engineer you already know:
- What Prometheus metrics look like (gauge, counter, histogram)
- What log lines look like and why they're hard to parse at scale
- What distributed traces are (spans, services, latency)
- Docker, Linux, scripting

The ML blocks build on this. Examples use Prometheus-style data throughout.
```

- [ ] **Step 2: Create phases/phase-1-ml-foundations/block-a-python-for-data.md**

```markdown
# Block A — Python for Data

**Duration:** Week 1–2 | **Focus:** NumPy, Pandas, Matplotlib with time series data

## Why This Matters for AIOps

Your metrics are time series. Your logs are sequences of strings. Before any ML, you need to load, reshape, and visualize this data fluently. Pandas is the lingua franca for this work.

## NumPy Essentials

The only NumPy you need for AIOps:

```python
import numpy as np

# Arrays
arr = np.array([1.0, 2.0, 3.0])
arr.mean()       # 2.0
arr.std()        # standard deviation
arr.min(), arr.max()

# Operations used constantly in anomaly detection
z_scores = (arr - arr.mean()) / arr.std()

# Rolling window (manual, before you learn Pandas)
window = 5
rolling_mean = np.convolve(arr, np.ones(window)/window, mode='valid')
```

## Pandas for Time Series

```python
import pandas as pd

# Load a CSV Prometheus export
# Typical format: timestamp, metric_name, value, labels
df = pd.read_csv('prometheus_export.csv', parse_dates=['timestamp'])
df = df.set_index('timestamp').sort_index()

# Resample to 1-minute intervals
df_1m = df['cpu_usage'].resample('1min').mean()

# Rolling statistics — the foundation of many AIOps baselines
rolling_mean = df_1m.rolling(window=60).mean()    # 1-hour rolling mean
rolling_std  = df_1m.rolling(window=60).std()

# Lag features — used in time series ML
df['lag_1']  = df['cpu_usage'].shift(1)
df['lag_60'] = df['cpu_usage'].shift(60)

# Boolean indexing — find spikes
spikes = df[df['cpu_usage'] > (rolling_mean + 3 * rolling_std)]
```

## Matplotlib for Ops Visualization

```python
import matplotlib.pyplot as plt

fig, axes = plt.subplots(2, 1, figsize=(14, 6), sharex=True)

# Top: raw metric with rolling mean
axes[0].plot(df.index, df['cpu_usage'], alpha=0.5, label='CPU %')
axes[0].plot(df.index, rolling_mean, color='red', label='60-min mean')
axes[0].fill_between(df.index,
    rolling_mean - 3*rolling_std,
    rolling_mean + 3*rolling_std,
    alpha=0.2, label='3σ band')
axes[0].legend()
axes[0].set_title('CPU Usage with Dynamic Threshold')

# Bottom: z-score
z = (df['cpu_usage'] - rolling_mean) / rolling_std
axes[1].plot(df.index, z, color='orange')
axes[1].axhline(3, color='red', linestyle='--', label='3σ threshold')
axes[1].set_title('Z-Score')
axes[1].legend()

plt.tight_layout()
plt.savefig('cpu_analysis.png', dpi=150)
```

## Practice Exercise

**Goal:** Load real Prometheus data, plot it, identify outliers visually.

1. Export 7 days of CPU, memory, and request rate data from your Prometheus via:
   ```
   http://localhost:9090/api/v1/query_range?query=node_cpu_seconds_total&start=...&end=...&step=60
   ```
   Save as CSV.

2. Load into Pandas, resample to 1-minute intervals, plot all three metrics.

3. Compute 1-hour rolling mean and 3σ bands for CPU. Mark where CPU exceeded the band.

4. Answer these questions by looking at the chart:
   - Is the CPU pattern seasonal (daily/weekly cycle)?
   - Are outliers correlated with request rate spikes?
   - What does "normal" look like for your service?

**Done when:** You have a saved `cpu_analysis.png` and can answer the 3 questions above.
```

- [ ] **Step 3: Commit**

```bash
git add phases/phase-1-ml-foundations/
git commit -m "feat: add Phase 1 ML foundations overview and Block A"
```

---

## Task 5: Phase 1 — Block B and Block C

**Files:**
- Create: `phases/phase-1-ml-foundations/block-b-core-ml-concepts.md`
- Create: `phases/phase-1-ml-foundations/block-c-time-series.md`

- [ ] **Step 1: Create block-b-core-ml-concepts.md**

```markdown
# Block B — Core ML Concepts

**Duration:** Week 3–5 | **Focus:** Algorithms you will actually use in AIOps

## The AIOps ML Toolkit

AIOps uses **unsupervised learning** almost exclusively — you rarely have labeled data saying "this was an anomaly." The algorithms below are the ones you'll reach for in Phases 2–5.

## Isolation Forest (your primary anomaly detector)

Isolates anomalies by randomly partitioning data. Anomalies need fewer cuts to isolate — they're unusual. Returns a score, not just a binary label.

```python
from sklearn.ensemble import IsolationForest
import numpy as np

# Simulate 1 week of CPU data with injected anomalies
np.random.seed(42)
normal = np.random.normal(loc=50, scale=5, size=1000)
anomalies = np.array([95, 92, 88, 91])          # injected spikes
data = np.concatenate([normal, anomalies]).reshape(-1, 1)

# Train — contamination = expected fraction of anomalies
clf = IsolationForest(contamination=0.004, random_state=42)
clf.fit(data)

# Predict: -1 = anomaly, 1 = normal
predictions = clf.predict(data)
scores = clf.score_samples(data)               # lower = more anomalous

anomaly_indices = np.where(predictions == -1)[0]
print(f"Detected {len(anomaly_indices)} anomalies at indices: {anomaly_indices}")
```

**Key parameter:** `contamination` — set to your expected anomaly rate. Start at 0.01 (1%) and tune using precision/recall.

## DBSCAN (for log clustering and event grouping)

Density-based clustering — finds clusters of arbitrary shape and labels outliers as noise (-1). You don't need to specify the number of clusters upfront.

```python
from sklearn.cluster import DBSCAN
from sklearn.preprocessing import StandardScaler

# After Phase 3 you'll cluster log embeddings — here we use numeric features
features = np.array([[1,2],[2,2],[2,3],[8,7],[8,8],[25,80]])
features_scaled = StandardScaler().fit_transform(features)

db = DBSCAN(eps=0.5, min_samples=2)
labels = db.fit_predict(features_scaled)
# -1 = noise/outlier, 0,1,2... = cluster IDs
```

**Key parameters:** `eps` (neighborhood radius) and `min_samples` (min points to form cluster). Tune with silhouette score.

## k-means (for grouping similar metrics or events)

Partitions data into k clusters by minimizing intra-cluster variance. Use when you know roughly how many groups you expect.

```python
from sklearn.cluster import KMeans
from sklearn.metrics import silhouette_score

# Find optimal k with elbow method
inertias = []
for k in range(2, 10):
    km = KMeans(n_clusters=k, random_state=42, n_init=10)
    km.fit(features_scaled)
    inertias.append(km.inertia_)

# Use silhouette score to confirm k
km_best = KMeans(n_clusters=3, random_state=42, n_init=10)
labels = km_best.fit_predict(features_scaled)
print(f"Silhouette score: {silhouette_score(features_scaled, labels):.3f}")
# Score > 0.5 is reasonable, > 0.7 is good
```

## Evaluation Metrics

You need these to know if your model is actually working.

```python
from sklearn.metrics import precision_score, recall_score, f1_score

# true_labels: 1=anomaly, 0=normal (you label a sample manually to evaluate)
true_labels  = np.array([0,0,0,1,0,1,0,0,1,0])
pred_labels  = np.array([0,0,1,1,0,1,0,0,0,0])

precision = precision_score(true_labels, pred_labels)  # of detected, how many real?
recall    = recall_score(true_labels, pred_labels)     # of real, how many caught?
f1        = f1_score(true_labels, pred_labels)         # harmonic mean

print(f"Precision: {precision:.2f}  Recall: {recall:.2f}  F1: {f1:.2f}")
```

**For anomaly detection, recall matters more than precision.** Missing a real anomaly (false negative) is worse than a false alarm.

## Practice Exercise

1. Generate 2000 CPU data points: 1950 normal (mean=50, std=5), 50 anomalies (mean=90, std=3).
2. Train an Isolation Forest with `contamination=0.025`.
3. Compute precision, recall, F1 against your known anomaly labels.
4. Try `contamination=0.01` and `contamination=0.05` — observe the trade-off.
5. Plot the data with anomalies colored red.

**Done when:** F1 > 0.7 with `contamination=0.025` on the synthetic data.
```

- [ ] **Step 2: Create block-c-time-series.md**

```markdown
# Block C — Time Series Analysis

**Duration:** Week 6–8 | **Focus:** STL, SARIMA, Prophet, anomaly on time series

## Why Time Series Is Different

Standard ML assumes samples are i.i.d. (independent and identically distributed). Time series data is neither — each point depends on its neighbors, and there are seasonal patterns (daily, weekly) that must be modeled, not treated as noise.

## Key Concepts

**Stationarity:** A time series is stationary when its mean and variance don't change over time. Most ML models assume stationarity. You must check for it and transform if needed.

```python
from statsmodels.tsa.stattools import adfuller

result = adfuller(df['cpu_usage'].dropna())
print(f"ADF Statistic: {result[0]:.4f}")
print(f"p-value: {result[1]:.4f}")
# p < 0.05 = stationary (good). p > 0.05 = non-stationary, apply differencing.
```

## STL Decomposition

Separates a time series into Trend + Seasonal + Residual components. The residual is what you run anomaly detection on — after removing expected patterns.

```python
from statsmodels.tsa.seasonal import STL

stl = STL(df['cpu_usage'], period=1440)  # 1440 = minutes per day for 1-min data
result = stl.fit()

trend    = result.trend
seasonal = result.seasonal
residual = result.resid

# Anomaly detection on the residual (actual surprise, not seasonal spike)
from sklearn.ensemble import IsolationForest
iso = IsolationForest(contamination=0.01, random_state=42)
anomalies = iso.fit_predict(residual.values.reshape(-1,1))
```

## Facebook Prophet

Business-friendly forecasting. Handles daily/weekly/yearly seasonality automatically. Returns a forecast with uncertainty intervals — use the interval to flag anomalies.

```python
from prophet import Prophet
import pandas as pd

# Prophet requires columns named 'ds' (datetime) and 'y' (value)
df_prophet = df[['cpu_usage']].reset_index()
df_prophet.columns = ['ds', 'y']

m = Prophet(
    changepoint_prior_scale=0.05,   # sensitivity to trend changes
    seasonality_mode='multiplicative'
)
m.fit(df_prophet)

future = m.make_future_dataframe(periods=60, freq='min')  # forecast 1 hour ahead
forecast = m.predict(future)

# Flag actuals outside the 95% uncertainty interval as anomalies
merged = df_prophet.merge(forecast[['ds','yhat','yhat_lower','yhat_upper']], on='ds')
merged['anomaly'] = (merged['y'] < merged['yhat_lower']) | (merged['y'] > merged['yhat_upper'])
```

## Comparing Anomaly Detection Approaches

| Method | Best For | Weakness |
|---|---|---|
| Z-score | Fast baseline, stationary data | Fails with seasonality |
| IQR | Robust to outliers in baseline | Same seasonality problem |
| STL + Isolation Forest | Seasonal data (metrics) | Needs enough history for STL |
| Prophet | Forecasting + anomaly | Slow to train, needs weeks of data |
| LSTM Autoencoder | Complex multivariate patterns | High complexity, slow |

## Practice Exercise — Numenta Anomaly Benchmark (NAB)

1. Download NAB: `git clone https://github.com/numenta/NAB`
2. Load `realKnownCause/machine_temperature_system_failure.csv`
3. Apply STL decomposition, plot the three components
4. Run z-score on the residual → compute F1 against NAB's ground truth labels
5. Run Isolation Forest on the residual → compare F1
6. Run Prophet on the full series → compare F1

**Done when:** You have a comparison table showing F1 for each method, and you can explain *why* one method outperforms the others on this specific dataset.
```

- [ ] **Step 3: Commit**

```bash
git add phases/phase-1-ml-foundations/block-b-core-ml-concepts.md
git add phases/phase-1-ml-foundations/block-c-time-series.md
git commit -m "feat: add Phase 1 Block B and Block C guides"
```

---

## Task 6: Phase 2 — Anomaly Detection theory + practice guide

**Files:**
- Create: `phases/phase-2-anomaly-detection/README.md`
- Create: `phases/phase-2-anomaly-detection/practice/module-1-anomaly-detector.md`

- [ ] **Step 1: Create phases/phase-2-anomaly-detection/README.md**

```markdown
# Phase 2 — Anomaly Detection & Alerting

**Duration:** Month 3 | **Capstone output:** Module 1 — live anomaly detector on Prometheus

## Theory

### Why Static Thresholds Fail

Static thresholds (`alert if CPU > 80%`) cause alert fatigue because:
- Normal peaks (deployments, batch jobs, traffic spikes) trigger false positives
- Gradual degradation below threshold goes undetected
- Every service has different "normal" — one threshold doesn't fit all

### Dynamic Thresholding Methods

**Bollinger Bands:** Rolling mean ± k×rolling_std. Simple and effective for stable services.
```python
window = 60  # 60-minute rolling window
mean = series.rolling(window).mean()
std  = series.rolling(window).std()
upper_band = mean + 3 * std
lower_band = mean - 3 * std
anomaly = (series > upper_band) | (series < lower_band)
```

**Holt-Winters (Exponential Smoothing):** Handles trend and seasonality with exponential weights. Better than Bollinger Bands when your metric has a clear daily cycle.
```python
from statsmodels.tsa.holtwinters import ExponentialSmoothing
model = ExponentialSmoothing(series, trend='add', seasonal='add', seasonal_periods=1440)
fit = model.fit()
forecast = fit.fittedvalues
residuals = series - forecast
anomaly = residuals.abs() > (3 * residuals.std())
```

**Isolation Forest:** Learns what "normal" looks like from a training window. No need to specify thresholds. Best when you have multiple correlated metrics as features.

**LSTM Autoencoder:** Learns to reconstruct normal sequences. High reconstruction error = anomaly. Use when simpler methods miss anomalies in complex multi-variate patterns. Only reach for this if Isolation Forest is insufficient.

### Severity Scoring

Don't output binary anomaly/not-anomaly. Score each anomaly:
```python
# Normalize isolation score to 0–1 severity
raw_score = clf.score_samples(X)           # more negative = more anomalous
severity  = 1 - (raw_score - raw_score.min()) / (raw_score.max() - raw_score.min())
```

## Open-Source Projects to Study

| Project | What to look at |
|---|---|
| [Luminol](https://github.com/linkedin/luminol) | `luminol/algorithms/` — how LinkedIn implements bitmap and derivative algorithms |
| [Alibi-Detect](https://github.com/SeldonIO/alibi-detect) | `alibi_detect/od/iforest.py` — production Isolation Forest wrapper |
| [Prometheus Anomaly Detector](https://github.com/AICoE/prometheus-anomaly-detector) | `app.py` — how to query Prometheus API and feed results to ML |

Spend 1–2 hours reading each codebase before starting Module 1.

## Proceed to Practice

→ [Module 1: Build the Live Anomaly Detector](practice/module-1-anomaly-detector.md)
```

- [ ] **Step 2: Create practice/module-1-anomaly-detector.md**

```markdown
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
    ("node_cpu_seconds_total{mode='idle'}", "cpu_idle"),
    ("node_memory_MemAvailable_bytes",       "mem_available"),
    ("http_requests_total",                  "http_requests"),
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
```

- [ ] **Step 3: Commit**

```bash
git add phases/phase-2-anomaly-detection/
git commit -m "feat: add Phase 2 anomaly detection theory and Module 1 practice guide"
```

---

## Task 7: Phase 3 — Log Intelligence theory + practice guide

**Files:**
- Create: `phases/phase-3-log-intelligence/README.md`
- Create: `phases/phase-3-log-intelligence/practice/module-2-log-parser.md`

- [ ] **Step 1: Create phases/phase-3-log-intelligence/README.md**

```markdown
# Phase 3 — Log Intelligence

**Duration:** Month 4 | **Capstone output:** Module 2 — log parser + anomaly correlator

## Theory

### The Log Parsing Problem

Raw logs are unstructured strings. Before any ML, you must extract a **template** (the static part) from the **parameters** (the dynamic part):

```
Raw:      "User john connected from 192.168.1.5 at 14:32:01"
Template: "User <*> connected from <*> at <*>"
Params:   ["john", "192.168.1.5", "14:32:01"]
```

### Drain Algorithm

Drain is the de facto standard for online log parsing. It uses a fixed-depth parse tree:
- Depth 1: branch by log length
- Depth 2: branch by first token
- Leaf: cluster of similar log messages sharing a template

Key property: **streaming** — processes logs one by one, O(1) amortized per log.

### Log Clustering with DBSCAN

After parsing, represent each log template as a TF-IDF vector. Cluster templates with DBSCAN. Clusters correspond to "log types." Points labeled -1 (noise) are rare/novel log patterns — high-value anomaly signal.

### DeepLog

LSTM trained on sequences of log event IDs. Given a window of recent events, predicts what the next event should be. If the actual next event is not in the top-k predictions → anomaly.

Use DeepLog when Drain + clustering misses anomalies in the *sequence* of events (not just unusual individual log lines).

## Open-Source Projects to Study

| Project | What to look at |
|---|---|
| [Drain3](https://github.com/logpai/Drain3) | `drain3/drain.py` — the core parse tree implementation |
| [Logparser](https://github.com/logpai/logparser) | `logparser/Drain/` — benchmark implementation + datasets |
| [DeepLog](https://github.com/wuyifan18/DeepLog) | `deeplog.py` — LSTM anomaly detection on log key sequences |

## Proceed to Practice

→ [Module 2: Build the Log Intelligence Pipeline](practice/module-2-log-parser.md)
```

- [ ] **Step 2: Create practice/module-2-log-parser.md**

```markdown
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
```

- [ ] **Step 3: Commit**

```bash
git add phases/phase-3-log-intelligence/
git commit -m "feat: add Phase 3 log intelligence theory and Module 2 practice guide"
```

---

## Task 8: Phase 4 — Root Cause Analysis theory + practice guide

**Files:**
- Create: `phases/phase-4-root-cause-analysis/README.md`
- Create: `phases/phase-4-root-cause-analysis/practice/module-3-rca-engine.md`

- [ ] **Step 1: Create phases/phase-4-root-cause-analysis/README.md**

```markdown
# Phase 4 — Root Cause Analysis & Incident Correlation

**Duration:** Month 5 | **Capstone output:** Module 3 — incident correlator + RCA scorer

## Theory

### Event Correlation

**Temporal correlation:** Group alerts that fire within a time window. Simple, but misses causality — two unrelated services can alert at the same time.

**Topological correlation:** Use the service dependency graph to understand which alerts are *upstream* of others. If service A calls B, and both alert, B's alert is probably caused by A.

### Why Correlation ≠ Causality

In distributed systems, a single root cause cascades: database slow → API timeout → frontend error → user-facing alert. Temporal correlation groups all four. Topological correlation points upstream to the database.

Causality requires knowing the graph *and* the direction of propagation.

### Graph-Based RCA

1. Build a directed graph: node = service, edge = "A calls B"
2. When an incident occurs, walk the graph upstream from the alerting nodes
3. Score each upstream service by: number of downstream alerters it can reach × alert severity
4. Highest score = most likely root cause

### Building the Dependency Graph

Source the graph from your existing telemetry — don't maintain it manually:
- **OpenTelemetry traces:** parent span → child span = caller → callee
- **Service mesh (Istio/Linkerd):** mTLS topology is the graph
- **Jaeger:** trace view shows call chain directly

## Open-Source Projects to Study

| Project | What to look at |
|---|---|
| [Causal-learn](https://github.com/py-why/causal-learn) | `causallearn/search/ConstraintBased/PC.py` — PC algorithm for causal discovery |
| [CIRCA](https://github.com/NetManAIOps/CIRCA) | `circa/alg/` — production RCA algorithms from NeurIPS 2022 |
| [MicroTosca](https://github.com/di-unipi-socc/microTosca) | `microtosca/` — microservice topology modeling |

## Proceed to Practice

→ [Module 3: Build the RCA Engine](practice/module-3-rca-engine.md)
```

- [ ] **Step 2: Create practice/module-3-rca-engine.md**

```markdown
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
        spans = {s["spanID"]: s for s in trace["spans"]}
        for span in trace["spans"]:
            caller = span["processID"]          # parent service
            callee = span.get("operationName")  # child operation
            if span.get("references"):
                parent_id = span["references"][0]["spanID"]
                if parent_id in spans:
                    parent_service = spans[parent_id]["processID"]
                    G.add_edge(parent_service, span["processID"])
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

def run():
    alerts = load_recent_alerts(window_minutes=10)
    if not alerts:
        print("No recent alerts — no incident to analyze")
        return
    incident  = group_into_incident(alerts)
    graph     = build_dependency_graph(lookback_minutes=60)
    candidates = score_root_causes(graph, incident["affected_metrics"])
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
```

- [ ] **Step 3: Commit**

```bash
git add phases/phase-4-root-cause-analysis/
git commit -m "feat: add Phase 4 RCA theory and Module 3 practice guide"
```

---

## Task 9: Phase 5 — Capacity Planning theory + practice guide

**Files:**
- Create: `phases/phase-5-capacity-planning/README.md`
- Create: `phases/phase-5-capacity-planning/practice/module-4-forecasting.md`

- [ ] **Step 1: Create phases/phase-5-capacity-planning/README.md**

```markdown
# Phase 5 — Capacity Planning & Predictive Scaling

**Duration:** Month 6 | **Capstone output:** Module 4 — saturation forecaster

## Theory

### Workload Characterization

Before forecasting, understand your workload's shape:
- **Diurnal pattern:** Does traffic spike during business hours? Drop at night?
- **Weekly cycle:** Is Monday morning different from Friday afternoon?
- **Growth trend:** Is baseline increasing month over month?

Plot 90 days of data before choosing a forecasting method. Visualizing the pattern tells you which model to use.

### Choosing a Forecasting Method

| Method | Use when |
|---|---|
| Prophet | Clear daily/weekly seasonality, holiday effects, business metrics |
| SARIMA | Stationary or near-stationary data, short horizon (<24h) |
| LSTM | Multiple correlated input features (multivariate), complex patterns |

**Start with Prophet.** It's robust, interpretable, and handles the most common ops patterns (daily cycles, weekly patterns). Only move to LSTM if Prophet's forecast error is too high.

### Saturation Forecasting

You're not forecasting the metric value — you're forecasting *time to saturation* (when a resource hits its limit).

```
saturation_time = time when forecast crosses threshold (e.g., 80% CPU)
```

### Proactive Alerting

Integrate with Module 1: instead of alerting when CPU *is* high, alert when the forecast shows CPU *will hit* 80% within 2 hours. This gives the ops team time to act before degradation.

## Open-Source Projects to Study

| Project | What to look at |
|---|---|
| [Prophet](https://github.com/facebook/prophet) | `python/prophet/forecaster.py` — how seasonality is modeled |
| [NeuralForecast](https://github.com/Nixtla/neuralforecast) | `neuralforecast/models/` — NHITS and NBEATS for ops forecasting |
| [Karpenter](https://github.com/aws/karpenter) | `pkg/controllers/provisioning/` — how production autoscaling decisions are made |

## Proceed to Practice

→ [Module 4: Build the Saturation Forecaster](practice/module-4-forecasting.md)
```

- [ ] **Step 2: Create practice/module-4-forecasting.md**

```markdown
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
```

- [ ] **Step 3: Commit**

```bash
git add phases/phase-5-capacity-planning/
git commit -m "feat: add Phase 5 capacity planning theory and Module 4 practice guide"
```

---

## Task 10: Phase 6 — Capstone integration guide + architecture

**Files:**
- Create: `phases/phase-6-capstone/README.md`
- Create: `phases/phase-6-capstone/architecture.md`

- [ ] **Step 1: Create phases/phase-6-capstone/README.md**

```markdown
# Phase 6 — Capstone Integration + MLOps in Production

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
```

- [ ] **Step 2: Create phases/phase-6-capstone/architecture.md**

```markdown
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
```

- [ ] **Step 3: Commit**

```bash
git add phases/phase-6-capstone/
git commit -m "feat: add Phase 6 capstone integration guide and system architecture"
```

---

## Task 11: Resources directory

**Files:**
- Create: `resources/datasets.md`
- Create: `resources/papers.md`
- Create: `resources/open-source.md`

- [ ] **Step 1: Create resources/datasets.md**

```markdown
# Datasets

## Numenta Anomaly Benchmark (NAB)

**Use:** Phase 1 Block C practice, Phase 2 theory validation

```bash
git clone https://github.com/numenta/NAB
```

Key files:
- `data/realKnownCause/machine_temperature_system_failure.csv` — real sensor data with known anomalies
- `data/artificialWithAnomaly/` — synthetic data for controlled experiments
- `labels/combined_labels.json` — ground truth anomaly timestamps

Ground truth labels let you compute precision/recall — use this to evaluate your anomaly detector before running it against real infrastructure.

## AIOPS Challenge Datasets (2018–2022)

**Use:** Phases 2–4 (anomaly detection, log parsing, RCA)

Download from: https://competition.aiops-challenge.com (registration required — free)

Key datasets:
- **2018:** KPI anomaly detection — 58 real KPI time series with ground truth labels
- **2020:** Metric and log correlation challenge
- **2022:** Multivariate anomaly detection in microservices

The 2018 KPI dataset is the most widely used benchmark in academic AIOps papers — your results are directly comparable to published work.

## Loghub

**Use:** Phase 3 log intelligence

```bash
git clone https://github.com/logpai/loghub
```

Contains 16 real log datasets from different systems (Hadoop, HDFS, Apache, OpenStack, etc.) with labeled anomalies for some datasets. Use `HDFS/HDFS_2k.log` to start — it's small and well-documented.
```

- [ ] **Step 2: Create resources/papers.md**

```markdown
# Papers Reading List

## Core Papers (read in this order)

### 1. AIOps Overview
**"AIOps: Real-World Challenges and Research Innovations"**
IBM Research, 2017.
*Why read:* A practitioner's taxonomy of AIOps problems. Sets vocabulary for the entire field. 15-minute read. Skim for context in Phase 0.

### 2. Log Parsing
**"Drain: An Online Log Parsing Approach with Fixed Depth Tree"**
He et al., ICWS 2017.
*Why read:* Drain is the algorithm you'll use in Module 2. Reading the paper first means you understand *why* the parse tree is structured the way it is — not just how to call the API.
Find at: arXiv or IEEE Xplore.

### 3. Log Anomaly Detection
**"DeepLog: Anomaly Detection and Diagnosis from System Logs through Deep Learning"**
Du et al., CCS 2017.
*Why read:* Foundation paper for LSTM-based log anomaly detection. The key insight — model log event sequences, not individual log lines — applies beyond this specific paper.

### 4. Root Cause Analysis
**"CIRCA: Causal Inference for Root Cause Analysis of Microservice Systems"**
Ding et al., NeurIPS 2022.
*Why read:* Best recent paper on production RCA. Read the "Problem Formulation" section carefully — it formalizes what you're building in Module 3.

## Extended Reading (after the capstone)

- **"Unsupervised Anomaly Detection via Variational Auto-Encoder"** (Kingma & Welling) — if you want to go deeper on autoencoders
- **"N-BEATS: Neural Basis Expansion Analysis for Interpretable Time Series Forecasting"** — if Prophet isn't accurate enough for your use case
- **"Causal Discovery from Observational Data"** (Peters et al.) — if you want rigorous causal inference beyond graph traversal
```

- [ ] **Step 3: Create resources/open-source.md**

```markdown
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
```

- [ ] **Step 4: Commit**

```bash
git add resources/
git commit -m "feat: add resources directory with datasets, papers, and open-source guides"
```

---

## Self-Review

### Spec Coverage Check

| Spec Requirement | Covered By |
|---|---|
| Phase 0 orientation | Task 3 |
| Phase 1 Block A (Python for data) | Task 4 |
| Phase 1 Block B (Core ML) | Task 5 |
| Phase 1 Block C (Time series) | Task 5 |
| Phase 2 anomaly detection theory | Task 6 |
| Phase 2 Module 1 practice | Task 6 |
| Phase 3 log intelligence theory | Task 7 |
| Phase 3 Module 2 practice | Task 7 |
| Phase 4 RCA theory | Task 8 |
| Phase 4 Module 3 practice | Task 8 |
| Phase 5 capacity planning theory | Task 9 |
| Phase 5 Module 4 practice | Task 9 |
| Phase 6 integration + MLOps | Task 10 |
| Capstone architecture | Task 10 |
| Open-source refs (Luminol, Alibi-Detect, PAD, Drain3, Logparser, DeepLog, Causal-learn, CIRCA, Prophet, NeuralForecast, Karpenter) | Task 11 |
| Datasets (NAB, AIOPS Challenge, Loghub) | Task 11 |
| Papers (Drain, DeepLog, CIRCA, AIOps overview) | Task 11 |
| Progress tracker | Task 2 |
| README + ROADMAP | Task 1 |

All spec requirements covered. ✓
