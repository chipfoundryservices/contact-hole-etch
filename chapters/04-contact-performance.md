# Chapter 4: Contact Resistance & Performance

## Overview

Contact resistance directly impacts circuit performance (delay), power consumption, and device yield. This chapter quantifies resistance mechanisms, measurement techniques, and reliability—bridging etch process to electrical outcomes.

**Learning Objectives:**
- Understand specific contact resistivity (ρ_c) and measurement via TLM
- Model resistance degradation from defects (undercut, residue, oxidation)
- Quantify leakage mechanisms (junction, TAT, GIDL)
- Design for contact reliability (TDDB, EM)
- Correlate etch defects to yield loss

---

## 4.1 Contact Resistance Fundamentals

### 4.1.1 Specific Contact Resistivity (ρ_c)

```
Definition:

Specific contact resistivity is the resistance per unit area at contact interface:
  ρ_c = R_c × A
  
  Units: Ω·µm² (or Ω·cm² when scaled)
  
  Inverse: Conductivity (G/A = 1 / ρ_c)

Physical origin:

Thermionic emission over Schottky barrier:
  J = A* × T² × exp(−φ_B / kT) × (exp(qV / kT) − 1)
  
  where:
    A*: Richardson constant
    T: Absolute temperature
    φ_B: Barrier height
    V: Applied voltage

Measured at room temperature:

W contact on p-Si:
  Typical: ρ_c ≈ 0.5-1.0 Ω·µm²
  Best case (excellent interface): ~0.1-0.3 Ω·µm²
  Worst case (damaged, oxidized): >2-5 Ω·µm² (spec fail)

Cu contact on TaN:
  Typical: ρ_c ≈ 0.1-0.3 Ω·µm² (better than W/Si)
  Best case: ~0.05-0.1 Ω·µm²
  Worst case: >1 Ω·µm²

Temperature dependence:

Arrhenius form:
  ρ_c(T) = ρ_c0 × exp(q × φ_B / kT)
  
  Temperature coefficient: α_ρ ≈ 1-3%/°C (positive, resistance increases with T)
  
  At 125°C (elevated temp):
    ρ_c increases ~20-50% from room T value
    This affects circuit timing (interconnect delay increases)

Scaling with feature size:

Total contact resistance:
  R_total = ρ_c / A + R_via (series connection)
  
  where A = π × r² (contact area)
  
  For W contact (45 nm diameter, r = 22.5 nm):
    A ≈ 1590 nm²
    ρ_c = 1 Ω·µm² = 10⁻¹⁵ Ω·cm²
    R_c = 10⁻¹⁵ / 1590 ≈ 0.63 Ω (from contact resistivity alone)
  
  Total (with via resistance ~0.1 Ω):
    R_total ≈ 0.73 Ω per contact
  
  For 7 nm node (much smaller contact, ~20 nm diameter):
    A ≈ 314 nm²
    R_c ≈ 10⁻¹⁵ / 314 ≈ 3.2 Ω (10× higher!)
    Contact scaling → resistance scales inversely with area
    
  Result: Smaller nodes face higher contact resistance (need better ρ_c)
```

### 4.1.2 TLM (Transmission Line Model) Measurement

```
TLM test structure:

Designed to extract ρ_c from multiple contacts in parallel:

                 Metal Line (width W)
        ─────────────────────────────
        │      │      │      │      │
        L₁     L₂     L₃     L₄     
        
   contacts at spacing L₁, L₂, L₃, L₄ apart
   (L₁ < L₂ < L₃ < L₄)

Measurement procedure:

1. Apply voltage between two contacts
2. Measure resistance vs. spacing
3. Plot total resistance (R_total) vs. spacing (L)

Linear relationship:
  R_total(L) = 2R_c + R_sheet × (L / W)
  
  where:
    R_c: Contact resistance (both ends)
    R_sheet: Sheet resistance of metal line
    L: Contact spacing
    W: Line width

Data fitting:
  Slope = R_sheet / W
  From slope, extract sheet resistance
  
  Y-intercept = 2R_c
  From intercept, extract contact resistance

Specific resistivity extraction:
  From R_c and known contact area:
  ρ_c = R_c × A

TLM accuracy:

Typical measurement accuracy: ±10-20%
For large W: ~5% accuracy
For small W: ~20% accuracy (contact area uncertainty)

Production usage:

Run TLM on witness wafer after contact etch
Extract ρ_c value
Compare to spec: Must be <1 Ω·µm² (or process-specific target)
If >1.5 Ω·µm²: Recipe out-of-spec, troubleshoot
```

