# Chapter 8: Thermal Management During Metal Etch

## Overview

High bias power (1000-1500 W) converts to substrate heat (~80% efficiency), raising wafer temperature 50-100°C. This chapter quantifies thermal effects on selectivity, profile, and reliability—and designs cooling systems to maintain process windows.

**Learning Objectives:**
- Model RF power to substrate heating
- Design active cooling systems
- Quantify selectivity and etch rate temperature coefficients
- Predict thermal transients during recipe steps
- Optimize cluster tool thermal isolation

---

## 8.1 Substrate Heating from RF Power

### 8.1.1 Power Dissipation Model

```
RF power conversion to heat:

Bias power (electrical): P_bias = 1000 W (example)

Energy distribution:
  ~80% → Substrate heating (ion bombardment transfers energy)
  ~10% → Radiative/convective loss (chamber cooling)
  ~10% → RF matching loss (reflected power, tuning)
  
Substrate heating power: P_heat ≈ 800 W

Heat flux at wafer surface:
  Wafer area: A = π × (100 mm)² ≈ 31,416 mm² = 314 cm²
  Heat flux density: q = P / A = 800 / 314 ≈ 2.5 W/cm²

Temperature rise calculation:

Thermal resistance from wafer to chuck:
  R_thermal = (T_wafer − T_chuck) / P_heat
  
  Typical: R_thermal ≈ 0.1-0.2 K/W (depends on wafer clamping, backside gas)
  
  ΔT = P_heat × R_thermal = 800 × 0.15 = 120°C (substantial!)

Actual temperature rise:

Without active cooling:
  Chuck setpoint: 20°C (room temperature)
  Wafer temperature during etch: 20 + 120 = 140°C (very hot!)
  
With mechanical chiller at chuck:
  Chuck setpoint: 0°C (chilled)
  Wafer temperature: 0 + 120 = 120°C (slightly better)
  
With He backside cooling:
  Thermal conductance improved ~10× (He gas conducts heat better)
  Effective R_thermal ≈ 0.01-0.02 K/W
  ΔT ≈ 800 × 0.015 ≈ 12°C (much better!)
  Wafer temperature: 20 + 12 = 32°C (nearly ambient)

Trade-off: Cooling cost vs. temperature control
  No cooling: $0, but T +120°C (selectivity/profile risk)
  Water chiller: $30-50K capital, $10K/year, gives T +50-80°C
  He backside: $50K capital + $5K/year gas, gives T +10-20°C
```

### 8.1.2 Temperature Effects on Selectivity

```
Selectivity temperature dependence:

From Chapter 3: S(T) ∝ exp((E_a,SiO₂ − E_a,W) / RT)
                    = exp(13 / RT)  (where E_a ≈ 22 − 9 = 13 kcal/mol)

Calculation:

At T = 293 K (20°C):
  S ∝ exp(13 / (1.987×10⁻³ × 293)) = exp(22.3) ≈ 10⁹ (theoretical max)
  Practical: ~100-150:1 (limited by other factors)

At T = 333 K (60°C):
  S ∝ exp(13 / (1.987×10⁻³ × 333)) = exp(19.6) ≈ 2×10⁸
  Practical: ~80-120:1 (10-30% loss)

At T = 373 K (100°C):
  S ∝ exp(13 / (1.987×10⁻³ × 373)) = exp(17.5) ≈ 4×10⁷
  Practical: ~60-100:1 (30-50% loss)

At T = 413 K (140°C, without active cooling):
  S ∝ exp(13 / (1.987×10⁻³ × 413)) = exp(15.8) ≈ 7×10⁶
  Practical: ~40-70:1 (major selectivity loss)

Production consequence:

Recipe tuned at 20°C (room temperature):
  Selectivity target: 100:1
  Selectivity achieved: 100-150:1 (exceeds target)
  
If wafer heats to 140°C during etch:
  Selectivity achieved: 50:1 (50% loss!)
  Risk: Over-etch into oxide, damage profile
  Yield loss: Yes (out of window)

Mitigation:

Option 1: Reduce etch time (shorter → less heating)
  Selectivity window narrower
  But wafer heats up less
  Trade-off: Works if process already selective enough
  
Option 2: Active cooling
  Maintain T ~30-50°C
  Selectivity stays in window
  Higher equipment cost, but reliable process
  
Option 3: Multi-step recipe
  Step 1: No cooling, hot etch (fast bulk, less sensitive to selectivity)
  Step 2: Activate cooling, warm etch (careful selective finish, T controlled)
  Result: Balance speed and selectivity
```

