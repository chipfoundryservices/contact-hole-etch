# Chapter 2: Metal & Dielectric Materials

## Overview

Contact-hole etch must selectively etch through multiple materials with different chemistry and oxidation rates. This chapter quantifies material properties, etch selectivity, and oxidation kinetics—the foundation for recipe design.

**Learning Objectives:**
- Understand tungsten and copper properties, etch rates, and oxidation
- Quantify titanium/TaN barrier selectivity
- Model thermal and CVD oxide etch
- Characterize low-K dielectrics (mechanical, chemical)
- Predict material degradation during etch

---

## 2.1 Tungsten (W) in Contact Etch

### 2.1.1 Tungsten Properties & Structure

```
Tungsten atomic and material properties:

Atomic number: 74
Atomic mass: 183.84 g/mol
Electron configuration: [Xe] 4f¹⁴ 5d⁴ 6s²

Crystal structure:
  Cubic (body-centered cubic, BCC)
  Lattice parameter: a = 3.165 Å
  Density: 19.3 g/cm³ (very dense, ~2× Al)

Electrical properties:
  Resistivity (bulk, 20°C): ρ ≈ 5.6 µΩ·cm (moderate, vs. Cu 1.7 µΩ·cm)
  Temperature coefficient: +0.4-0.5%/°C
  Barrier work function: ~4.5 eV (good for p-type, moderate for n-type)

Mechanical properties:
  Elastic modulus: E ≈ 400 GPa (very stiff, high internal stress in thin films)
  Yield strength: σ_y ≈ 200-300 MPa (high strength)
  Thermal conductivity: κ ≈ 180 W/m·K (good, ~50% of Cu)
  CTE: α ≈ 4.5 ppm/°C (2× higher than Si, CTE mismatch risk)

Film stress in via fill:
  Intrinsic (growth stress): σ_intrinsic ≈ 500-2000 MPa (compressive typical)
  Thermal stress (cool-down from 800°C anneal):
    ΔT = 780°C, Δα = 2.0 ppm/°C (W vs. Si)
    σ_thermal ≈ 0.4 × 780 × 2.0 ≈ 600 MPa (additional tensile)
  Total: 1000-2600 MPa residual stress (can cause hillock formation, diffusion)
```

### 2.1.2 Tungsten Etch Chemistry

```
Chlorine etch of tungsten:

Primary reaction:
  W + xCl• → WCl_x (volatile etch products)
  
  For stoichiometric: W + 6Cl• → WCl₆↑
  Molar mass WCl₆: 384 g/mol
  
  Actual x varies (WCl₅, WCl₄ solid intermediates)

Reaction kinetics:
  Rate equation: R = k × [Cl•]^n
  n ≈ 1 (first order in Cl radical)
  Temperature dependence:
    k(T) = A × exp(−E_a / kT)
    E_a ≈ 8-10 kcal/mol (relatively low, etch fast even at room T)
  
  Typical Cl• density: ~10¹² cm⁻³
  Collision frequency: ν ≈ 10⁹ s⁻¹
  Etch rate: ~50-200 nm/min at standard conditions (very fast!)

Ion-assisted etch:
  Cl⁺ ions (100-150 eV) physically sputter W: Y ≈ 0.1-0.3 atoms/ion
  Sputtering contribution: ~10-20% of total etch rate
  
  Physical sputtering rate:
    R_sputter = Y × φ_ion × M / (ρ × N_A)
              ≈ 0.2 × 10¹⁵ × 184 / (19.3×10²³) ≈ 2 nm/sec ≈ 120 nm/min
  
  Combined chemical+physical: 50-200 nm/min typical

Byproducts:
  WCl₆: Volatile, escapes to exhaust
  WCl₅, WCl₄: Partially volatile, some redeposition risk
  WOCl₄: Forms if oxygen present (etch slows)
```

### 2.1.3 Tungsten Oxidation During Etch