---

## 4.2 Resistance Degradation from Defects

### 4.2.1 Undercut & Its Effect

```
Undercut definition:

Lateral etch beyond intended feature edge:
  Intended: 50 nm diameter contact
  Actual undercut: 5 nm lateral (creates 60 nm effective diameter)
  
  OR (more commonly):
  Intended: 50 nm contact
  Actual: 45 nm diameter (under-etched by 5 nm)
  This is actually "over-etch" into edge (negative undercut)

Lateral etch mechanism:

Anisotropic etch (Cl₂ direct ion path): Minimal lateral etch
Isotropic etch (radicals from sides): Creates lateral etch

At high AR contact, shadowing prevents ions from reaching sidewalls
Radicals diffuse inward from sides
Net: Undercut = combination of isotropic radical etch + ion shadowing edge effects

Resistance impact:

Area reduction:
  Area_nominal = π × (25)² = 1963 nm²
  With 5 nm undercut: Area = π × (20)² = 1257 nm²
  Area loss: 36% (not linear with diameter change because it's squared!)
  
  Resistance increase: R ∝ 1/A
  R_new / R_old = 1963 / 1257 = 1.56 (56% increase!)

Undercut of 10 nm (very severe):
  Area = π × (15)² = 707 nm²
  Area loss: 64%
  Resistance increase: 2.8× (280% increase!)

Specification impact:

If ρ_c nominal = 0.5 Ω·µm²:
  With no undercut: R_c ≈ 0.6 Ω (meets <1 Ω spec)
  With 5 nm undercut: R_c ≈ 0.94 Ω (still OK, but margin gone)
  With 10 nm undercut: R_c ≈ 1.7 Ω (FAIL spec)

Production acceptance:

Undercut <5 nm: Good
Undercut 5-10 nm: Marginal (borderline spec)
Undercut >10 nm: Fail (rework required)

Yield correlation:

Undercut from process variation (non-uniform across wafer):
  Center: 3 nm undercut (R = 0.7 Ω)
  Edge: 8 nm undercut (R = 1.2 Ω)
  
  If spec <1.0 Ω: Edge contacts fail
  Yield loss: ~20% (edge region non-functional)
```

### 4.2.2 Residue Impact on Resistance

```
Residue film on contact floor:

Composition: Metal fluorides (WF₆ partially volatile, deposits as WCl₂/WCl₃)
Thickness: 2-10 nm typical (depends on etch time, material)
Conductivity: Insulating to semiconducting (poor)

Two failure mechanisms:

1. Insulating layer effect (most severe):
   
   If residue is truly insulating:
     ~5 nm WCl₂ layer on floor
     Barrier height for electron tunneling: φ ≈ 1-2 eV
     Tunneling current exponentially low
     Resistance >> 100 Ω (near-open circuit, device fails!)

2. Contact pinning height rise:
   
   If residue partially conducting:
     Effective contact interface shifts upward
     Contact no longer on Si, but on residue/W interface
     Different φ_B (different semiconductor)
     ρ_c increases by 10-100× (empirically measured)
     
     Example:
       Nominal ρ_c (W/Si): 0.5 Ω·µm²
       With 5 nm residue (W/WCl₂/Si): ρ_c ≈ 5-10 Ω·µm²
       Contact resistance: 5-10× higher than spec

Production consequence:

Residue-free etch: ρ_c = 0.5 Ω·µm² (100% yield)
5 nm residue layer: ρ_c = 5 Ω·µm² (0% yield, 100% fail)
Post-etch ashing (removes residue): ρ_c = 0.6 Ω·µm² (restored, 99% yield)

Cost-benefit:
  Add ashing step: +5 min per wafer, +$2K process equipment
  Prevents 100% yield loss from residue
  Payback: Immediate (worth doing for every contact etch)

Specification:
  Residue thickness: <1 nm preferred, <2 nm acceptable, >3 nm FAIL
  Post-etch residue check: SEM, TEM, or plasma XPS
```

