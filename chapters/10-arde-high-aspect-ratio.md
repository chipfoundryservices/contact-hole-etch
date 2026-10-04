# Chapter 10: Aspect Ratio Dependent Etching (ARDE) at High Aspect Ratio

## Overview

Contact-hole aspect ratios (50-200:1) create extreme radical depletion and shadowing effects. This chapter quantifies ARDE mechanisms, predicts 50-100× etch rate variation, and designs multi-step compensation strategies.

**Learning Objectives:**
- Model radical depletion as function of aspect ratio
- Quantify view factor and shadowing effects
- Predict etch uniformity from ARDE
- Design multi-step ARDE compensation recipes
- Optimize pressure and pulsed plasma for uniformity

---

## 10.1 Radical Depletion at High Aspect Ratio

### 10.1.1 Depletion Mechanism

```
Fundamental problem:

Contact via: 5 nm wide, 500 nm deep (100:1 AR)
Radical flux into via: φ_radical ≈ 10¹⁵ cm⁻²s⁻¹

As etch proceeds down the via:
  Top (entrance): Full radical flux φ₀
  Mid-depth (250 nm): Radicals depleted as they react
  Bottom (500 nm): Severely depleted
  
Depletion model (conservation of radical flux):

Continuity equation:
  dφ/dz = −k × φ × v_etch
  
  where:
    z: depth into via
    k: reaction rate coefficient
    v_etch: etch rate (consumes radicals)
  
Solution:
  φ(z) = φ₀ × exp(−α × z)
  
  where α = k × v_etch (depletion coefficient)
  
  Empirically: α ≈ 0.003-0.01 /nm (depends on gas, pressure)

Quantitative example (100:1 AR via):

  α = 0.005 /nm (typical)
  
  At z = 100 nm (20% depth):
    φ(100) = φ₀ × exp(−0.005 × 100) = φ₀ × exp(−0.5) = 0.606 × φ₀
    (39% depletion)
  
  At z = 250 nm (50% depth):
    φ(250) = φ₀ × exp(−1.25) = 0.287 × φ₀
    (71% depletion)
  
  At z = 400 nm (80% depth):
    φ(400) = φ₀ × exp(−2.0) = 0.135 × φ₀
    (86% depletion)
  
  At z = 500 nm (100% depth, bottom):
    φ(500) = φ₀ × exp(−2.5) = 0.082 × φ₀
    (92% depletion!)

Etch rate vs. depth:

R(z) ∝ φ(z) (etch rate proportional to radical flux)

  R(500) / R(0) = 0.082 = 8.2% (bottom etches only 8% as fast as top!)
  
  Etch time variation:
    Top: Completes in time t_fast
    Bottom: Takes time t_bottom = t_fast / 0.082 ≈ 12× longer
    
  Net: Bottom still reaches 500 nm depth, but through much slower process

ARDE ratio definition:

  ARDE = R_top / R_bottom = 1 / 0.082 = 12:1
  (For this specific via geometry and depletion model)
  
  In production: ARDE values 5-100:1 typical (depends on AR, pressure, chemistry)
```

### 10.1.2 Scaling with Aspect Ratio

```
ARDE scales approximately with AR:

Theoretical prediction:
  ARDE ≈ 1 + β × AR
  
  where β ≈ 0.1-0.2 (empirical fit parameter)

Experimental data (Cl₂ etch):

  AR    | ARDE (measured) | ARDE (predicted) | Depth (nm)
  ------|-----------------|------------------|----------
  5:1   | 2:1             | 1.5:1            | 50
  10:1  | 3:1             | 2:1              | 100
  20:1  | 5:1             | 3:1              | 200
  50:1  | 12:1            | 6:1              | 500
  100:1 | 25:1            | 11:1             | 1000
  
  (Predicted values conservative; actual ARDE often worse)

For 100:1 contact via (5 nm wide, 500 nm deep):

  Predicted ARDE: 12:1
  Actual (with shadowing): 20-50:1 typical
  
  Reason: Shadowing (lateral ion blocking) additional to radical depletion
  
Production impact:

  3D NAND contact (100:1 AR, 500 nm depth):
    Top etch completes in 120 seconds
    Bottom still etching at 1/20th rate
    Total time to clear bottom: 2400 seconds (40 minutes!) vs. 120 sec
    
    OR: Accept bottom incomplete, get high-aspect-ratio voids
    
  Result: ARDE is production bottleneck at extreme AR
```

