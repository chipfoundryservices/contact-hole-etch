# Chapter 3: Etch Chemistry - Halogen Systems

## Overview

Contact-hole etch uses chlorine and fluorine chemistry to achieve metal/dielectric selectivity. This chapter quantifies reaction mechanisms, kinetics, and selectivity—the foundation for process tuning.

**Learning Objectives:**
- Understand Cl₂, F₂, and Br₂ dissociation pathways
- Model etch rate temperature and pressure dependence
- Quantify ion vs. radical contributions
- Design selectivity ratios for multi-layer etch
- Predict byproduct formation and residue

---

## 3.1 Chlorine Plasma Chemistry

### 3.1.1 Cl₂ Dissociation Pathways

```
Electron-impact dissociation of Cl₂:

Primary pathway (most important):
  e⁻ + Cl₂ → e⁻ + 2Cl•
  
  Dissociation energy: D ≈ 2.5 eV
  Electron threshold: ~2.5 eV
  Cross-section peak: σ_max ≈ 2-3 × 10⁻¹⁵ cm² at ~8 eV electron energy
  
  Electron temperature in CCP: T_e ≈ 3-5 eV (kT in electron Volts)
  Dissociation rate: Fraction of electrons >2.5 eV: ~70-80%
  Result: High Cl• production rate

Secondary pathway (ionization):
  e⁻ + Cl₂ → Cl⁺ + Cl + 2e⁻
  
  Ionization energy: I ≈ 12.7 eV
  Electron threshold: 12.7 eV
  Cross-section: σ ≈ 0.5 × 10⁻¹⁵ cm² (lower than dissociation)
  
  Ionization rate: ~10-20% of dissociation rate
  Result: Cl⁺ ion production (secondary etch channel)

Ion composition in Cl₂ plasma:
  Cl⁺ (from ionization): ~10% of ion current
  Cl₂⁺ (molecular ion, rare): <1%
  Other ions (H₂O⁺, O⁺ from residuals): ~5-10%
  
  Dominant species: Cl• radical (>60% of reactive species)

Temperature dependence of dissociation:

Boltzmann distribution of electrons:
  f(E) = (2π) × (E^0.5 / (π × (kT_e)^1.5)) × exp(−E / kT_e)
  
  At T_e = 3 eV:
    Fraction with E > 2.5 eV: ~30% (lower T, fewer high-energy electrons)
  At T_e = 5 eV:
    Fraction with E > 2.5 eV: ~70% (higher T, more dissociation)
  
  Cl• production scales with T_e^0.5 (roughly; detailed rate coefficient nonlinear)
```

### 3.1.2 Chlorine Etch Kinetics

```
Etch rate model (W or Si in Cl₂ plasma):

Material + nCl• → Volatile products

Reaction rate (Langmuir-Hinshelwood model):
  R = k × f_Cl• × θ_empty
  
  where:
    k: Surface reaction rate constant (temperature-dependent)
    f_Cl•: Cl• neutral flux to surface
    θ_empty: Fraction of surface sites available (depends on coverage)

Simplified rate equation (typical for etch):
  R = k(T) × [Cl•]^m × P^n
  
  Exponents:
    m ≈ 1 (first order in Cl•)
    n ≈ −0.5 (half-order in pressure, due to ion-assist)
  
  Result: Higher pressure → lower etch rate (at constant Cl•)
          Lower pressure → higher etch rate (and better selectivity possible)

Arrhenius temperature dependence:
  k(T) = A × exp(−E_a / RT)
  
  For W etch by Cl•:
    E_a ≈ 8-10 kcal/mol (low activation energy)
    T = 293 K (20°C): k ∝ exp(−8 / (1.987×10⁻³ × 293)) = exp(−13.8)
    T = 373 K (100°C): k ∝ exp(−8 / (1.987×10⁻³ × 373)) = exp(−10.8)
    Ratio k(100°C) / k(20°C) = exp(3.0) ≈ 20× (etch 20× faster at 100°C!)

For SiO₂ etch by Cl•:
  E_a ≈ 20-25 kcal/mol (higher than W, more temperature-dependent)
  T = 293 K: k ∝ exp(−22 / (1.987×10⁻³ × 293)) = exp(−37.8)
  T = 373 K: k ∝ exp(−22 / (1.987×10⁻³ × 373)) = exp(−29.8)
  Ratio k(100°C) / k(20°C) = exp(8.0) ≈ 3000× (massive increase!)

Selectivity vs. temperature:
  S(T) = R_W / R_SiO₂
  
  At constant [Cl•]:
    S(T) ∝ exp((E_a,SiO₂ − E_a,W) / RT)
         = exp((20 − 8) / RT)
  
  At T = 20°C:
    S ∝ exp(12 / (1.987×10⁻³ × 293)) = exp(20.6) ≈ 10⁹ (mathematically huge!)
    Practical: ~100-500:1 (limited by other factors like pressure, additive gases)
  
  At T = 100°C:
    S ∝ exp(12 / (1.987×10⁻³ × 373)) = exp(16.2) ≈ 10⁷ (still huge)
    Practical: ~50-200:1 (lower, but still selective)

Conclusion: Selectivity improves dramatically at lower temperature!
           (This is why room-temperature contact etch works; heating would reduce selectivity)
```