```
Oxidation mechanism:

W + O₂ → WO₃ (at elevated temperature)

Oxidation kinetics (Arrhenius model):
  Rate: dx/dt = k × exp(−E_a / RT)
  where x = oxide thickness
  
Parabolic growth (diffusion-limited):
  x = √(2Dt)  (if diffusion controls)
  D: diffusion coefficient of O through oxide
  
Linear growth (reaction-limited, observed at low T):
  x = vt (linear in time)
  v ≈ rate constant

Experimental data (room temperature oxidation of W):
  After 1 hour in air: ~1-2 nm WO₃ layer
  After 24 hours: ~3-5 nm
  After 1 week: ~5-10 nm (saturation ~10 nm)

During etch (in oxidizing plasma or with O₂ additive):
  Simultaneous etch (Cl•) and oxidation (O₂)
  Net rate depends on balance
  
  100% Cl₂: Etch fast, minimal oxidation
  Cl₂ + 5% O₂: Etch rate 70%, oxidation layer ~1-2 nm forms
  Cl₂ + 10% O₂: Etch rate 50%, oxidation layer ~3-5 nm
  
Oxidation layer consequence:
  WO₃ resistivity: ~10¹⁴ Ω·cm (insulating!)
  Even 1 nm layer increases contact resistance ~10× (conduction through oxide)
  5 nm layer: >1000× resistance increase (near-open circuit)

Anti-oxidation strategy:
  Post-etch H₂ plasma: Reduces WO₃ → W (for recovery)
  N₂ additive during etch: Suppresses O₂ oxidation
  Immediate capping: Al or Ti deposited <1 sec post-etch
```

---

## 2.2 Copper (Cu) in Via Fill

### 2.2.1 Copper Properties

```
Copper in interconnect:

Atomic number: 29
Atomic mass: 63.55 g/mol
Crystal structure: FCC
Density: 8.96 g/cm³

Electrical:
  Resistivity: ρ ≈ 1.7 µΩ·cm (best of common metals, ~3× better than W)
  Temperature coefficient: +0.4%/°C
  
Mechanical:
  Elastic modulus: E ≈ 110 GPa (softer than W)
  Yield strength: σ_y ≈ 60-100 MPa (weaker than W)
  CTE: α ≈ 16.5 ppm/°C (3.7× higher than Si, very high mismatch)

Electrical performance advantage:
  Via resistance at fixed geometry: ~50% lower than tungsten
  Power dissipation: ~50% lower (I²R loss)
  Advantage diminishes at high current density (electromigration risk)
```

### 2.2.2 Copper Oxidation & Corrosion

```
Copper oxidation pathways:

2Cu + O₂ → 2CuO (fast, black oxide)
4Cu + O₂ → 2Cu₂O (fast, red oxide)
3Cu + 2H₂O + O₂ → 2Cu(OH)₂ (with moisture)

Oxidation kinetics (room temperature, air):
  After 1 min: ~0.5 nm oxide layer (fast initial oxidation)
  After 10 min: ~2-5 nm
  After 1 hour: ~10-20 nm
  After 1 day: ~50-100 nm (visible red/black tarnish)

Oxide properties:
  CuO: Resistivity ~10⁴ Ω·cm (resistive but not insulating)
  Cu₂O: Resistivity ~10⁶ Ω·cm (more resistive)
  Even thin oxide (1-2 nm) doubles contact resistance
  10 nm oxide: >100× resistance increase

During etch (Cl₂ with trace O₂ or moisture):
  Chlorine etches Cu: Cu + 2Cl• → CuCl₂ (fast)
  But oxidation accelerates: CuO formation simultaneous
  
  Rate balance:
    Pure Cl₂: Fast etch, minimal oxidation
    With air/O₂: Slower etch, significant oxidation (CuCl + CuO mix)
    With moisture: Etch slows further, Cu(OH)₂ forms

Corrosion during storage:
  Copper via left in air >1 hour: ~1-2 nm oxide
  >1 day: ~5-10 nm (resistance impact measurable)
  
  Production impact:
    Via etch Monday 5 PM, no capping
    Tuesday 9 AM measurement: 10× higher resistance than Monday
    Process appears to have failed; actually oxide corrosion only

Prevention:
  Capping layer (Al, TiN) deposited within 30 seconds post-etch
  N₂ purge atmosphere post-etch (remove O₂, moisture)
  Vacuum storage if possible (eliminate oxidation)
```

---

## 2.3 Barrier Materials (Ti, TaN)

### 2.3.1 Titanium (Ti) Barrier

```
Titanium barrier function:

Placed between Cu/W and dielectric to:
  1. Prevent Cu diffusion into dielectric (blocks Cu migration)
  2. Provide adhesion to dielectric
  3. Act as etch stop (different chemistry than metal)

Typical thickness: 5-15 nm (ultrathin, just enough to block diffusion)

Properties:
  Density: 4.51 g/cm³
  Resistivity: ρ ≈ 42 µΩ·cm (high, 25× higher than Cu!)
  Elastic modulus: E ≈ 100-120 GPa

Etch selectivity vs. dielectrics:
  Ti etch rate (Cl₂): ~20-50 nm/min (moderate)
  SiO₂ etch rate: ~1-5 nm/min (slow due to selectivity)
  Ti/SiO₂ selectivity: ~10-20:1
  
  Ti etch rate: ~30-80 nm/min
  SiN etch rate: ~5-20 nm/min (SiN more resistant than SiO₂)
  Ti/SiN selectivity: ~5-10:1

Etch chemistry:
  Ti + 2Cl• → TiCl₂ (forms solid intermediate, some sticking)
  TiCl₂ + energy → volatile products or redeposition
  
  Can create residue: TiCl₂, TiCl₄ partially volatile
  Requires post-etch cleaning (ashing) to remove Ti residue

Barrier integrity risk:
  If etched through: Cu diffuses into dielectric
  Device degrades (barrier failure)
  Typical spec: Stop within ±50% of nominal thickness
  (If 10 nm nominal, stop between 5-15 nm)
```