---

## 10.2 Compensation Strategies

### 10.2.1 Multi-Step ARDE Compensation

```
Three-step recipe approach:

Step 1: Fast bulk etch (high power, poor selectivity acceptable)
  Duration: 60 sec
  Target: Etch 250 nm (50% of total depth)
  Power: 2000 W coil, 1500 W bias (maximum)
  Pressure: 40 mTorr
  Expected: R_top ≈ 100 nm/min, R_bottom ≈ 20 nm/min
  ARDE compensation: Not compensated; faster is fine
  
Step 2: Transition (moderate power, increasing selectivity)
  Duration: 40 sec
  Target: Etch additional 150 nm (bringing total to 400 nm)
  Power: 1500 W coil, 800 W bias
  Pressure: 50 mTorr (higher, helps uniformity)
  Expected: R_top ≈ 50 nm/min, R_bottom ≈ 20 nm/min
  ARDE: 2.5:1 (improved due to higher pressure reducing directivity)
  
Step 3: Selective finish (low power, high selectivity)
  Duration: 60 sec
  Target: Etch final 100 nm to oxide (reaching 500 nm total)
  Power: 800 W coil, 300 W bias
  Pressure: 30 mTorr (lower, more selective)
  Expected: R_top ≈ 30 nm/min, R_bottom ≈ 20 nm/min
  ARDE: 1.5:1 (minimal variation, conservative)
  
Total time: ~160 sec (2.7 min) to etch 500 nm

Analysis:
  Step 1: Deposits most at top, some at bottom (bulk removal)
  Step 2: Continued etching, transition to selectivity
  Step 3: Final removal with tight selectivity, minimal over-etch
  
  Result: Bottom reaches target depth via "gentle" finishing
          Avoids catastrophic over-etch (which would reach through oxide)

Effectiveness:
  Without compensation: ARDE 25:1, time to clear >400 sec
  With 3-step: ARDE ~8:1 average, time ~160 sec
  Improvement: ~2.5× faster, ARDE 3× better
  Cost: 50% longer total time vs. single-step
  Trade: Acceptable for production (multi-step recipes standard)
```

### 10.2.2 Pressure & Pulsed Plasma Compensation

```
Pressure modulation effect:

Low pressure (10 mTorr):
  Mean free path λ ≈ 1 mm (very long)
  Radicals travel in straight lines
  More collisions with sidewalls (but still directional)
  ARDE worse: 25-50:1 typical
  But selectivity excellent: 100-200:1
  
High pressure (80 mTorr):
  Mean free path λ ≈ 0.1 mm (very short)
  Radicals scattered, more diffusive
  More even coverage, fewer corner effects
  ARDE better: 5-10:1 typical
  But selectivity worse: 20-50:1
  
Optimal: ~30-50 mTorr (balance)
  ARDE: 10-15:1 (manageable)
  Selectivity: 80-100:1 (adequate)

Pulsed plasma strategy:

ON/OFF cycling:

  Plasma ON 10 sec:
    Radicals generated, etch proceeds
    Top region etches ~100 nm
    Bottom region (depleted) etches ~20 nm
  
  Plasma OFF 10 sec:
    No new radicals
    Existing radicals diffuse
    Concentration equalizes (partial refill)
    Bottom "catches up" via diffusion alone
  
  Next ON cycle:
    Both top and bottom start with better radical balance
    ARDE reduced for this cycle
  
Duty cycle effect:

  100% duty (continuous): ARDE 20:1
  50% duty (5 sec ON, 5 sec OFF): ARDE 8:1 (60% reduction!)
  25% duty (5 sec ON, 15 sec OFF): ARDE 4:1 (but 4× longer total time!)

Cost:
  Pulsed etch: 50% duty → 2× longer process time
  Trade: ~3× better ARDE vs. 2× time penalty
  ROI: Enables higher-AR processes (100:1 → practical etch windows)

Production adoption:
  High-volume (3D NAND): Pulsed etch standard (extreme AR unavoidable)
  Logic (50:1 contact): Multi-step recipe often sufficient (pulsing optional)
  Low-volume (R&D): Single-step acceptable if selectivity margin large
```