### 3.1.3 Byproduct Formation

```
Chlorine etch byproducts:

Tungsten etching:
  W + 6Cl• → WCl₆ (primary product, volatile)
  
  WCl₆ properties:
    Molar mass: 384 g/mol
    Boiling point: 346°C (VOLATILE at room T, escapes as gas)
    Partial pressure at 20°C: ~1 Torr (very volatile)
  
  Secondary products:
    WCl₅ (solid at room T, possible redeposition)
    WCl₄ (solid, more redeposition risk)
    WOCl₄ (if O₂ present, lower volatility)

Silicon etching:
  Si + 4Cl• → SiCl₄
  
  SiCl₄ properties:
    Molar mass: 170 g/mol
    Boiling point: 58°C (volatile, but can condense at wafer surface)
    Partial pressure at 20°C: ~100 Torr (volatile)
  
  At cryogenic conditions (not used in contact etch):
    SiCl₄ can condense (forms liquid), creating residue

SiO₂ etching:
  SiO₂ + 6Cl• → SiCl₄ + 2CO + 2CO₂
  (Complex stoichiometry, some CO/CO₂ formation)
  
  Byproducts:
    SiCl₄ (volatile, as above)
    CO (semi-volatile, mostly escapes)
    CO₂ (fully volatile)
    Possible O-Cl compounds (less volatile)

Copper etching:
  Cu + 2Cl• → CuCl₂
  
  CuCl₂ properties:
    Molar mass: 135 g/mol
    Melting point: 630°C
    Boiling point: 993°C (NOT VOLATILE at room T!)
    
  Risk: CuCl₂ deposits on chamber walls, residue accumulates
        Requires plasma ashing (O₂) to remove CuCl₂ after etch

Titanium etching:
  Ti + 2Cl• → TiCl₂ (solid product, partially volatile)
  
  TiCl₂ properties:
    Boiling point: 1500°C (nearly non-volatile!)
    Partial pressure at 20°C: <10⁻⁶ Torr (essentially solid)
  
  Risk: TiCl₂ residue significant; post-etch ashing essential
```

---

## 3.2 Fluorine Chemistry & Selectivity Tuning

### 3.2.1 F₂ vs. Cl₂ Selectivity

```
Fluorine etch of materials (for comparison to Cl₂):

F₂ dissociation:
  e⁻ + F₂ → e⁻ + 2F•
  Dissociation energy: D ≈ 1.6 eV (lower than Cl₂)
  Cross-section: Similar, but activation lower
  Result: F• production slightly higher than Cl•

F• radical reactivity (vs. Cl•):
  F• is more reactive (higher valence, smaller size)
  Etch W faster: ~100-200 nm/min (similar to Cl₂)
  Etch SiO₂ faster: ~10-30 nm/min (vs. 2-5 nm/min for Cl₂)
  
  Selectivity W/SiO₂:
    Cl₂: ~50-100:1
    F₂:  ~5-20:1 (much less selective!)

Why use Cl₂ for contact etch (not F₂)?

  F₂ reacts too fast with everything (poor selectivity)
  Contact etch MUST stop cleanly on dielectric (tight timing)
  Cl₂ provides better selectivity (margin for over-etch)
  
  F₂ preferred for: Hard-mask etch, high-selectivity blanket etch
  Cl₂ preferred for: Multi-layer selective etch (contacts, vias)

Mixed halogen chemistry:

Cl₂ + HBr (hydrogen bromide):
  Provides Cl•, Br•, and H atoms
  Br• etch rate similar to Cl•
  H atoms reduce some byproducts
  Selectivity tuning: Can vary Cl:Br ratio to adjust chemistry
  Result: Better profile control in some cases

Cl₂ + F₂ (rarely used, difficult):
  Competitive dissociation of both
  Complex plasma chemistry
  Not standard for contact etch (unpredictable)
```

### 3.2.2 Selectivity Tuning Strategies

```
Pressure modulation:

At constant gas composition:
  Lower pressure: Higher ion fraction, more ion-assist
  Result: Etch W faster, SiO₂ slower (selectivity improves)
  
  At 5 mTorr: W 100 nm/min, SiO₂ 1 nm/min (100:1 selectivity)
  At 50 mTorr: W 50 nm/min, SiO₂ 2 nm/min (25:1 selectivity)
  At 100 mTorr: W 30 nm/min, SiO₂ 3 nm/min (10:1 selectivity)
  
  Reason: Low pressure → more directed plasma, better ion-surface coupling

Temperature tuning:

Lower temperature: Improves selectivity (higher E_a difference)
  At 20°C: S ≈ 100-200:1 (excellent)
  At 100°C: S ≈ 50-100:1 (good)
  At 200°C: S ≈ 20-50:1 (marginal)

Cost: Lower temperature means higher cooling requirement (expensive)

Additive gas strategy:

O₂ addition (1-5% of gas):
  Forms protective SiO₂ layer on dielectric sidewalls
  Effect: SiO₂ etch rate drops further (more selective)
  
  At 0% O₂: W 100 nm/min, SiO₂ 2 nm/min (50:1)
  At 3% O₂: W 90 nm/min, SiO₂ 0.5 nm/min (180:1 selectivity!)
  
  Cost: Slightly longer etch time, but better profile

HBr addition (0.5-2% of gas):
  Modifies ion/radical balance
  Can improve profile (sidewall protection)
  Variable effect on etch rate depending on ratio

N₂ or Ar diluent:
  Dilutes active Cl•, slows etch
  Can improve uniformity (reduces ARDE at high AR)
  Etch time increases proportionally
```

