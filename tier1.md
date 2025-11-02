# Tier 1 — Baseline Calibration (Dragon SF)

**Purpose:**  
Establish a mechanical and thermal reference point for your 3D printer.  
Tier 1 represents the minimal operational settings used for calibration, bring-up, and baseline verification.  
It focuses on *accuracy, stability, and repeatability*, not speed.

---

## Overview

| Parameter | Description |
|------------|--------------|
| **Tier Level** | 1 — Baseline |
| **Hotend** | Dragon SF (Standard Flow) |
| **Volumetric Flow Limit** | ≤6 mm³/s |
| **Nozzle Sizes** | 0.4 mm, 0.6 mm |
| **Materials** | PLA, PETG, ASA, TPU |
| **Goal** | Establish flow, PA, IS, thermal and mechanical consistency |

---

## Baseline Print Parameters

### 0.4 mm nozzle
- Line width: **0.45 mm**
- Layer height: **0.20 mm**
- Max flow: **6 mm³/s**
- Max wall speed: **40–60 mm/s**
- Max infill speed: **60 mm/s**
- Travel speed: **100 mm/s**
- Acceleration: **1500–3000 mm/s²**
- Square corner velocity: **5–8 mm/s**

### 0.6 mm nozzle
- Line width: **0.60 mm**
- Layer height: **0.25 mm**
- Max flow: **6 mm³/s**
- Max wall speed: **25–40 mm/s**
- Max infill speed: **40 mm/s**
- Travel speed: **100 mm/s**
- Acceleration: **1500–3000 mm/s²**
- Square corner velocity: **5–8 mm/s**

---

## Thermal and Cooling Envelope (PLA example)

| Setting | Value |
|----------|--------|
| **Hotend Temp** | 205–215 °C |
| **Bed Temp** | 60 °C |
| **Fan** | 80–100 % |
| **Chamber** | Open air |
| **Ambient Target** | 20–25 °C |

---

## Calibration Sequence

1. **E-Steps and Flow Check**  
   - Mark 100 mm filament, extrude, and measure actual length.  
   - Adjust steps/mm if deviation >1%.

2. **Filament Diameter Measurement**  
   - Average three readings at three rotations; input into slicer.

3. **Single-Wall Flow Cube**  
   - 0.45 mm target; measure wall thickness and adjust flow % to match.

4. **First-Layer Calibration**  
   - 75×75 mm bed patch; tune Z offset for continuous sheen.

5. **Temperature Tower**  
   - 5 °C steps (e.g., 195→220 °C); choose lowest stable fusion temperature.

6. **Pressure Advance (PA)**  
   - Print PA tower at 40 mm/s walls; select sharpest non-bulging corners.

7. **Input Shaper (IS)**  
   - Use accelerometer or ringing tower; run SHAPER_CALIBRATE or equivalent.

8. **Validation Cube**  
   - 20 mm cube; check dimensional accuracy and inspect walls for ringing.

---

## Promotion Criteria to Tier 2

| Requirement | Target |
|--------------|--------|
| **Extrusion width tolerance** | ±0.02 mm |
| **Visible ringing** | None at 2500 mm/s² |
| **Flow stability** | No thinning up to 60 mm/s |
| **Layer adhesion** | Consistent across tower temps |
| **Dimensional accuracy** | <0.1% deviation |

---

## Example Klipper Parameters

```
[printer]
max_velocity: 120
max_accel: 3000
max_accel_to_decel: 1500
square_corner_velocity: 6
```

---

## Example OrcaSlicer Profile Parameters

| Setting | Value |
|----------|--------|
| **Volumetric speed limit** | 6 mm³/s |
| **Perimeter speed** | 40 mm/s |
| **Infill speed** | 60 mm/s |
| **Travel speed** | 100 mm/s |
| **Acceleration control** | Enabled (1500–3000 mm/s²) |
| **Min layer time** | 8 s (PLA) |

---

## Tips

- Perform all Tier 1 calibration on open-air PLA before advancing to PETG or ASA.  
- Log each calibration result (temp, PA, IS) in a per-filament profile.  
- Maintain one verified Tier 1 config as your “factory baseline.”

---

## Author

Tier 1 Framework © **wiigelec** — part of the *Tiered 3D Printer Performance Framework* project.
