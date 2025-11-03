# Tier 3 — High Flow Optimization (Dragon HF / Rapido HF)

**Purpose:**  
Tier 3 represents the transition from standard flow to high flow operation.  
It leverages the capabilities of **Dragon HF** and **Rapido HF** hotends, allowing volumetric flow rates up to **20–30 mm³/s**.  
This tier targets *high-performance printing* with a focus on maximizing throughput while maintaining predictable print quality.

---

## Overview

| Parameter | Description |
|------------|--------------|
| **Tier Level** | 3 — High Flow |
| **Hotend** | Dragon HF / Rapido HF |
| **Volumetric Flow Limit** | 20–30 mm³/s |
| **Nozzle Sizes** | 0.4 mm, 0.6 mm |
| **Materials** | PLA, PETG, ASA, PC, Nylon |
| **Goal** | Achieve fast, reliable prints with tuned extrusion flow and mechanical resonance control |

---

## Print Speed and Acceleration Table

| Feature | 0.4 mm Line Width | 0.6 mm Line Width | 0.4 mm Accel (mm/s²) | 0.6 mm Accel (mm/s²) |
|----------|------------------|------------------|----------------------|----------------------|
| **External Walls** | 90 mm/s | 70 mm/s | 6000 | 6000 |
| **Inner Walls** | 120 mm/s | 90 mm/s | 8000 | 8000 |
| **Top/Bottom** | 90 mm/s | 70 mm/s | 7000 | 7000 |
| **Infill** | 180 mm/s | 140 mm/s | 12000 | 12000 |
| **Bridges** | 40 mm/s | 40 mm/s | 2500 | 2500 |
| **Travel** | 200 mm/s | 200 mm/s | 15000 | 15000 |
| **First Layer** | 30 mm/s | 25 mm/s | 1500 | 1500 |
| **Support Interface** | 90 mm/s | 70 mm/s | 6000 | 6000 |
| **Small Perimeters** | 50 mm/s | 35 mm/s | 4000 | 4000 |

**Square Corner Velocity:** 10–12 mm/s  
**Max Accel to Decel:** 50% of max accel

---

## Line Width and Layer Height Recommendations

| Nozzle | Line Width Range | Layer Height Range | Typical Use |
|---------|------------------|--------------------|--------------|
| 0.4 mm | 0.44–0.52 mm | 0.20–0.28 mm | High-quality fast printing |
| 0.6 mm | 0.60–0.72 mm | 0.24–0.36 mm | Strong functional parts, efficient throughput |

---

## Thermal and Cooling Envelope (PLA example)

| Setting | Value |
|----------|--------|
| **Hotend Temp** | 215–230 °C |
| **Bed Temp** | 60–65 °C |
| **Fan** | 100 % |
| **Chamber** | Optional (for PC/ASA/PA) |
| **Ambient Target** | 20–35 °C |

---

## Calibration Sequence

1. **Maximum Flow Validation**  
   - Print a flow tower increasing speed until under-extrusion appears.  
   - Record maximum volumetric rate and reduce by 20% for reliable operation.

2. **Pressure Advance Fine Tune**  
   - Retest PA at higher acceleration; high-flow nozzles can exhibit small lag differences.

3. **Input Shaper Validation**  
   - Re-run SHAPER_CALIBRATE with your heaviest toolhead configuration.  
   - Test accel up to 15,000 mm/s² and note any residual ringing.

4. **Thermal Throughput Check**  
   - Long print at 0.3 mm layers, 0.6 mm line width, 120 mm/s walls.  
   - Watch for temperature droop >3 °C; adjust PID tuning if necessary.

5. **Surface Consistency Test**  
   - Large flat plate (≥150×150 mm) to verify consistent infill overlap and wall blending.

---

## Promotion Criteria to Tier 4

| Requirement | Target |
|--------------|--------|
| **Extrusion stability** | Maintained at ≥25 mm³/s |
| **Ringing** | Negligible up to 8000 mm/s² |
| **Flow integrity** | No under-extrusion at target temps |
| **Hotend temperature stability** | ±2 °C during continuous flow |
| **Surface quality** | Minor cosmetic artifacts acceptable |

---

## Example Klipper Parameters

```
[printer]
max_velocity: 400
max_accel: 15000
max_accel_to_decel: 7500
square_corner_velocity: 11
```

---

## Example OrcaSlicer Profile Parameters

| Setting | Value |
|----------|--------|
| **Volumetric speed limit** | 25 mm³/s |
| **Perimeter speed** | 90 mm/s |
| **Infill speed** | 180 mm/s |
| **Travel speed** | 200 mm/s |
| **Acceleration control** | Enabled (6000–15000 mm/s²) |
| **Min layer time** | 6 s (PLA), 4 s (PETG/ASA) |

---

## Tips

- Increase nozzle temperature slightly (5–10 °C) at higher speeds to maintain viscosity balance.  
- Large parts benefit from thicker lines over higher head speeds for thermal efficiency.  
- Use 0.6 mm nozzle and 0.3 mm layer for best balance of surface quality and speed.  
- Confirm hotend’s heater cartridge wattage supports sustained 25+ mm³/s flow (40 W recommended).

---

## Author

Tier 3 Framework © **wiigelec** — part of the *Tiered 3D Printer Performance Framework* project.