---

## 3.3 Ion Contribution to Etch

### 3.3.1 Physical Sputtering by Cl⁺

```
Ion-driven sputtering (vs. chemical etch by Cl•):

Sputtering yield (atoms/ion):
  W at 100 eV Cl⁺: Y ≈ 0.2-0.3
  Si at 100 eV: Y ≈ 0.5-0.8
  SiO₂ at 100 eV: Y ≈ 0.3-0.4

Sputtering contribution to total etch rate:
  For W etch:
    Chemical (Cl•): ~80-90% of total
    Physical (Cl⁺): ~10-20% of total
    
  For SiO₂ etch:
    Chemical (Cl•): ~60-70% of total
    Physical (Cl⁺): ~30-40% of total
    
  Reason: SiO₂ more resistant to chemical etch, so physical contribution larger

Ion energy effect on selectivity:

Higher ion energy → More physical sputtering (less selective):
  At E_ion = 50 eV: W/SiO₂ selectivity ~60:1 (good)
  At E_ion = 100 eV: W/SiO₂ selectivity ~40:1 (moderate)
  At E_ion = 200 eV: W/SiO₂ selectivity ~20:1 (poor)
  
  Reason: High-energy ions sputter SiO₂ more efficiently
           while W sputtering already saturates

Conclusion: Lower ion energy improves selectivity
           (chemical etch advantage over physical sputtering)

Production recipe strategy:
  Step 1 (bulk etch): High power, high E_ion (fast)
  Step 2 (selective): Low power, low E_ion (better selectivity, profile)
```

### 3.3.2 Ion-Assisted Chemical Etch

```
Combined ion-chemistry model:

Etch rate decomposition:
  R_total = R_chemical + R_sputtering
  
  R_chemical ∝ [Cl•] × exp(−E_a / kT)
  R_sputtering ∝ Y(E_ion) × φ_ion

Example: W etch at standard conditions

  Chemical component:
    Cl• density: ~10¹² cm⁻³
    E_a ≈ 9 kcal/mol
    Rate: ~40 nm/min
  
  Sputtering component:
    Y ≈ 0.25, φ_ion ≈ 10¹⁵ cm⁻²s⁻¹
    Rate: ~10 nm/min
  
  Total: 50 nm/min

If bias power reduced (lower E_ion):
  Ion energy drops (coefficient 0.3 × V_bias)
  Y(E_ion) decreases ~30%
  φ_ion increases (coil power constant, easier plasma formation)
  
  Result: Sputtering component drops but chemical stays same
          Total etch rate: ~45 nm/min (small change)
          But selectivity improves (SiO₂ sputtering reduced more)
```

---

## 3.4 Summary & Key Takeaways

1. **Cl₂ Primary Etch Source** — Dissociation via electron impact creates Cl• radicals; 70-80% of electrons have E >2.5 eV dissociation threshold; Cl• flux dominates etch rate.

2. **W Etch Temperature-Independent** — E_a ≈ 9 kcal/mol; etch rate changes ~20× from 0°C to 100°C; F_W etch can proceed at room T (unlike STI F₂ which slows at cold temps).

3. **SiO₂ Highly Temperature-Dependent** — E_a ≈ 22 kcal/mol; etch rate changes ~3000× from 20°C to 100°C; selectivity (W/SiO₂) scales exp((22−9) / RT) ≈ exp(20-30).

4. **Selectivity Optimization Multi-Lever** — Temperature (lower better), pressure (lower better), additive gases (O₂ improves), ion energy (lower better); typical contact etch ~100-200:1 W/SiO₂.

5. **Byproducts Volatile or Non-Volatile** — WCl₆ escapes freely (boiling pt 346°C); TiCl₂ and CuCl₂ non-volatile (require post-etch ashing); residue control critical.

6. **Ion Contribution Secondary** — Physical sputtering 10-20% of W etch rate, 30-40% of SiO₂; reducing E_ion improves selectivity by suppressing SiO₂ sputtering.

7. **F₂ Less Selective Than Cl₂** — Better for dielectric etch; Cl₂ chosen for contact work (multi-layer selectivity); HBr/Cl₂ blends offer tuning options.

---

**Next Chapter:** [Chapter 4 - Contact Resistance & Performance](./04-contact-performance.md)

**Chapter 3 Development Status:** Complete etch chemistry and selectivity framework  
**Version:** 1.0

