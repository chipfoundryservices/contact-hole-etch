# Chapter 6: Ion Source & Energy Control

## Overview

Independent control of ion flux (via coil power) and ion energy (via bias power) is the key advantage of CCP over ICP. This chapter quantifies plasma generation, ion energy distribution, and spatial uniformity—the foundation for selectivity and profile tuning.

**Learning Objectives:**
- Understand ion generation and energy from RF fields
- Quantify coil/bias power relationship to flux and energy
- Model ion energy distribution (IED)
- Design for spatial uniformity
- Predict temperature and pressure effects on plasma

---

## 6.1 Plasma Generation in CCP

### 6.1.1 Coil Power & Plasma Density

```
Inductive coupling (coil power):

13.56 MHz RF current flows through coil
Magnetic field induces electric field in plasma
Electrons accelerated by E-field, gain energy
Collisions with neutral atoms → ionization

Ionization rate vs. coil power:

Electron avalanche multiplication:
  n_e(t) = n_e,0 × exp(α × z)
  
  where α = ionization coefficient (cm⁻¹)
  α ∝ E/P (electric field / pressure)
  
  Higher E/P → more ionization

Power-to-plasma relationship:

Simplified plasma density model:
  n_e ∝ √(P_coil)
  
  (Empirically observed for CCP in Cl₂)

Example (Cl₂ plasma at 40 mTorr):

  P_coil = 1000 W → n_e ≈ 5×10¹⁵ m⁻³
  P_coil = 2000 W → n_e ≈ 7×10¹⁵ m⁻³
  P_coil = 4000 W (hypothetical) → n_e ≈ 10¹⁶ m⁻³
  
  Scaling: Doubling coil power → √2× (~1.4×) plasma density increase
  
  Practical: 1500-2000 W typical (higher power allows faster etch)

Ion flux consequence:

Flux to electrode ∝ n_e × v_thermal
  
  where v_thermal = √(kT_e / m_e)
  
  Higher n_e → higher ion flux φ_ion
  
  Ion flux density: φ_ion ~ 10¹⁵ cm⁻²s⁻¹ at 2000 W coil
  
Etch rate scaling:

R_etch = R_chemical + R_sputtering
       ∝ √(P_coil) + Y × φ_ion
       ∝ √(P_coil) + Y × √(P_coil)
       ≈ k × √(P_coil)  (for typical etch, R dominated by chemistry/sputtering)
  
  Practically: Doubling coil power → ~40% faster etch (not 2×, due to plasma saturation)

Temperature coefficient:

Electron temperature rises with power:
  T_e(P) ∝ P^0.3 (empirical scaling)
  
  At P_coil = 1000 W: T_e ≈ 3.5 eV
  At P_coil = 2000 W: T_e ≈ 4.2 eV
  At P_coil = 4000 W: T_e ≈ 5.0 eV
  
  Higher T_e → more high-energy electrons → better dissociation
  Effect: Cl• production increases with power (partly independent of density scaling)
```

### 6.1.2 Bias Power & Ion Energy

```
Bias voltage creates sheath at electrode:

Electrode (wafer chuck) at negative bias:
  Electrons repelled (too light, move faster)
  Ions attracted (positive, move slower)
  Space-charge region forms: sheath

Sheath voltage builds until:
  Ion current from plasma = electron current to electrode
  (quasi-neutrality in plasma bulk)

Ion energy in sheath:

Ion enters sheath at T_e ≈ few eV
Accelerated across sheath voltage V_bias
Gains energy: E_ion = e × V_bias (approximately)

Self-bias estimation:

For symmetric electrode geometry:
  V_self−bias ≈ 0.3 × V_bias
  
  (Coefficient ~0.3, depends on geometry)

Example:

Bias power = 800 W, 13.56 MHz
Voltage amplitude: V = √(2 × P × R) / (ω × C)
  (Simplified; actual complex impedance network)
  
Typical: V_bias ≈ √(2 × 800) ≈ 40 V (voltage amplitude)
Peak voltage: ~60 V (peak-to-peak ~120 V)
Average DC bias: ~0.3 × 60 ≈ 20 V (conservative)
Ion energy: E_ion ≈ 20 eV

More practical observation:

Direct measurement or empirical relationship:
  E_ion ≈ 0.3 × √(P_bias / frequency_factor)
  
At 13.56 MHz, 800 W bias:
  E_ion ≈ 70 eV typical (experimentally observed)

Energy tuning via bias power:

P_bias = 400 W → E_ion ≈ 35-50 eV (low energy, selective)
P_bias = 800 W → E_ion ≈ 70 eV (standard)
P_bias = 1500 W → E_ion ≈ 100 eV (high energy, faster but less selective)

Independence from coil power:

Key advantage of CCP:
  Coil power controls flux (n_e, φ_ion)
  Bias power controls energy (E_ion)
  Independent tuning possible!
  
ICP cannot do this (only one power source controls both)
```

