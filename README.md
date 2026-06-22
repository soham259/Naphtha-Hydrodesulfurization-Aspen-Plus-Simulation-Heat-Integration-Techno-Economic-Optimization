# 🛢️ Naphtha Hydrodesulfurization (HDS)
### Process Simulation · Heat Integration · Techno-Economic Analysis

## 📌 Overview

This project presents a **full process simulation, heat integration, and techno-economic analysis** of a Naphtha Hydrodesulfurization (HDS) unit — a critical refinery process that removes sulfur from naphtha before catalytic reforming.

Driven by **India's BS-VI mandate** (≤10 ppm sulfur) and global Euro VI regulations, HDS units are now mandatory across all major refineries. This project simulates an industrial-scale 3,000 kg/hr Naphtha HDS unit using **Aspen Plus V12**, integrates heat recovery using **Aspen Energy Analyzer (AEA)**, and evaluates project economics using **Aspen Process Economic Analyzer (APEA)**.

### Highlights at a Glance

| Metric | Value |
|---|---|
| Feed | 3,000 kg/hr Naphtha (C5–C12) |
| Sulfur Conversion | 100% |
| Regulatory Compliance | BS-VI / Euro VI (≤10 ppm S) |
| Energy Savings (Pinch) | 73.44% |
| CO₂ Reduction | 186.7 kg/hr (69.6%) |
| Total Capital Cost | $7.56M |
| Annual Profit | $19.82M/yr |
| Payback Period | 2.73 years @ 20% ROR |

---

## ⚙️ Software & Tools

| Tool | Version | Purpose |
|---|---|---|
| **Aspen Plus** | V12 | Full process flowsheet simulation |
| **Aspen Energy Analyzer (AEA)** | V12 | Pinch analysis & HEN synthesis |
| **Aspen Process Economic Analyzer (APEA)** | V12 | Capital & operating cost estimation |

**Thermodynamic Model:** Peng-Robinson EOS (Boston-Mathias extrapolation for supercritical H₂)

---

## 🔬 Background & Motivation

- Naphtha (C5–C12) is the primary feedstock for catalytic reforming and petrochemical production.
- Trace sulfur **permanently poisons Pt/Re reforming catalysts** — desulfurization is mandatory before the reformer.
- India's **BS-VI mandate (2020)** required all major refineries (HPCL, BPCL, IOC) to upgrade HDS units.
- HDS processes collectively treat **60–70% of all refinery streams** worldwide.

### HDS Reaction (Simplified)

```
R–SH  +  H₂  →  R–H  +  H₂S        (Co-Mo/Al₂O₃, 350°C, 40 bar)
```

All HDS reactions are **exothermic** (ΔH° ≈ −66 to −280 kJ/mol) and thermodynamically favorable (>99.9% equilibrium conversion at design conditions).

### Why Co-Mo over Ni-Mo?

| Property | Co-Mo/Al₂O₃ ✅ (This Work) | Ni-Mo/Al₂O₃ |
|---|---|---|
| Best for | Naphtha, light feeds | Heavy gas oil, diesel |
| Temperature | 280–340°C | 320–380°C |
| Pressure | 20–50 bar | 40–80 bar |
| H₂ Consumption | Lower | 20–30% higher |
| Pathway | Direct Desulfurization (DDS) | Hydrogenation (HYD) |

---

## 🔧 Process Description

### Process Flowsheet

The simulation was built in Aspen Plus V12 with the following unit operations:

<img width="1097" height="480" alt="image" src="https://github.com/user-attachments/assets/d34e759c-b863-44dd-9bc4-9885a7513111" />


### Step-by-Step Flow

1. **Feed Preparation** — Naphtha (3,000 kg/hr, 25°C, 2 bar) pressurized to 41 bar via PUMP; mixed with fresh H₂ (4.43 kmol/hr) and recycle H₂ (7.04 kmol/hr) in MIXER.

2. **Preheating** — Mixed stream preheated in HX1 (38.8 → 250°C via process-to-process heat exchange), throttled via VALVE (41 → 40 bar), then heated to 350°C in HX2.

3. **Reaction** — RStoic reactor (350°C, 40 bar, isothermal) with Co-Mo/γ-Al₂O₃ catalyst achieves **100% conversion** of all sulfur species to H₂S.

