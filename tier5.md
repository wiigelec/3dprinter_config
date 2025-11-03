# Tier 5 — Machine-Limited Performance

**Purpose:**  
Tier 5 represents the **absolute mechanical and kinematic limit** of the printer.  
At this stage, the hotend is no longer the bottleneck — motion control, resonance, and firmware timing define performance boundaries.  
Tier 5 is ideal for advanced tuning, benchmarking, and validation of printer rigidity, firmware optimization, and part geometry integrity under extreme acceleration.

---

## Overview

| Parameter | Description |
|------------|--------------|
| **Tier Level** | 5 — Machine-Limited |
| **Hotend** | Any capable of ≥60 mm³/s |
| **Volumetric Flow Limit** | Machine/thermal limited |
| **Nozzle Sizes** | 0.4 mm – 0.8 mm |
| **Materials** | PLA, PETG, ASA, PC, Nylon, CF blends |
| **Goal** | Push kinematics, resonance, and firmware throughput to maximum sustainable limits |

---

## Print Speed and Acceleration Table

| Feature | 0.4 mm Line Width | 0.6 mm Line Width | 0.8 mm Line Width | Accel (mm/s²) |
|----------|------------------|------------------|------------------|----------------|
| **External Walls** | 160 mm/s | 130 mm/s | 100 mm/s | 15000 |
| **Inner Walls** | 220 mm/s | 180 mm/s | 140 mm/s | 20000 |
| **Top/Bottom** | 160 mm/s | 130 mm/s | 100 mm/s | 15000 |
| **Infill** | 400 mm/s | 350 mm/s | 250 mm/s | 30000 |
| **Bridges** | 50 mm/s | 50 mm/s | 50 mm/s | 3000 |
| **Travel** | 700 mm/s | 700 mm/s | 700 mm/s | 40000 |
| **First Layer** | 40 mm/s | 35 mm/s | 30 mm/s | 1500 |
| **Support Interface** | 150 mm/s | 120 mm/s | 100 mm/s | 10000 |
| **Small Perimeters** | 70 mm/s | 50 mm/s | 40 mm/s | 6000 |

**Square Corner Velocity:** 14–16 mm/s  
**Max Accel to Decel:** 50% of max accel

---

## Line Width and Layer Height Recommendations

| Nozzle | Line Width Range | Layer Height Range | Typical Use |
|---------|------------------|--------------------|--------------|
| 0.4 mm | 0.45–0.55 mm | 0.20–0.30 mm | Benchmarking precision |
| 0.6 mm | 0.60–0.72 mm | 0.26–0.36 mm | Balanced high-speed throughput |
| 0.8 mm | 0.80–1.00 mm | 0.32–0.48 mm | Structural and mechanical stress tests |

---

## Thermal and Cooling Envelope (PLA example)

| Setting | Value |
|----------|--------|
| **Hotend Temp** | 225–240 °C |
| **Bed Temp** | 60–70 °C |
| **Fan** | 100 % minimum, preferably dual-duct |
| **Chamber** | Enclosed for engineering filaments |
| **Ambient Target** | 30–45 °C |

---

## Calibration Sequence

1. **Full Kinematic Stress Test**  
   - 700 mm/s travel and 40k accel using input shaper active.  
   - Print long straight infill lines; observe skipped steps or stepper overheat.

2. **Resonance Mapping**  
   - Run multi-axis `SHAPER_CALIBRATE` and analyze frequency spectrum.  
   - Adjust `square_corner_velocity` and `max_accel` for best tradeoff between stability and speed.

3. **Thermal Throughput Validation**  
   - Confirm heater cartridge maintains stable temp at 100% duty cycle with flow above 50 mm³/s.  
   - Replace heater if droop >5 °C during continuous printing.

4. **Mechanical Integrity Check**  
   - Print tall narrow towers at 25–35 mm/s walls and 20k accel.  
   - Inspect for skew, step loss, or layer shift artifacts.

5. **Surface & Accuracy Verification**  
   - 200×200×10 mm slab at full speed; verify linearity and parallelism of infill pattern.  
   - Measure dimensional variance; acceptable tolerance ±0.5%.

---

## Tier 5 Readiness Checklist

| Requirement | Target |
|--------------|--------|
| **No skipped steps at 40k accel** | Pass |
| **Heater output stable within ±3 °C** | Pass |
| **Frame resonance managed via IS** | Pass |
| **Extrusion uniform at 400 mm/s walls** | Pass |
| **Surface stability under motion stress** | Minor artifacts acceptable |

---

## Example Klipper Parameters

```
[printer]
max_velocity: 700
max_accel: 40000
max_accel_to_decel: 20000
square_corner_velocity: 15
```

---

## Example OrcaSlicer Profile Parameters

| Setting | Value |
|----------|--------|
| **Volumetric speed limit** | 60+ mm³/s |
| **Perimeter speed** | 160 mm/s |
| **Infill speed** | 400 mm/s |
| **Travel speed** | 700 mm/s |
| **Acceleration control** | Enabled (15000–40000 mm/s²) |
| **Min layer time** | 3–5 s depending on material |

---

## Tips

- Tune input shaper aggressively and retest after every mechanical change.  
- Avoid small, intricate parts; this tier favors large continuous motions.  
- Use filament with consistent diameter and melt flow index.  
- Cooling is the primary limiter for PLA; reduce acceleration before airflow fails.  
- Always run long-duration thermal soak tests before production.

---

## Author

Tier 5 Framework © **wiigelec** — part of the *Tiered 3D Printer Performance Framework* project.
