# Chapter 9: Gas Delivery & Plasma Chemistry Control

## Overview

Recipe tuning requires precise gas composition control. This chapter covers MFC tuning, additive strategy, plasma diagnostics (RGA), and optimization for uniformity and selectivity.

**Learning Objectives:**
- Design multi-gas flow recipes
- Tune O₂, HBr, N₂ additives for profile control
- Use RGA for plasma composition diagnosis
- Optimize flow for uniformity
- Model flow dynamics and mixing

---

## 9.1 Multi-Gas Recipe Strategy

### 9.1.1 Primary Gas & Additive Roles

```
Cl₂ primary etch gas (control via MFC):

Flow range: 0-500 sccm (scale depends on process)

Example recipes:

Bulk etch (fast, less selective):
  Cl₂: 300 sccm (main etch species)
  O₂: 0 sccm (none)
  N₂: 0 sccm (none)
  Total: 300 sccm, 40 mTorr (typical)
  Selectivity: ~50-80:1 (good for bulk)

Transition (balanced):
  Cl₂: 250 sccm (reduced)
  O₂: 10 sccm (1% additive, helps profile)
  N₂: 0 sccm
  Total: 260 sccm, 35 mTorr
  Selectivity: ~80-120:1 (better)

Selective finish (slow, high selectivity):
  Cl₂: 150 sccm (low, for slow etch)
  O₂: 10 sccm (2% additive, SiO₂ protection)
  N₂: 50 sccm (20% diluent, reduces etch rate, improves uniformity)
  Total: 210 sccm, 30 mTorr
  Selectivity: ~100-150:1 (excellent)

Cost per wafer (gas consumables):

Cl₂ cost: ~$40/kg = $0.04/g
Consumption (bulk etch):
  300 sccm × 30 sec = 9000 sccm·sec = 0.15 L @ STP
  Mass: 0.15 L × (71 g/mol / 22.4 L/mol) ≈ 0.48 g
  Cost per wafer: 0.48 × $0.04 = $0.02/wafer (very cheap!)

O₂ cost: ~$10/kg = $0.01/g (cheaper than Cl₂)
Consumption (selective finish):
  10 sccm × 30 sec = 300 sccm·sec ≈ 0.005 L
  Mass: 0.005 × 32/22.4 ≈ 0.007 g
  Cost: 0.007 × $0.01 = $0.00007/wafer (negligible)

N₂ cost: ~$5/kg = $0.005/g
Consumption (selective finish):
  50 sccm × 30 sec = 1500 sccm·sec = 0.025 L
  Mass: 0.025 × 28/22.4 ≈ 0.031 g
  Cost: 0.031 × $0.005 = $0.00016/wafer (negligible)

Total gas cost per wafer: ~$0.02 (less than 1¢!)
Annual (50K wafers): ~$1,000 (minimal vs. equipment cost)
```

### 9.1.2 Additive Effects on Process

```
Oxygen (O₂) additive:

Effect on selectivity:
  Forms SiO₂ protection layer on dielectric surface
  O• radical creates SiO₂ coating (even during etch)
  Etch rate of SiO₂ slows dramatically
  
Typical selectivity improvement:
  0% O₂: S = 50:1
  1% O₂: S = 100:1 (2× improvement!)
  3% O₂: S = 150:1 (best)
  5% O₂: S = 140:1 (saturation, slight decrease)

Side effects:
  O₂ consumes some Cl• (competes for radicals)
  W etch rate drops ~10-20% with 3% O₂
  Trade-off: Slower etch but better selectivity
  
Production use:
  Step 1 (bulk): 0% O₂ (maximum etch rate)
  Step 3 (finish): 2-3% O₂ (maximum selectivity)

Hydrogen bromide (HBr) additive (rare, specialized):

Effect on profile:
  Br• modifies sidewall chemistry
  Can reduce scalloping (smoother sidewalls)
  
Typical usage:
  HBr: 0.5-2% of flow
  Purpose: Profile smoothing in high-AR features
  Trade-off: More complex plasma, less predictable

Nitrogen (N₂) diluent:

Effect on etch rate:
  N₂ doesn't etch, just dilutes Cl•
  Lower Cl• concentration → slower etch
  
Uniformity improvement:
  High N₂ reduces ARDE (fewer radicals, less depletion effect)
  More uniform etch across AR variation
  
Typical usage:
  0% N₂: Fast but non-uniform (ARDE +/−20%)
  10% N₂: Balanced (ARDE +/−10%)
  20% N₂: Uniform but slow (ARDE +/−5%, etch rate -30%)
  
  Selective finish step often uses 15-25% N₂
```

---

## 9.2 Plasma Diagnostics & Monitoring

### 9.2.1 Residual Gas Analyzer (RGA)