---

## 8.2 Cooling System Design

### 8.2.1 Mechanical Chiller vs. LN₂

```
Mechanical chiller (common, cost-effective):

Design:
  Vapor-compression refrigeration cycle
  Water coolant circulates through chuck
  Compressor driven by AC motor

Specifications:
  Cooling capacity: ~5-10 kW (depends on model)
  Setpoint range: −20 to +50°C
  Temperature stability: ±2-5°C
  Power consumption: ~2-5 kW (compressor runs continuously)

Cost:
  Capital: $30-50K
  Annual operating: $5-10K (electricity, maintenance)
  Payback: ~5-7 years (if high-volume production)
  
Performance:
  Wafer temperature at 1000 W bias: ~50-80°C (warm)
  Selectivity: ~70-100:1 (marginal, not ideal)

Advantages:
  Cost-effective
  No special gas supply needed
  Reliable, proven technology
  Easy maintenance

Disadvantages:
  Limited cooling capacity
  Can't reach true cryogenic
  Wafer still heats significantly
  Selectivity not optimal

LN₂ (liquid nitrogen) cooling:

Design:
  LN₂ (−196°C) circulates through chuck
  Extremely cold, excellent cooling
  Vaporizes, gas exhausted

Specifications:
  Cooling capacity: ~20-50 kW (very high!)
  Setpoint range: −140 to +50°C
  Temperature stability: ±3°C (excellent)
  Consumption: ~500 L/week (expensive!)

Cost:
  Capital: $50-100K (equipment purchase + installation)
  Annual operating: $20-30K (LN₂ gas, $0.50/L × 26K L/year)
  Payback: ~3-5 years (justifiable for high-value fabs)
  
Performance:
  Wafer temperature at 1000 W bias: ~30-50°C (warm but controlled)
  Selectivity: ~100-150:1 (excellent)

Advantages:
  Highest cooling power
  Enables cryogenic etch (if needed)
  Best selectivity control
  Stable over long run

Disadvantages:
  High operating cost
  LN₂ supply logistics (weekly refills)
  Safety concerns (cryogenic hazard)
  Evaporation losses

Comparison table:

Parameter              | Mechanical | LN₂
-----------------------|------------|--------
Capital cost           | $40K       | $75K
Annual operating       | $7.5K      | $25K
Wafer temp (1000W)     | 60°C       | 40°C
Selectivity achieved   | 80:1       | 120:1
Process margin         | Marginal   | Excellent
Best for              | Low-cost   | High-value
                      | fabs       | production

Fab decision:
  Budget-conscious → Mechanical chiller
  High-volume → LN₂ (margin worth cost)
  Research/development → Mechanical (flexibility)
```

### 8.2.2 Backside Gas Cooling

```
Helium backside cooling:

Principle:
  Wafer sits on chuck electrode
  He gas (or N₂) flows at back surface of wafer
  He excellent thermal conductor (5× better than air)
  Improves heat transfer from wafer to chuck ~10×

Implementation:
  Small gas inlet channel in chuck
  He supply: ~0.1-1 L/min at low pressure
  Maintains thin He layer between wafer and chuck

Thermal improvement:
  Without He: R_thermal ≈ 0.1-0.2 K/W
  With He (1 mTorr He): R_thermal ≈ 0.01-0.02 K/W (10× improvement!)
  
  Effect: ΔT = 800 W × 0.015 K/W ≈ 12°C
  Wafer temperature with 20°C chuck: ~32°C (much better!)

Combination: Chiller + He backside

Mechanical chiller setpoint: 0°C
He backside gas: Reduces ΔT from 60°C to ~15°C
Final wafer temperature: 0 + 15 = 15°C (excellent control!)

Cost:
  He supply: ~$50/month (modest)
  Plumbing/integration: ~$10K one-time
  Payback: Very fast (enables better recipes, higher yield)

Downsides:
  He gas cost (not cheap)
  Plumbing complexity (He line integration into chuck)
  Potential He leakage/contamination issues
  Require chiller as foundation (can't rely on He alone)

Modern approach:
  Most high-end tools: Mechanical chiller + He backside combination
  Achieves stable T ~30-40°C with acceptable cost
  Provides process margin needed for complex recipes
```

