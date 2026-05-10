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
