# 2E-LIRAP

# Decision Intelligence for Resilient Reverse Logistics

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Gurobi Optimizer](https://img.shields.io/badge/Gurobi-10.0+-red.svg)](https://www.gurobi.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

> **Official repository** for the code, datasets, and supplementary materials associated with the manuscript:  
> *"Decision Intelligence for Resilient Reverse Logistics: A Three-Phase Matheuristic Framework for the Two-Echelon Location-Inventory-Routing-Assignment Problem (MP-HF-SD-2E-LIRAP)"*  
> Submitted to **Transportation Research Part C: Emerging Technologies** (Special Issue: Boosting Efficiency, Sustainability and Resilience of Logistics Systems: Decision Intelligence with AI and OR).

---

## 📌 Overview

This repository provides an end-to-end **Decision Intelligence Pipeline** that seamlessly integrates Artificial Intelligence (Machine Learning) and Operations Research (Exact MILP and Metaheuristics) to solve the agricultural reverse logistics problem under deep climatic and macroeconomic uncertainty.

### Key Features of the Codebase:
1. **Predictive AI Pipeline:** L2-regularized Artificial Neural Networks (ANN), Verhulst Logistic Growth modeling, and Lognormal Monte Carlo simulations to extract robust $P_{95}$ stress-test capacity bounds.
2. **AI-Driven Structural-Start:** A parameter-free, capacity-driven K-Means clustering algorithm that translates demand gravity into topological archetypes to prevent "cold-start" inefficiencies in metaheuristics.
3. **3-Phase Matheuristic (LIRAP):**
   * *Phase 1:* Strategic Network Design (evaluating topologies via analytical proxies).
   * *Phase 2:* Tactical Set Partitioning MILP (fleet sizing and multi-echelon inventory routing via ALNS Warm-Start).
   * *Phase 3:* Operational Assignment MILP (exact physical vehicle scheduling, deadheading tracking, and equitable workload distribution).
4. **Proxy Border Hub Mechanism:** Algorithmic resolution for unserved micro-regions using an exact $139 \times 139$ over-the-road distance matrix.
5. **GHG Emissions Tracking:** Environmental productivity calculator adopting the **GLEC Framework / ISO 14083** and **CMEM** protocols to measure loaded vs. deadheading carbon footprints.
