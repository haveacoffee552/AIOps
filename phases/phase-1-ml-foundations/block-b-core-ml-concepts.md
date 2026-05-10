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
