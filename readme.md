# AI-Assisted Hospital Patient Flow Simulation
**Agent-Based Modeling of Organizational Efficiency**

## Overview
This project implements an **agent-based simulation model** to evaluate the **organizational impact of AI-assisted clinical decision support** in a hospital setting.

The model compares two operational scenarios under identical demand and capacity conditions:

- **Baseline scenario**:  
  4 clinicians, traditional decision-making (no AI)
- **AI-assisted scenario**:  
  3 clinicians supported by an AI decision-support tool

The core objective is to assess whether **AI-enabled reductions in decision latency and variability** can compensate for reduced staffing **without degrading organizational performance**.

The project is developed within the context of **Strategic Management, Operations Management, and Systems Thinking**, and is fully documented in the accompanying project report.

---

## Modeled System
The hospital is modeled as a **complex adaptive system** consisting of interacting agents:

### Patient Agents
- Arrive stochastically
- Have heterogeneous severity levels
- Experience **deterioration when waiting**
- Progress through decision, treatment, and discharge stages

### Clinician Agents
- Act as the main decision-making bottleneck
- Decision time depends on workload and congestion
- In the AI-assisted scenario, clinicians retain full control, while AI **reduces decision time and variability**

### AI Decision Support
- Does **not** improve diagnostic accuracy
- Does **not** replace clinicians
- Reduces:
  - Mean decision latency
  - Variability of decision-making
- Modeled as a proportional efficiency gain (10%–40%)

---

## Research Questions
- Can AI-assisted decision support compensate for reduced staffing?
- Under which demand conditions does AI create organizational value?
- How do AI-driven reductions in decision delay affect:
  - Length of Stay (LOS)
  - Throughput
  - Tail performance (95th percentile LOS)
  - System stability and variability?

---

## Key Performance Indicators (KPIs)
The simulation evaluates organizational performance using:

- **Decision Latency**
- **Mean Length of Stay (LOS)**
- **LOS at 95th percentile (LOS p95)**
- **Throughput**
- **Variability and robustness (Monte Carlo statistics)**

All results are obtained through **Monte Carlo simulation (1,000 replications)** to ensure statistical robustness.

---

## Experimental Design
Two demand regimes are analyzed:

- **Low load**: demand below capacity (no structural congestion)
- **High load**: demand near the decision-making bottleneck

The **only structural difference** between scenarios is:
- Number of clinicians
- Presence or absence of AI support

This allows isolation of **organizational effects of AI** from capacity expansion.

---

## Methodology
- **Agent-Based Modeling (ABM)** using discrete-event simulation
- Decision delays generate feedback loops affecting congestion and deterioration
- AI acts as a **process innovation**, reshaping timing and coordination
- Results interpreted through:
  - Healthcare operations theory
  - Systems thinking
  - Value-based healthcare
  - Strategic management frameworks

---

## 🗂 Project Structure
 project/
│── README.md
│── requirements.txt
│
├── src/
│ └── main.ipynb
│
├── results/
│ └── figures/
│
└── report/
└── Quantifying Organizational Efficiency Gains from AI-Driven.pdf


---
## Contributors

- Ehsan Izadi Zamanabadi
- Sina
- Seyed Mahdi Seyedishandiz 
- Reza
---
## How to Run

### Install dependencies
```bash
pip install -r requirements.txt


jupyter notebook src/main.ipynb