4. **Flash Separation** — Reactor effluent cooled and fed to FLASH (35°C, 4 bar) separating vapor (H₂, H₂S, light HC) from liquid naphtha.

5. **H₂S Removal** — Flash vapor enters ABSORBER with 50 kmol/hr lean amine. H₂S-free H₂ overhead: 10% purged, 90% recompressed (COMP2) and recycled.

6. **Product Recovery** — Flash liquid fed to RadFrac DIST column separating light HC from desulfurized naphtha bottoms (**S14: 2,526 kg/hr at 40°C**).

### Material Balance

| Stream | Flow | Notes |
|---|---|---|
| Naphtha Feed | 3,000 kg/hr | C5–C12, 25°C, 2 bar |
| H₂ Fresh Feed | 4.43 kmol/hr | Limiting reactant |
| H₂ Recycle (S28) | 7.04 kmol/hr | 70–85% H₂ saving |
| H₂S Produced | 81.19 kg/hr | Sent to Claus plant |
| Product Naphtha (S14) | 2,526 kg/hr | Zero detectable sulfur |
| Purge Stream | 11.38 kg/hr | Mostly CH₄ |

---

## 🔥 Heat Integration & Pinch Analysis

Heat integration was performed using **Aspen Energy Analyzer (AEA)** to minimize utility consumption.

<img width="1092" height="565" alt="image" src="https://github.com/user-attachments/assets/83e232e7-d5cf-40ef-a159-a7380d33bbbb" />


### AEA Savings Summary

| Utility | Actual (cal/s) | Target (cal/s) | Savings |
|---|---|---|---|
| Total Utilities | 5.70 × 10⁵ | 1.514 × 10⁵ | **73.44%** |
| Heating Utilities | 3.008 × 10⁵ | 9.151 × 10⁴ | 69.58% |
| Cooling Utilities | 2.692 × 10⁵ | 5.986 × 10⁴ | 77.76% |
| CO₂ Emissions | 268.3 kg/hr | 81.61 kg/hr | **186.7 kg/hr saved** |

### Pinch Analysis Key Results

- **Pinch Point:** 40–50°C (cold composite)
- **Dominant Heat Match:** Hot reactor effluent (S6→S7: 350→35°C) preheats cold mixed feed (S2→S3: 38.8→250°C) via HX1
- **QH,min** = 9.151 × 10⁴ cal/s
- **QC,min** = 5.986 × 10⁴ cal/s
- AEA synthesized **6 candidate HEN designs** (A_Design2 to A_Design6)
- CO₂ reduction equivalent to **$0.4–0.8M/yr** benefit at $50/tonne CO₂ at industrial scale

### Process Streams for HEN (AEA Data)

| Stream | Tin (°C) | Tout (°C) | Type |
|---|---|---|---|
| S6→S7 (Reactor Out) | 350.0 | 35.0 | Hot |
| S13→S14 (Product) | 98.5 | 40.0 | Hot |
| S26→S27 | 145.4 | 110.0 | Hot |
| DIST Condenser | 45.7 | 33.7 | Hot |
| S2→S3 (Feed) | 38.8 | 250.0 | Cold |
| S4→S5 | 249.5 | 350.0 | Cold |
| DIST Reboiler | 99.1 | 99.5 | Cold |

---

## 📈 Sensitivity Analysis

Four sensitivity studies were conducted in Aspen Plus varying one parameter at a time.

### S1 — H₂ Feed Flow Rate vs. Reactor Performance

<img width="1152" height="571" alt="image" src="https://github.com/user-attachments/assets/86c80877-8aa3-4497-b280-8790d805f7e0" />

**Varied:** H₂ molar flow, 2.0–8.0 kmol/hr

| H₂ (kmol/hr) | H₂S Mole Fraction | Product (kmol/hr) |
|---|---|---|
| 2.0 | 0.031 | 1.00 |
| **4.43 (design)** | **0.060** | **2.43** |
| 5.4 | 0.075 | 4.57 |
| 8.0 | 0.085 | 7.42 |

> **Optimal: 4.43–5 kmol/hr** — H₂ limiting below this; diminishing returns above 6 kmol/hr.

---

### S2 — Flash Drum Pressure vs. H₂ Recovery

