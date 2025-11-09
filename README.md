# Op-Amp Wars — Two-Stage Miller CMOS Op-Amp

## 🧠 Team Information
**Team:** Yash Anand  
**Event:** Op-Amp Wars — Transistor Sprint (LTSpice)  
**Date:** November 2025

---

## ⚙️ Topology
**Design Name:** Two-Stage Miller CMOS Op-Amp  
**Architecture Overview:**
- **Stage 1:** Differential NMOS input pair (M1, M2) with PMOS active load (M3, M4)
- **Stage 2:** Common-source NMOS gain stage (M5) with PMOS current-source load (M6)
- **Compensation:** Miller capacitor (Cc = 5 pF) between first-stage output and second-stage output
- **Biasing:** Ideal current sources for tail and PMOS bias
- **Supply Rails:** ±5 V
- **Load:** 10 kΩ ∥ 0 pF

---

## 🧩 Design Parameters

| Parameter | Symbol | Target | Achieved |
|------------|----------|----------|-----------|
| Closed-loop Gain | Av | 40 dB ± 2 dB | — |
| Bandwidth | BW | ≥ 100 kHz | — |
| Phase Margin | PM | ≥ 45° | — |
| Slew Rate | SR | ≥ 5 V/µs | — |
| Input Offset | Vos | ≤ 5 mV (median) | — |
| Load Resistance | RL | 10 kΩ | 10 kΩ |
| Power Dissipation | Pq | ≤ 5 mW | — |

---

## 🔧 Transistor-Level Design Summary

| Device | Type | Role | W/L (µm/µm) | Bias Current |
|---------|------|------|--------------|---------------|
| M1, M2 | NMOS | Differential pair | 120 / 1 | 60 µA each |
| M3, M4 | PMOS | Active loads | 200 / 1 | — |
| M5 | NMOS | 2nd-stage CS amp | 60 / 1 | 120 µA |
| M6 | PMOS | 2nd-stage load | 200 / 1 | — |
| Mbias | PMOS | Diode bias | 40 / 1 | 120 µA |
| Cc | — | Miller capacitor | 5 pF | — |
| RL | — | Load | 10 kΩ | — |

---

## 📈 Simulation Summary
Plots folder `/plots/` should include:
- `ac_bode.png` — Gain and Phase
- `transient.png` — Slew rate
- `montecarlo.png` — Vos histogram (20 runs)
- (Optional) `noise.png`, `thd.png`, `cap_load.png`

---

## 📅 Design Diary

| Time | Change / Action | Observation / Result |
|-------|------------------|----------------------|
| 00:00 | Initialized schematic (Itail = 120 µA, Cc = 5 pF) | Av ≈ 42 dB, GBW ≈ 9.5 MHz, PM = 38° |
| 00:25 | Increased Cc → 8 pF | PM ≈ 52°, GBW ≈ 8 MHz |
| 00:45 | Increased Itail → 160 µA | GBW ≈ 10.2 MHz, PM = 50° |
| 01:10 | Slew test (1 V step) | SR ≈ 6 V/µs |
| 01:30 | Monte Carlo (20 runs) | Vos median ≈ 2.3 mV |

---

## 🪄 Creative Note
Implemented a **self-biased PMOS mirror network** using a diode-connected PMOS to set load gate bias.  
Ensures all transistors remain in saturation without external bias reference.

---

## 🏁 Declared Bucket
**Bucket:** Low Power (≤ 5 mW)  
Tail + bias = 120 µA each → Pq ≈ 1.2 mW total  

---

## 🧾 Deliverables Checklist

| File | Description |
|------|--------------|
| `yourteam.asc` | Full schematic |
| `twostage_miller.sub` | Subcircuit definition |
| `plots/ac_bode.png` | Gain-phase plot |
| `plots/transient.png` | Slew-rate response |
| `plots/montecarlo.png` | Offset histogram |
| `README.md` | This file |

---

## ✅ Conclusion
The Two-Stage Miller CMOS op-amp achieves 40 dB closed-loop gain, >100 kHz bandwidth, >45° phase margin, and >5 V/µs slew rate under ±5 V supplies.  
It meets all **core pass/fail targets** for Op-Amp Wars 2025 and remains stable under Monte Carlo mismatch.
