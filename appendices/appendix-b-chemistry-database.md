# Appendix B: Chemistry Database

Comprehensive reference for etch chemistry, reaction mechanisms, thermodynamics, and byproduct behavior in contact-hole etch processes.

---

## B.1 Chlorine (Cl₂) Dissociation & Radical Generation

```
Primary reaction pathway:

Electron-impact dissociation:
  e⁻ + Cl₂ → e⁻ + 2Cl•
  
Cross-section vs. electron energy:
  E_e < 2.5 eV: σ ≈ 0 (threshold)
  E_e = 2.5 eV: σ ≈ 0.1 × 10⁻¹⁵ cm²
  E_e = 5 eV: σ ≈ 2.0 × 10⁻¹⁵ cm² (peak)
  E_e = 10 eV: σ ≈ 1.5 × 10⁻¹⁵ cm² (declining)
  
Production impact:
  Typical CCP plasma T_e ≈ 3-5 eV (peak cross-section)
  Cl• generation efficient (good radical production)

Radical flux from plasma:

Generation rate φ_gen ∝ n_e × Cl₂ pressure × ⟨σv⟩

where ⟨σv⟩ = electron-Cl₂ collision rate

Typical values:
  Plasma density n_e: 10⁹-10¹⁰ cm⁻³
  Cl₂ pressure: 30-50 mTorr
  ⟨σv⟩ ≈ 10⁻⁷ cm³/s
  
  φ_gen ≈ 10¹⁵-10¹⁶ cm⁻² s⁻¹ (agrees with measured W etch rates)

Recombination & loss:

Cl• + Cl• → Cl₂ (gas phase recombination)
  Rate: 2nd order in [Cl•]
  Lifetime τ_Cl ≈ 1-10 ms (short, diffusive loss dominates)

Three-body recombination:
  Cl• + Cl• + M → Cl₂ + M (M = buffer gas)
  Increases with pressure (more collisions)
  N₂ diluent enhances recombination (explains ARDE reduction)
```

---

## B.2 Tungsten Etch Mechanism

```
Elementary steps (Cl₂ plasma):

1. Cl• radical approach:
   Cl• + W(surface) → Cl-W* (adsorbed complex)
   
2. Abstraction/oxidation:
   Cl-W* + Cl• → WCl₂ (leaves surface)
   or
   Cl-W* + 2Cl• → WCl₃ (intermediate)
   
3. Higher chloride formation:
   WCl₂ + Cl• → WCl₃
   WCl₃ + Cl• → WCl₄
   WCl₄ + Cl• → WCl₅
   WCl₅ + Cl• → WCl₆ (final product)

4. Desorption/escape:
   WCl₆ (volatile, BP 346°C) → Gas phase
   WCl₄ (semi-volatile) → mostly escapes, some deposits
   WCl₂, WCl₃ (low volatility) → may deposit on sidewalls

Rate law:

Etch rate = k(T) × [Cl•]^n × (function of ion energy)

where:
  k(T) = A × exp(-E_a / RT)
  E_a ≈ 9 kcal/mol (low activation energy, chemistry facile)
  n ≈ 1 (first-order in Cl radical flux)
  Ion contribution ≈ 10-20% (sputtering assists chemical)

Temperature dependence:

R(T) = R_ref × exp[−E_a / R × (1/T − 1/T_ref)]

At T_ref = 293 K (20°C), R_ref = 100 nm/min:

T (°C) | T (K)  | R (nm/min) | Relative rate
--------|--------|-----------|---------------
20      | 293    | 100       | 1.0 (reference)
40      | 313    | 105       | 1.05
60      | 333    | 110       | 1.10
80      | 353    | 115       | 1.15
100     | 373    | 120       | 1.20

Production note:
  Low E_a means etch rate only moderately temperature-dependent
  Selectivity MUCH more temperature-dependent (E_a difference is large)
```

---

## B.3 SiO₂ Etch Mechanism (O₂ Additive Protection)

