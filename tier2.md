# Tier 2 — Standard Flow Tuning (Dragon SF)

**Purpose:**  
Tier 2 represents the *operational baseline* for standard flow hotends.  
It extends from the Tier 1 calibration base and introduces higher speeds and accelerations within the thermal and volumetric limits of the **Dragon SF** hotend (10–15 mm³/s).  
The goal is consistent production-quality printing with balanced throughput and finish.

---

## Overview

| Parameter | Description |
|------------|--------------|
| **Tier Level** | 2 — Standard Flow |
| **Hotend** | Dragon SF |
| **Volumetric Flow Limit** | 10–15 mm³/s |
| **Nozzle Sizes** | 0.4 mm, 0.6 mm |
| **Materials** | PLA, PETG, ASA, TPU |
| **Goal** | Achieve production-ready speeds while maintaining surface integrity |

---

## Print Speed and Acceleration Table

| Feature | 0.4 mm Line Width | 0.6 mm Line Width | 0.4 mm Accel (mm/s²) | 0.6 mm Accel (mm/s²) |
|----------|------------------|------------------|----------------------|----------------------|
| **External Walls** | 60 mm/s | 45 mm/s | 3000 | 3000 |
| **Inner Walls** | 80 mm/s | 55 mm/s | 4000 | 4000 |
| **Top/Bottom** | 70 mm/s | 50 mm/s | 3500 | 3500 |
| **Infill** | 110 mm/s | 80 mm/s | 5000 | 5000 |
| **Bridges** | 30 mm/s | 30 mm/s | 2000 | 2000 |
| **Travel** | 150 mm/s | 150 mm/s | 6000 | 6000 |
| **First Layer** | 25 mm/s | 20 mm/s | 1200 | 1200 |
| **Support Interface** | 60 mm/s | 40 mm/s | 3500 | 3500 |
| **Small Perimeters** | 35 mm/s | 25 mm/s | 2000 | 2000 |

**Square Corner Velocity:** 8–10 mm/s  
**Max Accel to Decel:** 50% of max accel

---

## Line Width and Layer Height Recommendations

| Nozzle | Line Width Range | Layer Height Range | Typical Use |
|---------|------------------|--------------------|--------------|
| 0.4 mm | 0.42–0.48 mm | 0.18–0.26 mm | Standard detailed printing |
| 0.6 mm | 0.60–0.68 mm | 0.22–0.30 mm | Higher throughput and stronger parts |

---

## Thermal and Cooling Envelope (PLA example)

| Setting | Value |
|----------|--------|
| **Hotend Temp** | 210–220 °C |
| **Bed Temp** | 60 °C |
| **Fan** | 90–100 % |
| **Chamber** | Open air or lightly enclosed |
| **Ambient Target** | 20–25 °C |

---

## Calibration Sequence

1. **Flow Validation**  
   - Print a 0.45 mm single-wall cube at 60–100 mm/s.  
   - Increase speed until extrusion begins to underfill; record maximum usable speed.

2. **Pressure Advance Re-Check**  
   - Print PA tower at 60–80 mm/s; fine-tune corners for slight bulge correction.

3. **Input Shaper Verification**  
   - Reprint ringing tower or use accelerometer data to verify damping holds at higher accel.

4. **Temperature Confirmation**  
   - Run a shorter tower (200 °C to 225 °C) at higher speed; verify layer adhesion remains consistent.

5. **Dimensional Stability Cube**  
   - 40 mm cube at 100 mm/s infill; confirm wall alignment and surface uniformity.

---

## Promotion Criteria to Tier 3

| Requirement | Target |
|--------------|--------|
| **Extrusion consistency** | Uniform at up to 100 mm/s |
| **Visible ringing** | None at 4000 mm/s² |
| **Flow stability** | No thinning up to 12 mm³/s |
| **Layer adhesion** | Consistent across tower temps |
| **Surface finish** | Comparable to Tier 1 at 2× speed |

---

## Example Klipper Parameters

```
[printer]
max_velocity: 250
max_accel: 6000
max_accel_to_decel: 3000
square_corner_velocity: 9
```

---

## Example OrcaSlicer Profile Parameters

| Setting | Value |
|----------|--------|
| **Volumetric speed limit** | 12 mm³/s |
| **Perimeter speed** | 60 mm/s |
| **Infill speed** | 110 mm/s |
| **Travel speed** | 150 mm/s |
| **Acceleration control** | Enabled (3000–6000 mm/s²) |
| **Min layer time** | 8 s (PLA) |

---

## Tips

- Re-tune Pressure Advance for each filament brand and color; viscosity changes at this tier.  
- For PETG, reduce fan to 40–60 % and increase temperature by 10–15 °C.  
- Use 0.6 mm nozzle for functional prints where time efficiency outweighs finish detail.  
- Verify all resonance frequencies before moving to Tier 3 (HF).

---

## Author

Tier 2 Framework © **wiigelec** — part of the *Tiered 3D Printer Performance Framework* project.