<img width="1155" height="492" alt="image" src="https://github.com/user-attachments/assets/aaefc9f9-2406-4776-b6d0-eaf90c6209c4" />

**Varied:** Flash pressure, 3–20 bar

| P (bar) | H₂S MF in Vapor | H₂ Recovery MF |
|---|---|---|
| 3.0 | 0.149 | 0.091 |
| 6.9 | 0.156 (max) | 0.111 |
| **12.5 (crossover)** | **0.116** | **0.140** |
| 18.0 | 0.072 | 0.158 |

> **Optimal: 12–13 bar** — crossover point where H₂S condenses into liquid while H₂ recovery is maximized.

---

### S3 — Lean Amine Flow vs. H₂S Removal

<img width="1160" height="512" alt="image" src="https://github.com/user-attachments/assets/c9d6f270-84ce-4fe2-aa0f-88eea557e38b" />

**Varied:** Lean amine molar flow, 30–100 kmol/hr

| Amine (kmol/hr) | H₂S in Purge (MF) | H₂ Purity in Recycle |
|---|---|---|
| 30.0 | 0.331 | 0.005 |
| 45.0 | 0.093 | 0.015 |
| **50.0 (design)** | **0.000** | **0.020** |
| 100.0 | 0.000 | 0.320 |

> **Optimal: 50 kmol/hr** — minimum flow for complete H₂S removal; minimum effective point.

---

### S4 — Purge Fraction vs. H₂ Loss & Compressor Duty

<img width="1153" height="520" alt="image" src="https://github.com/user-attachments/assets/04c238c9-c979-40a2-976b-446f0d6a66ee" />

**Varied:** Purge fraction, 0.05–0.50

| Purge | H₂ Loss (kmol/hr) | H₂ Recycle (kmol/hr) | Comp. Duty (kW) |
|---|---|---|---|
| 0.05 | 2.0 | 25.0 | 0.125 |
| **0.15 (optimal)** | **7.0** | **8.0** | **0.086** |
| 0.30 | 14.5 | 3.5 | 0.080 |
| 0.50 | 25.0 | 2.0 | 0.077 |

> **Optimal: 0.15** — crossover point where H₂ loss equals H₂ recycle; balances H₂ conservation against compressor cost.

---

## 💰 Techno-Economic Analysis (APEA)

### Summary

| Parameter | Value |
|---|---|
| Total Capital Cost | $7,559,710 |
| Total Installed Cost (TIC) | $5,419,800 |
| Equipment Cost | $3,280,300 |
| Lang Factor | 1.65 |
| Total Operating Cost | $36,944,900/yr |
| Raw Materials Cost | $32,006,800/yr (86.6% of OpEx) |
| Total Utilities Cost | $166,091/yr **(0.45% of OpEx)** |
| Product Sales | $56,768,900/yr |
| **Annual Profit** | **$19,824,000/yr** |
| Desired ROR | 20% |
| **Payback Period** | **2.73 years** |

> Industry threshold: 5–7 years. This project at **2.73 years is well within range.**

### Operating Cost Breakdown

| Component | Annual Cost | % of OpEx |
|---|---|---|
| Raw Materials (Naphtha, H₂) | $32,006,800 | 86.6% |
| Other Operating Costs | $4,772,009 | 12.9% |
| Utilities | $166,091 | **0.45%** |
| **Total** | **$36,944,900** | 100% |

### Top Equipment by Installed Cost

| Equipment | Equipment Cost | Installed Cost |
|---|---|---|
| COMP2 | $12,25,500 | $13,68,600 |
| COMP1 | $9,90,200 | $11,36,600 |
| REAC | $4,91,500 | $9,62,900 |
| DIST-tower | $1,78,500 | $4,19,300 |
| ABSORBER | $1,43,900 | $3,33,000 |

> COMP1 + REAC account for **~45% of total equipment cost** — primary targets for capital reduction.

### Utilities Breakdown

| Utility | Rate | Cost/hr |
|---|---|---|
| Electricity | 98.323 kW | $7.620 |
| Cooling Water | 0.023058 MMGAL/H | $2.767 |
| Steam @100 PSI | 1.05162 KLB/H | $8.560 |

---

## 📁 Repository Structure

