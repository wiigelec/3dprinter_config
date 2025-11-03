# Tier 4 — Ultra High Flow (Dragon UHF / Rapido UHF)

**Purpose:**  
Tier 4 is where hotend flow becomes the primary limiter rather than machine kinematics.  
It focuses on **Dragon UHF** and **Rapido UHF** hotends operating between **35–60 mm³/s**, emphasizing large-format printing, strong layer adhesion, and efficient throughput for engineering-grade materials.  
At this tier, the machine’s cooling and thermal stability are as critical as the extrusion system itself.

---

## Overview

| Parameter | Description |
|------------|--------------|
| **Tier Level** | 4 — Ultra High Flow |
| **Hotend** | Dragon UHF / Rapido UHF |
| **Volumetric Flow Limit** | 35–60 mm³/s |
| **Nozzle Sizes** | 0.4 mm, 0.6 mm, 0.8 mm |
| **Materials** | PLA, PETG, ASA, PC, Nylon, CF blends |
| **Goal** | Achieve maximum sustainable flow rate with stable mechanical behavior |

---

## Print Speed and Acceleration Table

| Feature | 0.4 mm Line Width | 0.6 mm Line Width | 0.8 mm Line Width | Accel (mm/s²) |
|----------|------------------|------------------|------------------|----------------|
| **External Walls** | 120 mm/s | 100 mm/s | 80 mm/s | 8000 |
| **Inner Walls** | 160 mm/s | 130 mm/s | 100 mm/s | 10000 |
| **Top/Bottom** | 120 mm/s | 100 mm/s | 80 mm/s | 8000 |
| **Infill** | 250 mm/s | 200 mm/s | 150 mm/s | 16000 |
| **Bridges** | 45 mm/s | 45 mm/s | 45 mm/s | 2500 |
| **Travel** | 250 mm/s | 250 mm/s | 250 mm/s | 20000 |
| **First Layer** | 35 mm/s | 30 mm/s | 25 mm/s | 1500 |
| **Support Interface** | 120 mm/s | 100 mm/s | 80 mm/s | 8000 |
| **Small Perimeters** | 60 mm/s | 45 mm/s | 35 mm/s | 4000 |

**Square Corner Velocity:** 12–14 mm/s  
**Max Accel to Decel:** 50% of max accel

---

## Line Width and Layer Height Recommendations

| Nozzle | Line Width Range | Layer Height Range | Typical Use |
|---------|------------------|--------------------|--------------|
| 0.4 mm | 0.45–0.55 mm | 0.22–0.28 mm | Fine high-speed printing |
| 0.6 mm | 0.60–0.72 mm | 0.26–0.36 mm | Balanced throughput and surface |
| 0.8 mm | 0.80–0.96 mm | 0.32–0.48 mm | Large-format and mechanical parts |

---

## Thermal and Cooling Envelope (PLA example)

| Setting | Value |
|----------|--------|
| **Hotend Temp** | 220–235 °C |
| **Bed Temp** | 60–70 °C |
| **Fan** | 100 % (ensure dual ducts) |
| **Chamber** | Recommended for ABS/ASA/PC |
| **Ambient Target** | 25–40 °C |

---

## Calibration Sequence

1. **Flow Stress Test**  
   - Increase speed layer-by-layer until under-extrusion appears.  
   - Record flow limit and reduce by 10–20% for reliability.

2. **Thermal Stability Check**  
   - Monitor heater output during sustained 10-minute infill print.  
   - Target: temperature deviation < ±2 °C.

3. **Pressure Advance Recalibration**  
   - Perform PA test at 150 mm/s walls.  
   - Tune to eliminate corner gaps and bulges under high back-pressure.

4. **Cooling Validation**  
   - Print steep overhangs (45°–60°).  
   - Verify fan performance keeps PLA from gloss banding or PETG from sagging.

5. **Ringing and Resonance Test**  
   - 100×20×150 mm tower with 45° infill at 16k accel; inspect for echoing.

---

## Promotion Criteria to Tier 5

| Requirement | Target |
|--------------|--------|
| **Extrusion stability** | Maintained at ≥50 mm³/s |
| **Ringing control** | None up to 10,000 mm/s² |
| **Thermal stability** | ±2 °C steady-state |
| **Flow uniformity** | Consistent extrusion thickness |
| **Surface finish** | Functional, minor aesthetic variation acceptable |

---

## Example Klipper Parameters

```
[printer]
max_velocity: 600
max_accel: 20000
max_accel_to_decel: 10000
square_corner_velocity: 13
```

---

## Example OrcaSlicer Profile Parameters

| Setting | Value |
|----------|--------|
| **Volumetric speed limit** | 45 mm³/s |
| **Perimeter speed** | 120 mm/s |
| **Infill speed** | 250 mm/s |
| **Travel speed** | 250 mm/s |
| **Acceleration control** | Enabled (8000–20000 mm/s²) |
| **Min layer time** | 5 s (PLA), 3 s (PETG/ASA) |

---

## Tips

- Avoid overcooling: thicker lines are better than higher speeds.  
- Ensure PSU and heater cartridge can sustain thermal load at continuous 40–60 mm³/s.  
- Test CF and PC blends at lower speeds until viscosity behavior is known.  
- Use 0.6–0.8 mm nozzles for maximum tier efficiency.  
- Ensure part cooling ducts evenly cover both sides of the nozzle.

---

## Author

Tier 4 Framework © **wiigelec** — part of the *Tiered 3D Printer Performance Framework* project.