### 2.3.2 Tantalum Nitride (TaN) Barrier

```
TaN advantages over Ti:

Chemical formula: Ta₂N, TaN (varies with deposition)
Density: 13.8 g/cm³
Resistivity: ρ ≈ 50-150 µΩ·cm (still high but better than Ti for current spreading)

Etch selectivity:
  TaN etch rate (Cl₂): ~30-100 nm/min (similar to Ti)
  SiO₂: ~1-5 nm/min (same)
  TaN/SiO₂ selectivity: ~10-20:1 (same as Ti)
  
  But TaN better as diffusion barrier (denser, more stable)

Etch chemistry:
  TaN + 3Cl• → TaCl₃ + N₂ (TaCl₃ more volatile than TiCl₂)
  Less residue risk than Ti
  
  N₂ byproduct: Contributes to gas-phase reactions

Residue after TaN etch:
  TaCl₃ mostly volatile
  Some TaCl₂ or oxynitride residue possible
  Generally cleaner than Ti (easier post-etch cleaning)

Production preference:
  Modern processes prefer TaN over Ti (better reliability, less residue)
  TaN thickness: 5-20 nm (slightly thicker for better barrier properties)
```

---

## 2.4 Dielectric Materials

### 2.4.1 Thermal vs. CVD Silicon Dioxide

```
Thermal SiO₂:
  Growth on Si by high-temperature oxidation (800-1000°C)
  Formula: Si + O₂ → SiO₂
  
  Properties:
    Density: 2.20 g/cm³
    Dielectric constant: κ ≈ 3.9
    Refractive index: n ≈ 1.46
    Band gap: E_g ≈ 9 eV (very wide, excellent insulator)
    Thermal conductivity: κ_th ≈ 0.01 W/m·K (poor, insulating)
    CTE: 0.5 ppm/°C (very low)
    Tensile strength: ~100-200 MPa
    Young's modulus: E ≈ 70-80 GPa

  Interface quality:
    D_it (Si/SiO₂ interface trap density): ~10¹⁰ cm⁻² eV⁻¹ (excellent)
    Charge density: <10¹¹ cm⁻² (very low)
    Breakdown strength: E_BD ≈ 8-10 MV/cm
  
  Etch rate (in Cl₂ plasma):
    With high selectivity mode: ~1-5 nm/min
    E_a (activation energy): ~20-25 kcal/mol (higher than W or Cu)

CVD SiO₂:
  Deposited by decomposition of silane (SiH₄) or tetraethylorthosilicate (TEOS)
  SiH₄ + O₂ → SiO₂ + H₂ (plasma or high-T pyrolysis)
  
  Properties:
    Density: 2.0-2.1 g/cm³ (slightly lower than thermal)
    Dielectric constant: κ ≈ 4.0-4.2 (slightly higher due to defects)
    Interface trap density: D_it ≈ 10¹¹-10¹² cm⁻² eV⁻¹ (worse than thermal)
    Contains trapped water/defects from process
  
  Etch rate similar to thermal SiO₂
  But slower Si/SiO₂ selectivity possible (due to impurities)

Selectivity tuning (Cl₂ vs. SiO₂):
  Pure Cl₂: SiO₂ etch slow (~1-3 nm/min)
  Cl₂ + O₂ additive: SiO₂ etch even slower (~0.5-1 nm/min)
    (O₂ forms protective SiO₂ layer on sidewalls)
  Cl₂ + HBr additive: SiO₂ etch variable (HBr can etch SiO₂)
```

### 2.4.2 Silicon Nitride (Si₃N₄)