---

## 6.2 Ion Energy Distribution (IED)

### 6.2.1 IED Shape & Temperature Dependence

```
Ion energy distribution (IED):

Not monochromatic; ions have range of energies
Gaussian-like distribution centered on E_ion

Typical IED in Cl₂ plasma (13.56 MHz):

Energy (eV) | Intensity (norm) | Notes
0-20        | 10%              | Low energy tail
20-40       | 25%              | Rising edge
40-60       | 35%              | Peak region (E_ion ~50 eV mean)
60-80       | 20%              | Falling edge
80-120      | 10%              | High energy tail

FWHM (full width half maximum):
  FWHM ≈ 20-40 eV typical
  
  Lower E_ion → narrower IED (more monochromatic)
  Higher E_ion → broader IED (wider spread)
  
  Ratio FWHM / E_ion ≈ 0.3-0.5 (30-50% of mean energy)

Temperature effect on IED:

At room temperature (20°C):
  E_ion ≈ 70 eV, FWHM ≈ 25 eV

At elevated temperature (100°C substrate):
  Substrate heats wafer → wafer heats electrode
  T increases → plasma temperature slightly increases
  Coefficient: ≈ +0.2 to +0.3 eV per °C
  
  E_ion(100°C) ≈ 70 + (100−20) × 0.25 ≈ 90 eV
  Effect: ~30% ion energy increase!

Implication for etch:

If recipe tuned at room T:
  E_ion = 70 eV, selectivity optimized
  
When substrate heats during etch:
  E_ion drifts to 90 eV (mid-etch)
  Selectivity degrades ~20-30% (sputtering contribution increases)
  Profile may degrade
  
Solution:
  Monitor substrate temperature during etch
  Cool substrate with backside He (if available)
  Or accept temperature drift as process variation (tight process window)
```

### 6.2.2 Ion Energy Distribution Model

```
Analytical IED model (Maxwellian approximation):

f(E) ∝ √E × exp(−E / E_eff)

where E_eff is effective energy scale

Normalization:
  ∫ f(E) dE = 1 (total probability)

Mean energy:
  ⟨E⟩ = ∫ E × f(E) dE ≈ 1.5 × E_eff

Peak energy (mode):
  E_peak = 0.5 × E_eff

FWHM calculation:
  E_half = E_eff × ln(2) ≈ 0.69 × E_eff
  Bounds at I(E) = 0.5 × I_max:
  
  FWHM ≈ 2 × √(2 ln(2) × E_eff) ≈ 2.35 × √(E_eff)
  
Example (E_eff = 25 eV):
  ⟨E⟩ ≈ 37.5 eV
  E_peak ≈ 12.5 eV
  FWHM ≈ 17 eV
  
  Matches experimental observation for low-energy distribution

Pressure effect on IED:

Lower pressure → fewer collisions
  Less thermalization in sheath
  Narrower, more monochromatic IED
  FWHM/E_ion ratio decreases
  
  At 5 mTorr: FWHM ≈ 15-20 eV (narrow)
  At 50 mTorr: FWHM ≈ 25-35 eV (broader)
  At 100 mTorr: FWHM ≈ 30-40 eV (very broad)

Practical consequence:

High-selectivity recipes use low pressure:
  Narrow IED → more ions at peak energy
  Fewer scattered low-energy ions (less sputtering on dielectric)
  Better selectivity window

Uniformity recipes use higher pressure:
  Broader IED and more scattered ions
  Better radial uniformity (less edge effects)
  Trade-off: Lower selectivity
```

---

## 6.3 Spatial Uniformity & Edge Effects

### 6.3.1 Center vs. Edge Plasma Density

