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