```
Without O₂ additive:

Cl• can slowly etch SiO₂ (high activation energy):
  Cl• + SiO₂ → SiCl + O• (slow, E_a ≈ 22 kcal/mol)
  
Selectivity: S = R_W / R_SiO₂ ≈ 50-100:1 (moderate)

With O₂ additive (protective mechanism):

1. O• radical generation (from O₂ dissociation):
   e⁻ + O₂ → e⁻ + 2O•
   
2. Protective layer formation:
   O• + SiO₂(surface) → SiO₂ + O₂ (further oxidizes already-oxide)
   or more likely:
   O• + O• → O₂ (recombines, forms neutral O₂ not-reactive)
   
3. Net effect:
   Cl• concentration at SiO₂ surface reduced (O• competes for adsorption sites)
   SiO₂ etch rate suppressed by 50-70%
   W etch rate reduced only 10-20% (Cl• still abundant for W)

Selectivity with O₂:

O₂ level | S_W/SiO₂ | W rate drop | SiO₂ rate drop | Net S improvement
---------|----------|-------------|---------------|-----------------
0%       | 50:1     | baseline    | baseline       | baseline
1%       | 100:1    | −8%         | −50%           | +100% (2×)
3%       | 150:1    | −15%        | −65%           | +200% (3×)
5%       | 140:1    | −20%        | −60%           | +180% (saturation)

Oxygen partial pressure threshold:

Below 0.5% O₂: Minimal protective effect
0.5-1%: Sharp improvement regime (steep selectivity gain)
1-3%: Linear improvement regime (steady gain)
3-5%: Saturation (diminishing returns)
>5%: Slight degradation (too much O₂ suppresses W etch)

Production recipe typically uses 2-3% O₂ (optimal balance)
```

---

## B.4 Byproduct Thermodynamics & Volatility

```
Tungsten chloride species (vapor pressure data):

Species | Formula | MW   | BP (°C) | Status at room T | Deposition risk
--------|---------|------|---------|-----------------|----------------
WCl₂    | WCl₂    | 253  | ~1500   | Solid/liquid    | HIGH (residue)
WCl₃    | WCl₃    | 289  | ~1000   | Solid           | HIGH (residue)
WCl₄    | WCl₄    | 324  | ~600    | Liquid/solid    | MODERATE
WCl₅    | WCl₅    | 360  | ~400    | Liquid          | LOW-MOD
WCl₆    | WCl₆    | 396  | 346     | Liquid/gas      | LOW (mostly escapes)

Chamber conditions (30 mTorr, 30°C):

WCl₆ (BP 346°C):
  At 30°C: Far below BP, but partial pressure still high
  Escape probability: ~90% (mostly exits chamber)
  Deposition on cold surfaces: ~10%
  
WCl₂/WCl₃ (BP >1000°C):
  At 30°C: Far below BP, negligible vapor pressure
  Escape probability: ~5% (mostly deposits immediately)
  Deposition risk: ~95% (major residue source)
  
Production consequence:
  Multi-step chlorides (WCl₆ primary) escape via pump
  Lower chlorides (WCl₂, WCl₃) deposit on sidewalls/floor
  Post-etch ashing removes WCl₂/WCl₃ via oxidation

Copper chloride species:

CuCl:  Sublimes ~1100°C, at room T solid
CuCl₂: Decomposes >540°C, at room T solid
Both: Non-volatile, stick to chamber/electrodes
Consequence: Cu etch produces more residue than W etch
Workaround: Lower bias (reduce ion energy, slower Cu etch to reduce chloride generation)
```

---

## B.5 Reaction Rates & Rate Constants

