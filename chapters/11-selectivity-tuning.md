# Chapter 11: Metal Etch Selectivity to Dielectrics

## Overview

Selectivity determines process window width. This chapter quantifies W/SiO₂ and Cu/SiN selectivity mechanisms, models temperature/pressure/chemistry effects, and optimizes for production margin.

---

## 11.1 Selectivity Mechanisms

### 11.1.1 Temperature-Dependent Chemistry

```
Selectivity fundamentals:

S(T) = R_W / R_SiO₂ ∝ exp((E_a,SiO₂ − E_a,W) / RT)

Activation energies:
  W etch: E_a ≈ 9 kcal/mol (low, chemistry facile)
  SiO₂ etch: E_a ≈ 22 kcal/mol (high, chemistry difficult)
  Difference: ΔE_a = 13 kcal/mol

Temperature effect (Cl₂ plasma):

  At 20°C (293 K):
    S ∝ exp(13 / 0.001987 × 293) = exp(22.3) → S_practical = 100-150:1
  
  At 50°C (323 K):
    S ∝ exp(13 / 0.001987 × 323) = exp(20.1) → S_practical = 70-100:1
  
  At 100°C (373 K):
    S ∝ exp(13 / 0.001987 × 373) = exp(17.5) → S_practical = 40-70:1
  
  Trend: Every 20°C rise → 20-30% selectivity degradation

Production consequence:

  Recipe tuned at 20°C (room T):
    Design selectivity target: 100:1
    Actual at 20°C: 120:1 (good margin)
    
  Substrate heats to 60°C during etch (high bias power):
    Selectivity at 60°C: 80:1 (33% loss!)
    Risk: Over-etch into oxide
    Yield: May fail if process window tight
```

### 11.1.2 Pressure & Ion Energy Effects

```
Pressure modulation:

Low pressure (10 mTorr):
  Fewer ion collisions with neutral gas
  More directed ion impact
  Higher effective ion energy
  More ion-driven sputtering contribution
  Result: SiO₂ sputtering increases (less selective)
  Typical: S = 50-80:1

Mid pressure (40 mTorr):
  Balanced ion/radical contributions
  Directional but some scattering
  Result: S = 100-150:1 (optimal)

High pressure (100 mTorr):
  Many collisions, ions thermalized
  Directivity lost, more chemical etch dominates
  Chemical selectivity naturally high
  Result: S = 120-180:1 (but slower etch)

Ion energy tuning:

Lower E_ion (reduce bias power):
  Less physical sputtering of SiO₂
  Chemical etch dominates for both materials
  Chemical selectivity naturally high
  Result: S = 100-200:1 (excellent)

Higher E_ion (increase bias power):
  More physical sputtering (ion contribution ~30% for SiO₂)
  Selectivity reduced
  Result: S = 50-100:1 (lower margin)

Production strategy:

Step 1 (bulk): High E_ion (fast, accept lower selectivity ~50:1)
Step 2 (finish): Low E_ion (slow, high selectivity ~150:1)
Result: Balance speed with selectivity margin
```

### 11.1.3 Additive Gas Effects

```
Oxygen (O₂) impact:

O₂ forms protective layer on SiO₂:
  SiO₂ surface oxidizes further
  Creates SiO₂-on-SiO₂ coating (very resistant)
  Etch rate of SiO₂ drops dramatically

Selectivity improvement:

Without O₂: S_W/SiO₂ = 50:1
With 1% O₂: S_W/SiO₂ = 100:1 (2× improvement!)
With 3% O₂: S_W/SiO₂ = 150:1 (3× improvement!)

Trade-off:
  W etch rate reduced 10-20% (O₂ consumes Cl• that would etch W)
  Acceptable (selectivity benefit > etch rate penalty)

HBr additive (alternative):

Br• etch chemistry different from Cl•
Can tune selectivity via Cl:Br ratio
Less effective than O₂ but offers additional tuning knob
Used in specialized recipes (rare)
```

---

## 11.2 Selectivity Windows & Process Control

### 11.2.1 Selectivity Windows

```
Selectivity requirement:

Via etch 100 nm through 50 nm SiO₂ dielectric:

Safe selectivity:
  S_min = 100 nm / 5 nm = 20:1
  (Over-etch 5 nm into dielectric, still safe margin)

Comfortable margin:
  S_design = 50:1 (provides 2× safety)

Excellent:
  S_actual = 100:1 (huge margin)

Process window (temperature range):

Recipe tuned at 20°C with S_design = 100:1:

  At 0°C: S = 120:1 (even better)
  At 20°C: S = 100:1 (target)
  At 40°C: S = 85:1 (margin eroding)
  At 60°C: S = 70:1 (approaching minimum 50:1)
  At 80°C: S = 50:1 (at limit!)
  At 100°C: S = 35:1 (FAIL! S < S_min)

Process window: 0-80°C (80°C range!)
Control strategy: Keep substrate 20-60°C → maintain safety margin

With active cooling (He backside):
  Can keep substrate 30-40°C
  Selectivity stays 80-100:1 (excellent)
  Process window: ±50°C comfortable
  Recipe robust to thermal variation
```

---

## 11.3 Summary & Key Takeaways

1. **Selectivity Temperature-Exponential** — S ∝ exp(13/RT); E_a difference 13 kcal/mol; 20°C → 100°C: selectivity drops 100:1 → 40:1 (60% loss).

2. **Pressure Sweet Spot 30-50 mTorr** — Low-P selective (80:1) but ARDE worse; high-P uniform (140:1) but slow; mid-P balances both ~100:1.

3. **O₂ Additive Doubles Selectivity** — Protective SiO₂ layer formation; 0% → 3% O₂: selectivity 50:1 → 150:1; W etch rate drops 10-20% (acceptable).

4. **Ion Energy Tuning Effective** — Low E_ion → chemical etch dominates (high selectivity); high E_ion → sputtering increases (selectivity degrades 50-100%).

5. **Process Window Large with Control** — Recipe at 20°C: S=100:1; uncontrolled heating → 100°C: S=35:1 (fail); with cooling maintains 80:1 (safe).

6. **Multi-Step Recipe Exploits Selectivity** — Bulk step (high power, low selectivity acceptable); finish step (low power + O₂, high selectivity margin); trades speed for yield.

7. **Selectivity Spec Typically 50:1+** — Over-etch margin ~5 nm; 50:1 minimum for 100 nm etch through 50 nm oxide; 100:1 design target provides safety.

---

**Next Chapter:** [Chapter 12 - Profile & Residue Formation](./12-profile-residue.md)

**Chapter 11 Development Status:** Complete selectivity tuning framework  
**Version:** 1.0