---

## 8.3 Thermal Transients & Multi-Step Recipes

### 8.3.1 Temperature Evolution During Recipe

```
Typical 3-step recipe:

Step 1 (bulk etch):
  Duration: 30 sec
  High power (2000 W coil, 1500 W bias)
  Fast etch rate (~100 nm/min)
  
  Temperature profile:
    t=0 sec: T = 20°C (chuck setpoint, wafer starts cool)
    t=5 sec: T = 50°C (rapid heating from bias power)
    t=10 sec: T = 70°C (approaching steady state)
    t=30 sec: T = 85°C (steady state reached)
  
  Time to steady state: ~20-30 sec (long!)

Step 2 (transition):
  Duration: 20 sec
  Medium power (1500 W coil, 800 W bias)
  Moderate etch rate (~50 nm/min)
  
  Temperature change:
    t=0 sec (start of step 2): T = 85°C (inherited from step 1)
    Bias power drops → ΔT decreases
    New steady state: ΔT = 400 W × 0.15 K/W = 60°C
    Final T: 20 + 60 = 80°C
    Time to equilibrate: ~10-15 sec
    
    t=20 sec: T = 80°C (reached new steady state)

Step 3 (selective finish):
  Duration: 30 sec
  Low power (1000 W coil, 400 W bias)
  Slow etch rate (~30 nm/min), high selectivity
  
  Temperature change:
    t=0 sec: T = 80°C (inherited)
    Bias power drops further → ΔT = 200 W × 0.15 K/W = 30°C
    New steady state: T = 50°C
    Time to cool: ~15-20 sec
    
    t=30 sec: T = 50°C (stabilized)

Summary:

Step 1: Etch fast (bulk, hot, ~100 nm/min)
Step 2: Transition (moderate, warm, ~50 nm/min)
Step 3: Selective finish (slow, cool, ~30 nm/min, high selectivity)

Total etch depth: ~100 nm (example)
Total time: ~80 sec
Temperature swing: 20°C → 85°C → 50°C

Selectivity impact:
  Step 1 (hot, T=85°C): S ≈ 60:1 (adequate, bulk etch less sensitive)
  Step 3 (cool, T=50°C): S ≈ 120:1 (excellent, selective finish needs margin)

This recipe structure exploits thermal transients to balance speed and selectivity!
```

---

## 8.4 Summary & Key Takeaways

1. **RF Power Converts to Substrate Heat** — Bias 1000 W → ~800 W heating; without cooling, wafer rises 120°C above chuck temperature; heating dominates thermal budget.

2. **Selectivity Degrades 10× per 50°C** — E_a difference ~13 kcal/mol; selectivity S ∝ exp(13/RT); from 20°C to 140°C: selectivity drops 100:1 → 50:1 (50% loss).

3. **Mechanical Chiller Cost-Effective** — $40K capital + $7.5K/year; enables ~60°C wafer temperature at 1 kW bias; acceptable for many processes but not optimal selectivity.

4. **He Backside Cooling Dramatic** — Improves thermal conductance 10×; reduces ΔT from 60°C to ~15°C; enables wafer T ~30°C even at high bias power.

5. **LN₂ Cryogenic Cooling Premium** — $75K capital + $25K/year LN₂ cost; enables 40°C wafer T and 120:1 selectivity; justified for high-value production.

6. **Multi-Step Recipe Exploits Transients** — Step 1 (hot, fast bulk); Step 2 (warm, transition); Step 3 (cool, selective finish); balances speed with selectivity margin.

7. **Thermal Equilibration ~20-30 sec** — Full steady-state reached; short recipes may never reach steady T; transient effects significant; recipe design accounts for heating ramps.

---

**Next Chapter:** [Chapter 9 - Gas Delivery & Plasma Control](./09-gas-delivery.md)

**Chapter 8 Development Status:** Complete thermal management framework  
**Version:** 1.0

