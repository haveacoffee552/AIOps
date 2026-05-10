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