```
Silicon nitride properties:

Stoichiometry: Si₃N₄ (but varies Si/N ratio in deposited films)
Density: 3.1 g/cm³ (denser than SiO₂)

Dielectric:
  κ ≈ 7-8 (higher than SiO₂, more capacitive)
  E_BD ≈ 10-12 MV/cm (slightly higher than SiO₂)

Mechanical:
  Young's modulus: E ≈ 300 GPa (much stiffer than SiO₂)
  Tensile strength: ~500-800 MPa (much stronger)
  CTE: 3-4 ppm/°C (closer to Si than SiO₂)
  Internal stress (as-deposited): 1-2 GPa (compressive, very high)

Interface:
  Si/SiN interface trap density: D_it ≈ 10¹¹ cm⁻² eV⁻¹ (poor)
  More charged traps than Si/SiO₂
  Higher leakage if used as primary dielectric

Etch rate (in Cl₂ plasma):
  ~5-20 nm/min (5-10× slower than Si!)
  Very selective to Si

Why SiN as barrier:

Example: Contact etch through SiO₂ to SiN to reach W
  W etch: 100-150 nm/min (fast)
  SiO₂ etch: 2-5 nm/min (slow, 20-50× selectivity to W)
  SiN etch: 1-2 nm/min (very slow, 50-100× selectivity to W)
  
  Total selectivity (W vs. SiN): ~100-200:1 (excellent stopping power!)
  
  Process: Etch W fast, then etch through SiO₂ slowly, stop cleanly on SiN
  Selectivity gap ensures stop layer is thick enough for margin
```

### 2.4.3 Low-K Dielectrics (SiOC, SiLK, Porous)

```
Low-K material motivation:

Traditional SiO₂: κ = 3.9
Low-K target: κ < 3.0 (reduces RC delay in interconnect)

Typical low-K options:

1. SiOC (Organosilicate glass):
   κ ≈ 2.5-3.0
   Contains Si-O backbone with organic C substituents
   Density: 1.2-1.5 g/cm³ (lower than SiO₂)
   Modulus: E ≈ 5-8 GPa (much softer, weak!)
   CTE: 10-20 ppm/°C (higher than SiO₂)

2. SiLK (polyphenylene derivative):
   κ ≈ 2.65
   Organic polymer-based
   Density: 1.3 g/cm³
   Modulus: E ≈ 3 GPa (very weak, fragile)
   CTE: 30-40 ppm/°C (very high, severe mismatch)

3. Porous Low-K (pSiOC, porous SiLK):
   κ ≈ 2.0-2.5 (lowest k achieved)
   Contains air pockets (porosity ~30-50%)
   Modulus: E ≈ 1-2 GPa (extremely weak, easily broken)
   Permeability: Moisture can diffuse in (degradation risk)

Etch sensitivity:
  SiOC: Moderate etch rate (~5-15 nm/min in Cl₂)
  SiLK: Fast etch (organic, burns away in O₂ plasma)
  Porous: Very fast etch, structural collapse risk
  
Damage during etch:
  Ion bombardment can break weak C-O bonds
  Create micro-cracks in low-K
  Increase defect density
  Modulus degrades further (post-etch E drops 20-50%)
  
  Device performance impact: Interconnect delay increases (loses low-K benefit)

Post-etch issue:
  Low-K fragile; cannot survive aggressive ashing
  Require gentle post-etch cleaning (avoid ion bombardment)
  Trade-off: Incomplete residue removal vs. material damage
```

---

## 2.5 Summary & Key Takeaways

1. **Tungsten Etch Fast, Oxidation Slow** — W etch rate 50-200 nm/min in Cl₂ (very fast); oxidation minimal without O₂ additive; WO₃ layer <0.5 nm post-etch typical.

2. **Copper Oxidizes Rapidly** — Cu oxidation 10× faster than W; 1-2 nm oxide forms in air within hours; capping layer or N₂ purge essential to preserve low resistance.

3. **Barrier Selectivity Critical** — Ti/TaN create 10-20:1 selectivity stop for dielectric etch; residue risk (TiCl₂) requires post-etch cleaning; TaN preferred over Ti (better barrier, less residue).

4. **Thermal SiO₂ Highest Quality** — Interface trap density 10¹⁰ cm⁻² eV⁻¹ (best); CVD SiO₂ worse (10¹¹-10¹² defects); affects device performance and reliability.

5. **SiN Excellent Stop Layer** — 50-100:1 selectivity to W via SiO₂; enables multi-layer selective etch with wide process window; 5-20× slower than SiO₂ etch.

6. **Low-K Fragile During Etch** — SiOC/SiLK modulus 1-8 GPa (soft); ion bombardment and aggressive post-etch damage material; requires gentle etch and ashing protocols.

7. **CTE Mismatch High** — Cu (16.5 ppm/K) vs. Si (2.6) creates 13.9 ppm/K mismatch; W (4.5 ppm/K) much better; stress relief structures needed for Cu vias.

---

**Next Chapter:** [Chapter 3 - Etch Chemistry Halogen Systems](./03-etch-chemistry.md)

**Chapter 2 Development Status:** Complete materials and etch properties framework  
**Version:** 1.0