### 4.2.3 Oxidation & Surface Degradation

```
Metal oxidation during etch:

Tungsten oxidation (W → WO₃):
  Oxide thickness without O₂ additive: <0.5 nm typical
  With O₂ additive (for selectivity): 1-3 nm typical
  Post-etch stored in air: +1-2 nm additional oxidation per day

WO₃ properties:
  Resistivity: ~10¹⁴ Ω·cm (insulating)
  Dielectric constant: ~8 (higher than SiO₂)

Resistance impact:
  ~1 nm WO₃ barrier: R increases ~5-10× (conduction via tunneling)
  ~3 nm WO₃: R increases ~100× (significant degradation)

Copper oxidation (faster than W):
  Air storage, no capping:
    1 hour: ~0.5 nm CuO
    8 hours (overnight): ~2-3 nm (visible color change)
    1 day: ~5 nm (strong resistivity increase)
  
  CuO resistivity: ~10⁴ Ω·cm (semiconducting, not insulating but poor)
  Resistance increase: ~30-50× after 1 day in air

Production impact:

Contact etch Monday, no capping:
  Same day (0 hours): R_c = 0.3 Ω (good)
  Monday night (12 hours): R_c = 2-3 Ω (marginal, failing spec)
  Tuesday morning (24 hours): R_c = 5+ Ω (fail)
  
  Process appears to have degraded overnight!
  Solution: Capping layer (Al, TiN) within 30 seconds post-etch
           Prevents oxidation completely
  
With capping:
  Monday etch: R_c = 0.3 Ω
  Tuesday morning: R_c = 0.31 Ω (stable, unchanged)
  
Prevention:
  Immediate capping: Best (eliminates oxidation risk)
  N₂ atmosphere storage: Good (removes O₂, slows oxidation)
  Refrigerated storage: Helps (lowers oxidation kinetics ~2× per 10°C)
```

---

## 4.3 Leakage Mechanisms

### 4.3.1 Junction Leakage

```
Reverse-biased diode leakage (W contact on p-Si):

Diode saturation current:
  I_0 = q × n_i² × (D_p / L_n × N_A + D_n / L_p × N_D)
  
  where:
    n_i: Intrinsic carrier concentration (~10¹⁰ cm⁻³ at 300 K)
    D_p, D_n: Diffusion coefficients
    L_n, L_p: Diffusion lengths
    N_A, N_D: Doping concentrations
  
  Typical I_0 ≈ 10⁻¹³ A for Si pn junction

Reverse bias current (ideal diode):
  I_reverse ≈ I_0 (independent of bias, until breakdown)

At −0.5 V reverse bias (typical operating condition):
  Ideal diode: I ≈ 10⁻¹³ A (1× 10⁻¹³ A)
  Per contact (45 nm diameter): I_per_contact ≈ 10⁻¹⁴ A = 10 pA

Specification:
  <100 pA per contact acceptable (100× margin above ideal)
  <50 pA preferred (200× margin)
  >1 nA: Indicates defect, investigate

Defect leakage:

Ion implantation damage increases n_i locally:
  Defective region: n_i,defect ≈ 10¹² cm⁻³ (100× higher)
  I_0,defect ≈ 100× I_0,ideal
  Reverse current: 1-10 pA (starting at 100 pA baseline, reaches 1 nA at −1 V)

Yield impact:
  5% of contacts exceed 1 nA leakage spec: 5% yield loss
  With process improvement (less damage): <1% yield loss
```

