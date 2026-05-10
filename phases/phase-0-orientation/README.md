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