```
RGA principle:

Mass spectrometer attached to chamber exhaust
Measures partial pressure of different gas species
Real-time plasma composition monitoring

Detection:

Vacuum ionization gauge:
  Electron beam ionizes gas molecules
  Voltage-swept analyzer selects mass
  Detector counts ions at each mass
  
Scan over mass range:
  m/z = 1-100 (covers all relevant species)
  Measurement time: ~30-60 sec per full scan

Typical RGA results (Cl₂ etch with O₂ additive):

Species        | m/z | Typical pressure (mTorr) | Notes
---------------|-----|--------------------------|----------
Cl₂            | 70  | 25-30                    | Main etch gas
Cl• (radical)  | 35  | 0.01-0.1                 | Doesn't ionize well, hard to measure directly
O₂             | 32  | 0.3-1.0                  | Additive, 1-3% of total
Cl⁺ (ion)      | 35  | 0.001-0.01               | Ions, small contribution
N₂             | 28  | 1-10                     | If diluent used
H₂O            | 18  | 0.1-0.5                  | Residual moisture (contamination)
WCl_x          | 300-385| <0.001                | Byproduct, mostly escapes
Ar             | 40  | <0.1                     | Calibration gas

Production use:

Daily check:
  Are gases flowing as expected?
  Is moisture contamination too high?
  Has O₂ pressure drifted?
  
Troubleshooting:
  If etch rate drops: Check Cl₂ partial pressure (bottle empty?)
  If selectivity degrades: Check O₂ level (additive not flowing?)
  If particles appear: Check H₂O (too high moisture → oxidation?)

Cost:
  RGA system: ~$50-100K installed
  Maintenance: ~$5K/year
  ROI: Prevents recipe drift issues, catches contamination
  Value: Diagnostics for complex multi-gas recipes
```

### 9.2.2 Flow Rate Tuning for Uniformity

```
Flow dynamics:

Gas enters chamber via showerhead
Flows radially outward toward exhaust
Pressure builds up, then exits

Flow pattern (simplified):

Radial flow velocity: v_r ∝ P / (μ × gap)
  where μ = gas viscosity

Higher pressure → faster radial flow → gas leaves quickly
Lower pressure → slower flow → longer residence time

Residence time effect:

Long residence time:
  Gas spends time in chamber
  More collisions, more complete dissociation
  Better uniformity (gas mix more homogeneous at different radii)
  
Short residence time:
  Gas exits fast
  Less time for mixing
  Edge gets fresher gas mixture, center depleted
  Non-uniformity possible

Optimization:

Set pressure for good mixing:
  Too low (<10 mTorr): Mean free path very long, poor mixing
  Too high (>100 mTorr): Flow so fast, radial gradient forms
  Optimal: 30-50 mTorr (good balance)
  
Total flow rate:
  Higher flow → fills chamber faster → less mixing
  Lower flow → more time for mixing → better uniformity
  But very low flow → pressure control difficult
  
  Typical: 200-400 sccm total (balance point)

Additive placement:

Add O₂ upstream (before showerhead):
  Mixes with Cl₂ before entering
  Reaches center and edge uniformly
  Better selectivity uniformity
  
Add O₂ downstream (direct chamber inlet):
  Reaches chamber directly
  May not mix well with bulk Cl₂
  Radial non-uniformity possible
  
Production: Upstream addition preferred (MFC mix station)
```

---

## 9.3 Summary & Key Takeaways

1. **Gas Cost Negligible** — Cl₂ ~$0.02/wafer, O₂/N₂ additives <$0.0001/wafer; gas cost <1% of total; focus on selectivity benefit, not cost savings.

2. **O₂ Additive Doubles Selectivity** — 0% → 1% O₂: selectivity 50:1 → 100:1; 3% O₂ optimal (~150:1); side effect: W etch rate drops 10-20% (acceptable trade-off).

3. **N₂ Diluent Improves Uniformity** — Reduces ARDE by 50%; 20% N₂ achieves ±5% uniformity (vs. ±20% with pure Cl₂); cost: etch rate slows 30% (balance in multi-step recipe).

4. **RGA Monitors Plasma Health** — Detects gas drift (Cl₂ bottle pressure), contamination (H₂O >1 mTorr, problem), additive flow (O₂/N₂ verification); costs $50K, prevents recipe drift.

5. **Pressure Sweet Spot 30-50 mTorr** — Lower pressure (<10 mTorr) poor mixing, higher (>100 mTorr) fast flow non-uniform; 30-50 optimal for selectivity + uniformity balance.

6. **Multi-Step Gas Recipe Exploits Tuning** — Step 1 (pure Cl₂, fast); Step 2 (1% O₂, balanced); Step 3 (3% O₂ + 20% N₂, selective+uniform); combines speed and quality.

7. **Upstream Additive Mixing Critical** — Add O₂/N₂ before showerhead (MFC combination) for uniform mixing; avoid direct-chamber addition (causes radial gradients).

---

**End of Part II: Hardware Design (Chapters 5-9) COMPLETE**

**Chapter 9 Development Status:** Complete gas delivery and plasma control framework  
**Version:** 1.0