### 4.3.2 Trap-Assisted Tunneling (TAT)

```
Interface traps at Si/SiO₂ contact:

Trap density D_it (cm⁻² eV⁻¹):
  
  High-quality thermal oxide: D_it ~10¹⁰ (excellent)
  CVD SiO₂: D_it ~10¹¹-10¹² (worse)
  Plasma-damaged oxide: D_it ~10¹²-10¹³ (very poor)

TAT current mechanism:

Electron tunnels from Si band edge to trap state, then to metal:
  J_TAT ∝ D_it × exp(−E_t / kT)
  
  where E_t: Trap binding energy

Temperature dependence:
  At 300 K: J_TAT ∝ exp(−E_t / (0.026 eV))
  E_t ≈ 0.2 eV typical:
  
  J_TAT ∝ exp(−0.2 / 0.026) = exp(−7.7) ≈ 4 × 10⁻⁴
  (Extremely small at room T)
  
  At 125°C (elevated, kT = 0.0335 eV):
  J_TAT ∝ exp(−7.4) ≈ 6 × 10⁻⁴
  (Still small, but slightly higher)

Leakage contribution:

High-quality contact (D_it ~10¹⁰):
  TAT contribution negligible
  Junction leakage dominates
  Total leakage: ~10 pA/contact

Damaged contact (D_it ~10¹² from ion implantation):
  D_it increases 100×
  TAT contribution: ~1000 pA/contact (100× increase)
  Leakage spec failure (>100 pA)

Yield impact:

Process with high ion energy (>150 eV bias):
  Creates more substrate damage
  D_it increases → leakage increases
  Yield loss: ~10-20% from leakage fail
  
Process with low ion energy (<50 eV bias):
  Minimal substrate damage
  D_it stays low
  Yield loss: <1% from leakage
  
Trade-off: Lower E_ion better selectivity (better for profile)
           but slower etch rate (longer cycle time)
```

### 4.3.3 Gate-Induced Drain Leakage (GIDL)

```
GIDL mechanism:

Occurs at junction edge with high gate bias
Gate attracts carriers, creates high field at junction
Band-to-band tunneling at junction edge: electrons tunnel from valence to conduction

Relevant for: Junction contacts (Si → metal), NOT metal-to-metal vias

For contact etch:
  Only relevant if contact is near transistor junction
  Not primary leakage mechanism (junction TAT dominates)

Specification:
  GIDL typically <10 pA at operating gate voltage
  Most contact defects fail on junction/TAT leakage before GIDL
  
Production:
  Monitor as secondary check
  Usually correlated with junction leakage failures
```

---

## 4.4 Reliability: TDDB & Electromigration

### 4.4.1 Time-Dependent Dielectric Breakdown (TDDB)

```
TDDB in contact barrier:

If contact includes thin oxide or interface layer:
  Reverse bias voltage creates electric field across oxide
  Long-term: Trap accumulation → breakdown

E-field at barrier:
  V_bias = 0.5 V across 1 nm SiO₂ layer
  E = 0.5 V / 1 nm = 5 MV/cm (very high!)
  
  Oxide breakdown field: E_BD ≈ 8-10 MV/cm
  
  Safe field: <3 MV/cm (for long-term reliability)
  Marginal: 3-5 MV/cm (acceptable but risky)
  Dangerous: >5 MV/cm (high failure rate)

TDDB lifetime model:

Weibull distribution of breakdown time:
  t_BD = t_0 × exp(E_0 / E_field)
  
  where E_0 ≈ 1-2 MV/cm (material parameter)

Example (SiO₂ barrier):
  At E_field = 2 MV/cm: t_BD ≈ 10-100 years (excellent)
  At E_field = 3 MV/cm: t_BD ≈ 1-10 years (acceptable)
  At E_field = 4 MV/cm: t_BD ≈ 1 month (unacceptable!)
  At E_field = 5 MV/cm: t_BD ≈ 1 day (catastrophic!)

Voltage tuning for reliability:

Operating voltage must keep field <3 MV/cm:
  For 1 nm interface layer: V_max = 3 V safe
  For 2 nm interface layer: V_max = 6 V safe
  
Production acceptance:
  Typical contact operating: 0.5-1.0 V (very safe, E < 1 MV/cm)
  High-power contexts: Up to 1.5-2 V (still safe)

Yield consideration:
  TDDB failures rare in production (well-designed bias)
  Mostly a long-term field issue (10+ year operation)
  Specified but not major yield driver in early production
```