```
📦 Naphtha-HDS-Simulation/
│
├── 📄 README.md
│
├── 📂 Simulation/
│   ├── PetroProjectSimulationFile.apwz      ← Aspen Plus V12 simulation file
│   └── PetroprojectEnergyAnalysis.hch       ← Aspen Energy Analyzer file
│
├── 📂 Economic_Analysis/
│   └── HDS_Economic_Analysis.xlsx           ← APEA exported economic data
│
└── 📂 Report/
    └── Final_petro_report.pdf               ← Full project report
```

---

## 🚀 How to Open & Run

### Aspen Plus Simulation (`.apwz`)
1. Install **Aspen Plus V12** (AspenTech suite)
2. Open `PetroProjectSimulationFile.apwz`
3. Run simulation: `Home → Run` or press `F5`
4. Navigate sheets: Flowsheet → Stream Results → Sensitivity Analysis

### Aspen Energy Analyzer (`.hch`)
1. Open **Aspen Energy Analyzer V12**
2. File → Open → `PetroprojectEnergyAnalysis.hch`
3. Navigate: Savings Summary → Utilities → Carbon Emissions → Composite Curves

### Economic Analysis (`.xlsx`)
1. Open `HDS_Economic_Analysis.xlsx` in Excel or Google Sheets
2. Review tabs: Summary / Utilities / Unit Operation / Equipment

> **Note:** Aspen Plus V12 requires a valid AspenTech license. Trial licenses are available at [aspentech.com](https://www.aspentech.com).

---

## 📊 Key Results Summary

| Category | Result |
|---|---|
| Sulfur Removal | 100% (259.5 → 0 kg/hr) |
| Product Naphtha | 2,526 kg/hr, S14, 40°C |
| H₂S Produced | 81.19 kg/hr → Claus plant |
| Energy Savings | 73.44% total utility reduction |
| CO₂ Reduction | 186.7 kg/hr |
| Capital Cost | $7.56M |
| Annual Profit | $19.82M/yr |
| Payback Period | 2.73 years |

---

## ⚠️ Simulation Assumptions & Limitations

| Assumption | Industrial Reality |
|---|---|
| RStoic reactor (no kinetics) | Real design needs Langmuir-Hinshelwood kinetics in PFR |
| Isothermal reactor | Actual adiabatic ΔT = 15–40°C; affects HEN sizing |
| Pure amine model | Real MEA/MDEA needs Electrolyte-NRTL model |
| No catalyst deactivation | End-of-run conversion 3–8% lower |
| No pressure drops | Real ΔP increases compressor duty 15–30% |
| APEA 2018 cost basis | Real costs may differ ±30% |
| No amine regeneration | Stripper reboiler energy not included in OPEX |

---

## 👥 Team

| Name | Roll Number |
|---|---|
| Soham Raut | 230008031 |
| Sohel | 230008032 |
| Srajan Kewat | 230008033 |
| Ashish Donth | 230008011 |
| Saumya Vaidya | 230008035 |

**Project Advisor:** Dr. Rajan Singh, Department of Chemical Engineering

**Course:** Petroleum Refining & Process Design | B.Tech Chemical Engineering | April 2026

---

## 📚 References

1. Sadighi et al. (2009). *Revamp of naphtha hydrotreating process in an Iranian refinery.* Petroleum and Coal, 51(1). [ResearchGate](https://www.researchgate.net/publication/26625024)

2. Ahmadpour et al. (2019). *Hydrodesulfurization unit for natural gas condensate: Simulation based on Aspen Plus.* Journal of Thermal Analysis and Calorimetry, 135(3). [DOI](https://doi.org/10.1007/s10973-018-7512-4)

3. Zhao et al. (2017). *Pinch analysis in optimising energy consumption on a naphtha hydrotreating unit.* Petroleum & Petrochemical Engineering Journal, 1(4). [DOI](https://doi.org/10.23880/ppej-16000126)

4. Aspen Technology (2021). *Aspen Process Economic Analyzer (APEA).* AspenTech, Bedford, MA. [AspenTech](https://www.aspentech.com/en/products/engineering/aspen-process-economic-analyzer)

---

## 📄 License

This project is submitted as an academic B.Tech final year project. Simulation files and report are shared for educational reference only.

---

*Department of Chemical Engineering | B.Tech Process Design Project | April 2026*
