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