### 4.4.2 Electromigration (EM)

```
Electromigration in contact metal:

Electron wind force on metal atoms:
  Metal atoms (W, Cu) drift under high current density
  Voids form (atoms leave), hillocks form (atoms accumulate)

Current density limit for contact:

Tungsten (W via):
  J_max ≈ 10⁶-10⁷ A/cm² at moderate current (conservative spec)
  Depending on temperature
  
For 45 nm diameter contact (A ≈ 1600 nm²):
  Current limit: I_max ≈ 10⁶ A/cm² × 1.6 × 10⁻⁷ cm² ≈ 0.16 mA
  
  Typical operating current: <1 µA (huge margin)
  High-power circuits: Up to 100 µA (still safe)
  
  Only problematic at extreme current density (power delivery)

EM lifetime:

Black's equation:
  t_f = K / (J^n) × exp(E_a / kT)
  
  where:
    K: Material constant
    n ≈ 2 (current density exponent)
    E_a ≈ 0.5 eV (activation energy)
    J: Current density
  
  Lifetime extremely sensitive to J: Doubling J → 4× shorter life

Production:
  Contact EM rarely problematic (<10 µA typical)
  Power delivery vias (multi-via stacks) at risk (100+ µA)
  Not primary concern for low-current signal contacts
```

---

## 4.5 Summary & Key Takeaways

1. **Specific Contact Resistivity Critical** — ρ_c 0.5-1.0 Ω·µm² typical; inversely proportional to contact area (smaller nodes need better ρ_c); TLM test extracts ρ_c from multi-contact structure.

2. **Undercut Devastating** — 5 nm undercut = 56% resistance increase; 10 nm undercut = 180% increase; area loss quadratic with undercut depth; specification <5 nm typical.

3. **Residue Most Damaging Defect** — 5 nm WCl₂ residue → 10× resistance increase; post-etch ashing essential (removes residue, restores ρ_c); residue control >99% yield difference.

4. **Oxidation Rapid for Cu** — W oxidizes ~0.1 nm/day in air; Cu oxidizes ~1-2 nm/day; capping layer (Al, TiN) within 30 seconds required; prevents overnight resistance increase 10-100×.

5. **Leakage Multi-Sourced** — Junction (ideal 10 pA), TAT from interface traps (10× per 100× D_it increase), GIDL secondary; total spec <100 pA typical; ion damage increases D_it, increases leakage.

6. **Ion Energy Trade-off** — Lower E_ion better for selectivity and leakage (less substrate damage); but slower etch rate (longer cycle time); multi-step recipe balances both.

7. **Reliability Usually Not Yield Driver** — TDDB lifetime >10 years at typical bias (<3 MV/cm); EM not problematic at <100 µA; process defects (ρ_c, leakage, undercut) dominate yield, not reliability.

---

**End of Part I: Fundamentals (Chapters 1-4) COMPLETE**

**Next:** Part II - Hardware Design (Chapters 5-9)

**Chapter 4 Development Status:** Complete contact performance and electrical specification framework  
**Version:** 1.0