```
Radial non-uniformity in CCP:

Coil magnetic field not perfectly uniform:
  Center stronger than edge (geometry)
  
Plasma density profile:
  n_e(r) = n_e,center × (1 − (r/R)^2 × factor)
  
  where factor ~ 0.2-0.4 (depends on coil design)

Radial variation:

At center (r = 0): n_e = 100% (baseline)
At mid-radius (r = 0.5R): n_e ≈ 90-95%
At edge (r = R): n_e ≈ 80-90%

Result:
  Center: 10-20% higher plasma density than edge
  Ion flux center ~15% > edge

Etch rate variation:

R ∝ √(n_e) (if flux-limited)

Radial etch rate:
  Center: +7-10% faster
  Edge: −7-10% slower
  Across-wafer non-uniformity: 15-20% total

Compensation strategies:

1. Showerhead design:
   Smaller holes at center (restrict flow)
   Larger holes at edge (allow more flow)
   Result: Uniform pressure across wafer
   Effect: Partially compensates etch rate non-uniformity
   Achievable: ±5-8% residual variation

2. RF tuning:
   Increase power slightly (drives higher plasma everywhere)
   If center saturation higher → edge benefit larger
   Result: May flatten radial profile
   Complicated; rarely used

3. Multi-step recipe:
   Use faster recipe in center-heavy step
   Use slower recipe in edge step
   Result: Can balance over multiple steps

Production acceptance:
  ±10% non-uniformity acceptable (typical)
  ±5% excellent (requires careful design + tuning)
  >±15% poor (rework or process change needed)
```

### 6.3.2 Edge Ring Compensation

```
Electrode edge ring (outer annular section):

Design:
  Wafer sits on main electrode (200 mm diameter)
  Outer ring around it (210-220 mm diameter)
  Ring isolated electrically, separate bias RF connection
  
Function:
  Adjustable bias voltage on ring
  Compensate edge plasma deficiency
  
Operation:

Normal electrode: V_bias = 800 V (40 V DC equivalent)
Edge ring: V_bias = 900-1000 V (50-55 V DC)

Higher bias on ring → higher E_ion at edge
Effect: More sputtering at edge → faster etch
Result: Compensates lower n_e at edge

Tuning:

Measure uniformity (CD-SEM or etch rate test across wafer)
Adjust ring voltage incrementally:
  +50 V on ring → typically 2-3% more etch at edge
  
Target: Match center and edge etch rates
Typical final ring voltage: +50-150 V vs. main electrode

Effectiveness:
  Can reduce across-wafer non-uniformity from ±10% to ±3-5%
  Cost: One additional RF power supply (~$50-100K)
  Payback: Improved yield (tighter process window)

Trade-off:
  Ring complicates electrode design, maintenance
  Additional tuning knob (adds to recipe complexity)
  Some fabs use it, some avoid it (standardize without ring)
```

---

## 6.4 Summary & Key Takeaways

1. **Coil Power Controls Flux** — Plasma density n_e ∝ √(P_coil); doubling coil power → 1.4× more plasma; etch rate increases ~40% (not linear, due to saturation).

2. **Bias Power Controls Energy** — Ion energy E_ion ≈ 0.3 × V_bias; independent of coil power; allows flux/energy decoupling (CCP advantage over ICP).

3. **IED Broadens with Pressure** — Low-P (5 mTorr) gives narrow IED ~15 eV FWHM (selective); high-P (100 mTorr) gives broad IED ~40 eV (uniform but less selective).

4. **Temperature Increases E_ion** — Substrate heating ~+0.25 eV/°C; 80°C rise → ~20 eV higher E_ion → ~30% selectivity loss; backside cooling mitigates.

5. **Center Plasma Denser 15%** — Radial coil geometry; causes 15-20% etch rate non-uniformity (center faster); showerhead design can partially compensate.

6. **Edge Ring Fine-Tunes Uniformity** — Adjustable bias on outer ring compensates edge deficiency; reduces non-uniformity ±10% → ±3-5%; adds cost, complexity.

7. **CCP Independent Control Key** — Separate coil and bias RF enables recipe flexibility (fast bulk via coil, selective finish via low bias); ICP cannot do this.

---

**Next Chapter:** [Chapter 7 - Metal Corrosion & Tool Lifetime](./07-metal-corrosion.md)

**Chapter 6 Development Status:** Complete ion source and energy control framework  
**Version:** 1.0