---

## 10.3 Uniformity Across Wafer

### 10.3.1 Center vs. Edge ARDE

```
ARDE variation across wafer:

Center region:
  Plasma density high (coil coupling stronger at center)
  Radical flux higher
  Depletion faster (fewer radicals available at bottom)
  ARDE worse: 20-30:1 typical

Edge region:
  Plasma density lower (coil geometry, showerhead edge effects)
  Radical flux 10-20% lower than center
  Depletion effect smaller (less etch total, so less depletion)
  ARDE better: 10-15:1

Result:
  Center etches slower at bottom than edge
  Creates radial variation in final profile
  
  Top etch completion: Center first (higher flux)
  Bottom etch completion: Edge first (lower ARDE)
  
  Thickness variation: ±10-20% center-to-edge possible

Mitigation:

  1. Showerhead design (unequal hole sizes)
     Reduce flow at center (restrict flux)
     Increase flow at edge (boost flux)
     Result: Equalizes radical availability across wafer
     Effectiveness: Can reduce ARDE variation to ±5-10%

  2. Edge ring RF power
     Increase bias on outer ring
     Higher E_ion at edge → more sputtering
     Compensates lower flux-dependent etch
     Result: Partial compensation of ARDE effects
     Effectiveness: ±5-10% reduction

  3. Thermal compensation
     Edge cooling (He backside more efficient at edge?)
     This is marginal, rarely used for ARDE

Combination approach (best practice):
  Showerhead optimization + Edge ring RF + Multi-step recipe
  Result: Can achieve ±5-10% within-wafer ARDE uniformity
```

---

## 10.4 Summary & Key Takeaways

1. **Radical Depletion Exponential** — φ(z) = φ₀ × exp(−αz); at 500 nm depth, 92% depletion typical; etch rate bottom = 8% of top → 12:1 ARDE minimum.

2. **ARDE Scales with AR** — ARDE ≈ 1 + β×AR (β~0.1-0.2); 100:1 contact → 12-50:1 ARDE depending on shadowing; 3D NAND severely impacted.

3. **Multi-Step Recipe Divides ARDE** — Step 1 (fast bulk, poor uniformity), Step 2 (transition), Step 3 (slow selective finish); average ARDE reduced 3× vs. single-step.

4. **Pulsed Plasma Diffuses Bottom** — 50% duty cycle (10 sec ON, 10 sec OFF) reduces ARDE 60% via radical redistribution; cost: 2× longer time; ROI high for extreme AR.

5. **Pressure Trade-off** — Low-P (10 mTorr) ARDE 25:1 but selective 100:1; high-P (80 mTorr) ARDE 5:1 but selective 20:1; optimal 30-50 mTorr balances.

6. **Showerhead Optimization Essential** — Center plasma 15% denser → worse ARDE; unequal hole sizes reduce center flow, equalize radical availability across wafer; ±10-20% variation down to ±5-10%.

7. **ARDE is Throughput Limiter** — 500 nm etch with uncompensated ARDE: 2400 sec to clear bottom vs. 120 sec with 3-step recipe; scheduling ARDE compensation recovery is production bottleneck.

---

**Next Chapter:** [Chapter 11 - Metal Etch Selectivity to Dielectrics](./11-selectivity-tuning.md)

**Chapter 10 Development Status:** Complete high-AR ARDE modeling and compensation framework  
**Version:** 1.0