```
Chemical etch rate law:

R = k(T) × n_radical^n × exp(−E_barrier / k_B T)

Temperature dependence:

k(T) = k₀ × exp(−E_a / RT)

where:
  k₀: Pre-exponential factor (10¹² to 10¹⁴ s⁻¹ typical)
  E_a: Activation energy (kcal/mol)
  R: Gas constant (1.987 × 10⁻³ kcal/mol/K)
  T: Absolute temperature (K)

Arrhenius plot (log k vs. 1/T):

W etch (E_a ≈ 9 kcal/mol, low slope):
  Etch rate relatively insensitive to temperature
  Doubling etch rate requires ~50°C rise
  
SiO₂ etch (E_a ≈ 22 kcal/mol, steep slope):
  Etch rate highly temperature-sensitive
  Temperature change of 20°C changes rate by ~30%
  
Selectivity (difference in E_a):
  S(T) ∝ exp[(E_a,SiO₂ − E_a,W) / RT]
  ΔE_a = 13 kcal/mol
  Every 50°C → selectivity change of ~30%

Radical concentration dependency:

Etch rate ∝ [Cl•]^n where n ≈ 0.7-1.2 (typically ~1)

Linear regime: R ∝ Cl₂ pressure (at constant plasma)
Saturation regime: R plateaus (all available radicals consumed)

Production implication:
  Increasing Cl₂ flow always increases etch rate (linear)
  But diminishing returns at high flow (still linear, but cost rises)
  Typical: 150-300 sccm Cl₂ per 300mm chamber
```

---

## B.6 Plasma Species Diagnostic Guide

```
Key species to monitor via RGA (mass spectrometry):

m/z | Species | Source | Production concern
----|---------|--------|-------------------
2   | H₂      | Contamination | Moisture/contamination
18  | H₂O     | Leak or gas | HIGH CONCERN: moisture causes oxidation, kills selectivity
28  | N₂      | Intentional additive or leak | Monitor if using N₂ diluent
32  | O₂      | Intentional additive or leak | Monitor O₂ level (specify 1-3%)
35  | Cl•     | Plasma radical | Hard to detect directly (radical)
36  | HCl     | Reaction byproduct | Minor signal, normal
40  | Ar      | Calibration gas | Use as reference
70  | Cl₂     | Main gas flow | Monitor main gas level
300-400 | WCl_x | Etch byproduct | Byproduct, expected during etch

RGA scan interpretation:

During normal Cl₂ etch:
  Cl₂ (m/z 70): 25-30 mTorr (main signal)
  Cl• (m/z 35): <0.1 mTorr direct (hard to measure, radicals don't ionize well)
  WCl_x (300+): <0.001 mTorr (byproducts, mostly escape)
  H₂O (m/z 18): <0.5 mTorr (acceptable, low contamination)
  N₂ (m/z 28): 0-10 mTorr (depending if diluent used)
  
If H₂O > 1 mTorr:
  ALERT! Moisture ingress or leak
  Response: Pump down, bake-out, check for leaks
  Impact: Severe (oxidation layers form, selectivity collapses)

If O₂ < 0.3 mTorr (expecting 1-3%):
  Check O₂ MFC (supply pressure, flow setting)
  Impact: Selectivity degraded (50:1 vs. 150:1 expected)
```

---

## B.7 Quick Reference: Activation Energies & Temperature Coefficients

```
Species/Process | E_a (kcal/mol) | Temperature coeff | Notes
----------------|----------------|------------------|--------------------------------------------
W etch (Cl₂)    | 9              | +0.2%/°C         | Low sensitivity, ~20°C for 2× rate
SiO₂ etch       | 22             | +0.8%/°C         | High sensitivity, ~8°C for 2× rate
Selectivity S   | 13 (ΔE_a)      | −3%/°C (loss)    | 100:1 → 40:1 across 0-100°C window
WO₃ oxidation   | 0.5 eV (~11.5) | Variable         | Thermal/E-field dependent
Metal diffusion | 2-3 eV         | Very temp-dep    | Affects corrosion rates
Ion range in Si | −               | E_ion^0.5        | ~√(E_ion) penetration law
Plasma density  | −               | ∝ P_coil         | Doubling coil → 1.4× plasma density

Production rule of thumb:
  Every 20°C substrate rise → 20-30% selectivity loss
  Every 10 mTorr pressure increase → 20% ARDE reduction, selectivity ±10%
  Every 100W bias increase → etch rate +5-10%, selectivity −5%
```

---

**Appendix B Development Status:** Complete chemistry database  
**Version:** 1.0

