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
