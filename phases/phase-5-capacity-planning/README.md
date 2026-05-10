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
