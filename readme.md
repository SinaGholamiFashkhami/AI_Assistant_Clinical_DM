# AI-Assisted Hospital Patient Flow Simulation

Agent-based simulation of organizational efficiency gains from AI-driven clinical decision support.

---

## What this project does

The model compares two hospital operating regimes under identical demand and capacity conditions:

- **Baseline**: 4 clinicians, traditional decision-making
- **AI-assisted**: 3 clinicians supported by an AI decision-support tool

The central question is whether AI-driven reductions in decision latency and variability can compensate for one fewer clinician — and under which conditions that trade-off holds. The scope is deliberately organizational: AI in the model does not improve diagnostic accuracy or replace clinical judgment. It only reduces how long decisions take and how variable that time is.

---

## Background

Healthcare organizations increasingly face simultaneous pressure from rising demand, staffing constraints, and clinician burnout. The standard response — adding capacity — is expensive and often impractical. This project asks a different question: how much of the efficiency loss from reduced staffing can be recovered through process-level improvements alone?

The simulation models patient arrivals as a Poisson process, clinicians as the primary decision bottleneck with workload-dependent latency, and patients as heterogeneous agents with individual severity, wait tolerance, and deterioration dynamics. AI support reduces both the mean and standard deviation of clinician decision time by a configurable effectiveness percentage (10%–40%).

This is a course project developed for Strategic Management / Operations Management at the University of Genoa, accompanied by a full research report (see `report/`).

---

## Key results

Under **low demand** (1 patient per 4 minutes), a 3-clinician AI-assisted team matches baseline performance at approximately 21% AI effectiveness (mean LOS) and 23% (LOS p95). At that demand level AI functions as a cost-efficiency tool rather than a throughput driver — revenue stays constant while staffing costs fall.

Under **high demand** (1 patient per 3.3 minutes), the break-even point shifts to 25–26% effectiveness across LOS and throughput. Below that threshold, reducing staff while AI is underperforming makes congestion significantly worse — mean LOS nearly doubles at 10% effectiveness. Above it, the AI-assisted configuration outperforms the 4-clinician baseline on both mean and tail metrics.

The sensitivity analysis (Section 7.6 of the report, cells [14–15] of the notebook) holds these findings across ±20% variation in inter-arrival time, confirming they are not artifacts of a single demand assumption.

---

## Project structure

```
.
├── README.md
├── requirements.txt
├── src/
│   └── main.ipynb          # Full simulation: model, Monte Carlo sweep, plots
├── results/
│   ├── 3-2/                # Low load, 3.2-min interarrival (4 plots + summary xlsx)
│   ├── 3-3/                # Low load, 3.3-min interarrival
│   ├── 3-4/                # Low load, 3.4-min interarrival
│   ├── 3-9/                # High load, 3.9-min interarrival
│   ├── 4-0/                # Nominal high-load scenario (decision, LOS, throughput plots)
│   ├── 4-1/                # High load, 4.1-min interarrival
│   ├── sensitivity-los.png
│   └── sensitivity-throughput.png
└── report/
    ├── Abstract.docx
    └── Quantifying Organizational Efficiency Gains from AI-Driven.pdf
```

Folder names in `results/` correspond to interarrival time in minutes (e.g., `3-3` = one patient every 3.3 minutes). Each folder contains four KPI plots (decision latency, mean LOS, LOS p95, throughput) and a summary spreadsheet of Monte Carlo statistics.

---

## Running the simulation

**Requirements**: Python 3.10+

```bash
pip install -r requirements.txt
jupyter notebook src/main.ipynb
```

The notebook is organized in 14 numbered cells:

| Cells | Content |
|---|---|
| 1–3 | Imports, parameters, utility functions |
| 4–8 | Agent definitions (Patient, Clinician) and process logic |
| 9 | `run_scenario()` — single simulation run |
| 10–11 | Monte Carlo sweep across AI effectiveness levels (1,000 reps) |
| 12–13 | KPI plots vs AI effectiveness |
| 14–15 | Sensitivity analysis plots (hardcoded pre-computed values) |

A full sweep (1,000 reps × 30 effectiveness levels) takes several minutes on a standard laptop.

---

## Simulation parameters

| Parameter | Baseline value | Notes |
|---|---|---|
| Simulation time | 640 min (8 hrs) | |
| Warm-up period | 120 min | Excluded from KPI collection |
| Interarrival mean | 4 min (low) / 3.33 min (high) | Exponential distribution |
| Clinicians | 4 (baseline) / 3 (AI scenario) | |
| Beds | 15 | Set high to avoid bed bottlenecks |
| Decision latency mean | 12 min | Normal, workload-dependent |
| Decision latency SD | 2 min | |
| Treatment time mean | 30 min | Scaled by patient severity |
| Wait tolerance mean | 25 min | Below this, no deterioration |
| Deterioration rate | 0.03 / min | Applied to excess waiting only |
| AI effectiveness range | 10%–40% | Proportional reduction in mean and SD |
| Monte Carlo replications | 1,000 | Per configuration |

---

## KPIs evaluated

- Mean decision latency
- Mean length of stay (LOS)
- LOS at 95th percentile (LOS p95)
- Throughput (patients / minute)
- LOS standard deviation (stability proxy)

Break-even points — where the 3-clinician AI-assisted configuration matches the 4-clinician baseline — are computed for each KPI and annotated in the plots.

---

## Contributors

- Sina Gholami Fashkhami
- Ehsan Izadi Zamanabadi
- Seyed Mahdi Seyedishandiz
- Reza Dehghani Abbasi

---

## Dependencies

```
numpy>=1.24
pandas>=2.0
simpy>=4.0
matplotlib>=3.7
```

---

## Limitations

Results are not calibrated against real hospital data — parameter choices are informed by the operations management literature and chosen to generate realistic congestion dynamics, not to reproduce a specific institution. The model isolates organizational effects by holding demand, bed capacity, and clinical accuracy constant; it does not capture institutional culture, long-term cost dynamics, or downstream clinical outcomes. See Section 10 of the report for a full discussion.
