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

# Tier 2 — Validation Test Suite and Promotion Criteria

**Hotend:** Dragon SF  
**Flow Ceiling:** ≈ 12 mm³/s  
**Acceleration Target:** 3,000–6,000 mm/s²  

Tier 2 is where the printer transitions from calibration to production performance.  
These tests validate flow, stability, and resonance at standard-flow operating speeds.  
The goal: confirm the system is ready to handle consistent, fast, repeatable prints.

---

## 🧩 Tier 2 Validation Test Suite

Each test has a clear purpose, artifact, and passing condition.

### 1. Flow-Rate Step Test (Volumetric Validation)
**Purpose:** Confirm melt throughput for Tier 2 speeds.  
**Artifact:** Flow tower (each 10 mm Z segment increases flow by +2 mm³/s).  
**Settings:**
```
0.45 mm line × 0.20 mm layer
Start = 6 mm³/s → End = 14 mm³/s
Single perimeter, no infill
```
**Pass:** No under-extrusion before 12 mm³/s.  
**Fail:** Thinning or gaps before 12 mm³/s → adjust Tier 2 flow ceiling.

---

### 2. Pressure Advance Re-Tune (Corner Stability)
**Purpose:** Refine PA at higher acceleration.  
**Artifact:** PA tower with speed steps (40 → 80 mm/s).  
**Pass:** Sharp corners without bulge or gap.  
**Expected Range:** PA = 0.020–0.045 depending on drive type.

---

### 3. Input Shaper Verification (Ringing Damping)
**Purpose:** Confirm that 6k accel doesn’t excite resonance.  
**Artifact:** Ringing tower, 45° infill, 100 mm tall, 3 perimeters.  
**Settings:** 120 mm/s walls, 6,000 mm/s² accel.  
**Pass:** No visible echo in reflected light.  
**Fail:** Echo or ghosting → re-run `SHAPER_CALIBRATE`.

---

### 4. Temperature Consistency Tower
**Purpose:** Determine extrusion temp under sustained load.  
**Artifact:** 25 mm × 25 mm tower; each 5 mm Z = +5 °C (200–225 °C).  
**Settings:** 80 mm/s walls @ 12 mm³/s flow.  
**Pass:** Smooth adhesion at lowest stable temp.  
**Fail:** Dull finish or weak fusion → raise temp.

---

### 5. Retraction and Stringing Test
**Purpose:** Validate retraction under Tier 2 motion.  
**Artifact:** 4-pillar stringing test (40 mm tall).  
**Settings:** 40–100 mm/s travel; 1–1.2 mm retraction.  
**Pass:** Minimal wisps, no blobs.  
**Fail:** Heavy strings → increase retraction or travel accel.

---

### 6. Dimensional Accuracy Cube
**Purpose:** Confirm mechanical precision under moderate accel.  
**Artifact:** 40 mm cube, 3 walls, 20 % infill.  
**Settings:** 100 mm/s infill, 4 k accel.  
**Pass:** ±0.1 mm XY, ±0.15 mm Z.  
**Fail:** Layer offset or overshoot → lower accel or re-tune shaper.

---

### 7. Surface Consistency Panel
**Purpose:** Verify surface uniformity at working speed.  
**Artifact:** 120×120×3 mm panel, 3 perimeters, 100 % infill, 1 top layer.  
**Settings:** 70 mm/s walls, 5 k accel.  
**Pass:** Even sheen, no pressure banding.  
**Fail:** Variable gloss → re-check flow or temp stability.

---

### 8. Thermal Soak and Fan Efficiency
**Purpose:** Confirm temperature stability at continuous load.  
**Artifact:** Two identical 50 mm cubes printed consecutively.  
**Monitor:** Hotend ±2 °C, bed ±1 °C, fan RPM ≥90 %.  
**Pass:** Identical weight (±1 %).  
**Fail:** Significant weight variance → check cooling or PID tune.

---

## ✅ Promotion Criteria — Advancement to Tier 3

| Metric | Target | Pass Condition |
|--------|---------|----------------|
| **Flow rate limit** | ≥ 12 mm³/s | Flow tower stable |
| **Acceleration response** | ≤ 1 % size error at 6 k | Cube within tolerance |
| **Thermal drift** | < 2 °C extruder variance | PID stable |
| **Ringing** | None visible at 6 k | Tower clean |
| **Retraction performance** | Minimal stringing | Verified visually |

**Promotion Requirement:**  
All tests must pass on **two materials** (PLA + one engineering filament such as PETG or ASA).  
Log results and generate a validation report in `/docs/calibration_results/`.

---

## 🧠 Notes
- Record your PA, IS, and flow results for each filament.  
- If layer adhesion fails before ringing, the tier is thermally limited, not mechanically.  
- Always validate with at least two consecutive successful prints before promoting.

---

## 🧾 Example Promotion Log Format
```
Material: PLA
Hotend: Dragon SF
Nozzle: 0.4 mm
Max flow stable: 12.3 mm³/s
Accel: 6000 mm/s²
Extruder drift: 1.7 °C
Result: PASS — promote to Tier 3
```
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
