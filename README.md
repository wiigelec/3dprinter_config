# Tiered 3D Printer Performance Framework

This repository defines a **five-tier performance model** for tuning and benchmarking 3D printers.  
Each tier represents an incremental step in speed, acceleration, and volumetric throughput — from initial calibration to machine-limited operation.  
The tiers are designed to map directly to common hotend configurations such as **Dragon SF, HF, UHF**, and **Rapido HF, UHF**.

---

## Overview

| Tier | Purpose | Hotend Class | Flow Limit (mm³/s) | Example Use |
|------|----------|--------------|--------------------|--------------|
| **1** | Baseline calibration | Any | ≤6 | First-layer, PA, IS, thermal checks |
| **2** | Standard flow tuning | Dragon SF | 10–15 | Reliable everyday printing |
| **3** | High flow optimization | Dragon HF / Rapido HF | 20–30 | Fast PLA / PETG / ABS throughput |
| **4** | Ultra high flow | Dragon UHF / Rapido UHF | 35–60 | Large nozzle or large part printing |
| **5** | Machine-limited | Any | >60 (kinematics bound) | Resonance & firmware limit testing |

Each higher tier builds upon the calibration and verified performance of the tier before it.  
Moving upward requires verified results: no extrusion instability, no ringing, and thermally consistent layers.

---

## Tier 1 — Baseline Calibration (Dragon SF Example)

**Purpose:**  
Establish a mechanical and thermal reference point. Used for input shaper, pressure advance, and flow tuning.

**Typical Settings (0.4 mm nozzle, PLA):**
- Line width: 0.45 mm  
- Layer height: 0.20 mm  
- Volumetric flow limit: 6 mm³/s  
- Max speed: 60 mm/s (walls), 100 mm/s (travel)  
- Acceleration: 1500–3000 mm/s²  
- Square corner velocity: 5–8 mm/s  
- Temperature: 205–215 °C  
- Fan: 80–100 %

**Calibration Sequence:**
1. E-steps and filament diameter verification  
2. Flow calibration (single-wall cube)  
3. First-layer Z offset  
4. Temperature tower  
5. Pressure Advance (PA) tower  
6. Input Shaper (IS) calibration  
7. Validation cube (dimensional + surface test)

**Promotion Criteria to Tier 2:**
- Extrusion width within ±0.02 mm  
- No visible ringing at 2500 mm/s²  
- Stable flow up to 60 mm/s  
- Consistent layer adhesion across temp tower

---

## Tier Progression Philosophy

Each tier has a specific goal:

- **Tier 1:** Baseline calibration and thermal tuning  
- **Tier 2:** Standard-flow operational optimization  
- **Tier 3:** High-flow expansion for faster throughput  
- **Tier 4:** Ultra-high-flow and heavy extrusion validation  
- **Tier 5:** Machine-limited maximum kinematic stress test  

A printer should only advance tiers when the prior tier’s stability metrics are met for at least two materials (PLA + one engineering filament).

---

## Material Guidelines

| Material | Typical Flow Range (mm³/s) | Notes |
|-----------|-----------------------------|-------|
| **PLA** | 8–50 | Cooling-limited; best for Tier 4–5 tests |
| **PETG** | 6–25 | Sensitive to stringing; slower walls recommended |
| **ASA/ABS** | 8–35 | Requires enclosure and moderate fan use |
| **PC** | 10–40 | Thermal throughput limited; use enclosure |
| **Nylon (PA)** | 10–30 | Must be dry; moisture affects flow consistency |
| **TPU** | 4–12 | Limited by filament compression; Tier 2 max |

---

## Recommended Nozzle Configurations

| Nozzle | Line Width | Layer Height | Best Tiers | Comment |
|---------|-------------|---------------|-------------|----------|
| 0.4 mm | 0.42–0.48 mm | 0.16–0.28 mm | 1–3 | General-purpose balance |
| 0.6 mm | 0.6–0.72 mm | 0.24–0.36 mm | 3–5 | Ideal for HF/UHF throughput |

---

## Key Equations

**Volumetric Speed Limit:**
```
v_max = VFR / (line_width × layer_height)
```
Use 80% of calculated v_max for continuous print moves.

**Example (PLA, 0.45 mm line, 0.20 mm layer):**
```
6 mm³/s ÷ (0.45 × 0.20) = 67 mm/s  →  run walls ≈ 40 mm/s
```

---


## License

Open source, under your preferred license (MIT recommended).

---

## Notes

- All parameters assume **Klipper firmware** and **OrcaSlicer / PrusaSlicer** compatible profiles.  
- Acceleration and SCV values scale with motion system rigidity and resonance behavior.  
- Always tune **Pressure Advance** and **Input Shaper** at Tier 1 before applying to higher tiers.

---

## Author

Project maintained by **wiigelec** — engineering the intersection of *open-source hardware* and *performance-class 3D printing*.
